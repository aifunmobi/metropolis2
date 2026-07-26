# CLAUDE.md - Metropolis 3D City Simulation

## Project Overview

Metropolis is an interactive 3D city simulation built as a **single HTML file** using Three.js. Users can fly through a living city and observe urban life including vehicles, pedestrians, weather, and random events.

## File Structure

```
metropolis/
├── metropolis-3d-city-7.html  # The entire application (single file, ~9000 lines)
└── README.md                  # Project documentation
```

## Architecture

### Single-File Design
The entire application is contained in `metropolis-3d-city.html`:
- **HTML structure** (lines 1-77): Canvas, HUD, minimap, loading screen, controls overlay
- **CSS styles** (lines 7-56): Embedded in `<style>` tag
- **JavaScript** (lines 78-end): ES module using Three.js from CDN

### Core Systems

All systems follow a **make/update pattern**: `mk*()` functions create objects, `upd*()` functions update them each frame.

| System | Create Function | Update Function | Description |
|--------|-----------------|-----------------|-------------|
| City Layout | `mkCityLayout()` | - | 4x4 grid of roads, sidewalks, crosswalks |
| Buildings | `mkBuildings()`, `mkBuilding()` | `updWindowLights()` | Dynamic buildings with flickering windows |
| Traffic Lights | `mkTrafficLights()`, `mkTL()` | `updTL()` | 4-way intersection signals |
| Cars | `mkCars()`, `mkCar()` | `updCars()` | Regular vehicles obeying traffic |
| Emergency | `mkEmergencyVehicles()` | `updEmergencyLights()` | Police, fire, ambulance |
| Buses | `mkBuses()`, `mkDoubleDecker()`, `mkJitney()` | - | Tourist and jitney buses |
| Omnibus | `createOmnibusLine()`, `mkOmnibus()` | `updOmnibus()` | Fixed route with boarding |
| Pedestrians | `mkPeds()`, `mkPed()` | `updPeds()` | Citizens with state machine |
| Bicycles | `mkBicycles()`, `mkBicycle()` | `updBicycles()` | Cyclists that ignore lights |
| Weather | - | `updWeather()`, `updRain()`, `updStormDebris()` | Sunny/cloudy/rain/storm |
| Special Events | Various `create*()` | `updSpecialEvents()`, `updateEvent()` | Random city events |
| Secrets | `mkSecrets()`, `mkUFO()`, `mkBalloon()`, `mkHelicopter()` | `updSecrets()` | Hidden discoverable objects |
| Billboards | `mkBillboards()` | `updBillboards()` | Animated rooftop signs |
| Shops | `mkStorefronts()`, `addShopUnit()`, `SHOP_CATALOG` | `updShops()`, `updShopTooltip()` | ~110 unique ground-floor stores, product windows, hover tooltips |
| Ped population | - | `updPedPopulation()` | Street crowd size follows time of day |
| Airport | `mkAirport()`, `mkJet()`, `mkJetBridge()` | `updAirport()` | RDU-style airport east of town (x≈100-215): Terminals 1/2, garage, jets, animated jet bridges, taxi/bus fleet |
| Street life | `mkStreetLife()`, `mkCinema()`, `mkFoodCart()`, `mkNewsstand()`, `mkStreetArtist()`, `mkDogWalkerUnit()` | `updStreetLife()`, `updCinemaCrowd()`, `updIdlers()` | Cinema with chasing marquee + box-office queue, food carts, newsstands, pavement artists, dog walkers |
| Outskirts | `mkOutskirts()` | - | Low-rise sprawl beyond the grid so downtown has a horizon; windows painted into the facade texture |
| Wall ads | `mkWallAds()` | - | Painted billboards with gooseneck floodlights on blank upper storeys |
| Airport fleet | `mkCourtesyBus()`, `mkAirportCar()`, `mkApronTug()`, `mkFuelTruck()`, `mkCateringTruck()`, `mkBeltLoader()`, `mkFollowMeCar()` | `updAirport()` | Ground fleet drives along its own +Z, so wheels use `vWheel(..., {zFwd:true})`; `apBeacon()` adds the rotating amber |
| Obstacles | `addObstacle()` | `resolveObstacles()`, `resolveWalkers()` | Bucketed static-collision field; keeps walkers out of furniture, carts and parked cars |
| Vehicle kit | `vWheel()`, `vLamp()`, `vLightbar()`, `vStripe()`, `vehSize()` | `spinWheels()` | Shared parts bin + per-vehicle footprints (`userData.len`/`wid`) that drive every traffic clearance |

### Visual conventions

- **Facade texturing** — `facadeBox()` tiles each wall by real metres (`FACADE_TILE`); a
  single stretched material makes brick come out the size of a car. `tiledTex()` caches
  the repeat variants.
- **Building form** — plinth (`PLINTH_H`) + shaft + belt course + `mkRoofKit()` (cornice,
  parapet, HVAC, water tower). Windows start above the plinth and stop below the cornice.
- **Ground layers** — everything flat declares its own depth layer via `polygonOffset`
  (yards < roads < repairs < markings). Sharing a `y` causes z-fighting while moving.
- **Vehicle clearances** — never hardcode a gap. Use `vGap()` / `vSide()` so a 14m artic
  and a 2.3m hatchback both stop at the right distance.
- **People vs traffic** — brake against `people` (rebuilt each frame by `refreshPeople()`),
  never `peds[]` alone: the cinema queue, dog walkers and performers are people too.
  Braking only covers what is ahead, so `pushPeopleOutOfVehicles()` is the backstop for
  someone walking into a flank and for vehicles running their own controllers, which
  skip the braking checks entirely.
- **Airport ground** — every flat airport surface takes a layer from the `Y` table plus a
  `polygonOffset`; they used to share a 16mm band across a 300m site, and the airport
  grass sat *below* the world ground plane, so the whole place shimmered.
- **Airport layout** — gate spacing must be `half-span(left) + half-span(right) + clearance`
  or parked wings intersect. Service routes stay aft of `AP.noseX + longest fuselage` and
  inboard of `AP.taxiX`. Never replace a vehicle's `userData` — `Object.assign` into it,
  or the route wipes its wheels, beacons and footprint.
- **Sky** — clouds are painted into the sky-dome shader, not hung on their own geometry:
  a separate cloud mesh shows its rim as a silhouette and fights the star layer for depth.
  The dome and starfield ride with the camera every frame — anchored at the origin, the
  far side of the 440-unit dome falls outside the 500-unit far plane as soon as you leave
  the middle of the map, and the clipped cap renders as a black dome over the city.

### Global Configuration

```javascript
const GRID = {
    cellSize: 24,      // Size of each city block
    roadWidth: 8,      // Width of roads
    sidewalkWidth: 2,  // Width of sidewalks
    gridCount: 4       // 4x4 blocks
};

const CFG = { cars: 25, emergencyVehicles: 3, peds: 50, bikes: 4 };
```

### Key Global Variables

- `scene`, `cam`, `renderer`, `clock` - Three.js core objects
- `buildings[]`, `cars[]`, `peds[]`, `tlights[]` - Entity arrays
- `weatherState` - Current weather: 'sunny', 'cloudy', 'rain', 'storm'
- `specialEvent` - Current active random event
- `omnibus`, `omnibusStops[]` - Bus line system

### Main Loop

The `animate()` function (line 4012) runs the game loop:
1. Handle camera movement from keyboard input
2. Call all update functions in sequence
3. Render the scene

## Pedestrian State Machine

Pedestrians (`peds`) use a state-based behavior system:
- `walking` - Moving along sidewalks
- `crossing` - Crossing street at crosswalk
- `waitToCross` - Waiting for safe crossing
- `enteringBuilding` / `insideBuilding` / `exitingBuilding` - Building interaction
- `toBusStop` / `waitingForBus` / `onBus` - Omnibus passenger behavior

## Traffic System

- Cars check traffic lights, pedestrians, other vehicles, and obstacles
- Emergency vehicles can ignore red lights but stop for pedestrians
- Vehicles attempt lane changes to avoid obstacles
- Traffic lights cycle on 10-second phases

## Special Events

Random events trigger periodically (see `triggerRandomEvent()`):
- `parade` - Floats, clown car, marching band
- `semiTruck` - Wide load convoy
- `iceCreamTruck` - Attracts pedestrians
- `dogWalker` - Person walking dogs
- `streaker` - Police chase
- `weddingCortege` - Wedding procession
- `brokenDownCar` - Blocks traffic

Standalone systems:
- Garbage truck with "suction" mechanic
- Falling person event with ambulance response

## Weather System

Weather changes automatically or via 'R' key:
1. **Sunny** - Clear skies, bright lighting
2. **Cloudy** - Overcast, light wind
3. **Rain** - Particle system (6000 drops)
4. **Storm** - Heavy rain, lightning flashes, flying debris

## Controls

| Key | Action |
|-----|--------|
| WASD / Arrows | Move |
| Q / E | Up / Down |
| Mouse | Look around |
| Scroll | Zoom (adjust FOV) |
| Space | Speed boost |
| R | Cycle weather |
| Click | Pointer lock |

## Development Guidelines

### Adding New Vehicle Types

1. Create a `mk[VehicleType]()` function that returns a THREE.Group
2. Add vehicle-specific userData properties (speed, type, etc.)
3. Call `placeCarOnRoad()` to position it
4. Push to `cars[]` array and add to scene
5. Handle special behavior in `updCars()` if needed

### Adding New Events

1. Create `create[EventName]()` function to spawn entities
2. Create `mk[EntityType]()` for event-specific objects
3. Add case to `triggerRandomEvent()` switch
4. Handle updates in `updateEvent()` if needed
5. Clean up in `endEvent()`

### Adding New Pedestrian Behaviors

1. Add new state string to the state machine
2. Handle state transitions in `setNewPedTarget()`
3. Add state-specific behavior in `updPeds()`

## Code Conventions

- Function names use camelCase with prefixes: `mk` (make), `upd` (update)
- Entity groups store metadata in `userData` property
- Colors are hex integers (e.g., `0xff3333`)
- Positions use Three.js Vector3 coordinates
- The $ helper function is shorthand for `getElementById`

## Performance Considerations

- Shadow maps: 2048x2048 resolution
- Fog: starts at 80 units, full at 350 units
- Rain particles: 6000 in rain, more in storm
- Window toggle rate: throttled to avoid excessive updates
- All entities share common materials where possible

## Dependencies

- Three.js v0.160.0 (loaded from CDN via import map)
- No build tools or package manager required

## Testing

Open `metropolis-3d-city.html` directly in a modern browser. No server required for basic testing (though some browsers may require a local server for ES modules).

```bash
# Quick start
open metropolis-3d-city.html

# Or with a local server
python -m http.server 8000
# Then visit http://localhost:8000/metropolis-3d-city.html
```

## Common Modification Points

| Goal | Location |
|------|----------|
| Change city size | `GRID.gridCount` |
| Add more vehicles | `CFG.cars` |
| New car colors | `cols` array in `mkCars()` |
| Billboard messages | `brands` array in `mkBillboards()` |
| Building heights | `types` array in `mkBuildings()` |
| Weather timing | `nextWeatherChange` calculation |
| Event frequency | `eventCooldown` and random checks |
