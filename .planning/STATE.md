# Project State: Metropolis

## Project Reference

See: .planning/PROJECT.md (updated 2026-01-25)

**Core value:** The city feels alive and worth watching
**Current focus:** v2.0 - Las Vegas Expansion

## Current Position

- **Milestone:** v2.0 - Las Vegas Expansion
- **Phase:** 2 of 6 (Iconic Landmarks - In Progress)
- **Plan:** 4 of 13 completed
- **Status:** Phase 2 in progress, Plan 02 complete
- **Last activity:** 2026-01-25 - Completed v2-02-02-PLAN.md (Bellagio and Caesars Palace)

**Progress:** ████░░░░░░░░░░░░ 31% (4/13 plans across all phases)

## Recent Progress

### v2.0 In Progress
- v2-02-02: Bellagio with fountain lake and Caesars Palace landmarks
- mkBellagio() with curved 3-section facade, tower, and 35x20 fountain lake
- Cream/beige Italianate styling, lake with transparent water and white border
- bellagioFountainLake global reference for Phase 4 fountain show
- mkCaesarsPalace() with 8 Roman columns, capitals/bases, triangular pediment
- Gold dome on roof, 3-step grand staircase, white marble finish
- 4 landmarks now in vegasLandmarks[] (Luxor, Paris, Bellagio, Caesars)
- v2-02-01: Luxor Pyramid and Paris Eiffel Tower landmarks positioned on Strip parking lots
- mkLuxorPyramid() with black glass pyramid (30 units), sandstone base, sphinx hint
- mkParisEiffelTower() with 4 angled legs, 2 observation decks, tapered spire (38 units)
- vegasLandmarks[] array initialized for Phase 3 lighting system
- Pyramid on west side near south end, Tower on east side in middle of Strip
- v2-01-02: The Strip road with sidewalks, independent Vegas sunny weather, temperature billboard (PHASE COMPLETE)
- The Strip (12 units wide, 70 units long) positioned at highway end, running north-south
- Double yellow center line, white edge lines, wide sidewalks (4 units) with curbs
- Sandy parking lot areas (30 units wide) beside sidewalks for future casinos
- Vegas weather isolation: stays sunny regardless of Metropolis weather state
- Rain particles constrained to Metropolis using position checks in updRain()
- Location-aware HUD displays Vegas sunny weather with hot temperature (95-115°F)
- Temperature billboard with canvas display, LED border animation, updates every 30 seconds
- v2-01-01: Route 66 highway with iconic marker sign connecting Metropolis to Vegas
- Highway extends 60 units east from Metropolis edge (X=48 to X=108)
- Desert terrain (0xc2956e sandy color) distinguishes Vegas zone from city grass
- Route 66 shield-style sign positioned at highway start with canvas texture
- VEGAS_CFG configuration provides zone dimensions for future phases
- v2.0 milestone initialized: Las Vegas expansion with 6 phases, 24 requirements
- Route 66 highway, 5 iconic landmarks, Vegas lights, entertainment, tourists, vehicles

### v1.0 Complete
- 05-02: Rooftop parties with string lights and animated figures (PHASE COMPLETE)
- Parties spawn every 60 seconds with 40% chance (max 2 simultaneous)
- Twinkling string lights in perimeter pattern with 12 lights per party
- 4-8 party figures wandering subtly within party area
- Static figures on gardens (1-3) and pools (1-2) with gentle animation
- 05-01: Static rooftop features (gardens and pools) with activeRooftops tracking
- Rooftop gardens with grass patch, 2-4 planters, 1-3 shrubs on ~20% tall buildings
- Rooftop pools with water surface, white rim, 2 loungers on ~10% remaining buildings
- activeRooftops[] array tracks buildings with features for Plan 02 figure placement
- 04-02: Pedestrian subway interaction with station activity indicators (PHASE COMPLETE)
- Pedestrians within 30 units of stations have 8% chance to walk toward entrance
- Pedestrians disappear when entering, reappear at different station after 8-20 seconds
- Station activity lights glow green when pedestrians entering/exiting or train stopped
- Cross-system protection prevents bus/garbage interruption of subway passengers
- 04-01: Subway infrastructure with 3 stations, elevated track, moving train
- Station entrances at ground level with covered stairway and platform
- Elevated track with support columns connecting L-shaped route
- Train moves between stations with 5-second stops
- 03-02: Pedestrian crowd behavior and performer interaction (PHASE COMPLETE)
- Pedestrians detect nearby performers and walk to semicircle watching positions
- 15% attraction chance creates organic crowd growth over time
- Watching state with 10-30 second duration before resuming walking
- Cross-system protection prevents bus/garbage interruption of crowds
- 03-01: Street performer entities with musician and statue types
- Musicians play guitar with strumming animation, statues pose with metallic finish
- Performers spawn on sidewalks facing roads at 45-second intervals
- Performance duration 60-120 seconds with automatic cleanup
- Maximum 3 simultaneous performers, 20-unit minimum spacing
- 02-02: Bird landing and scattering behavior with pedestrian proximity detection (PHASE COMPLETE)
- Birds periodically land on rooftops (70%) and sidewalks (30%)
- Pedestrians within 3 units cause birds to scatter and take flight
- State machine: flying, landing, landed, takeoff with distinct animations
- Landing duration 5-15 seconds with natural timing
- 02-01: Bird flock system with boids algorithm (separation, cohesion, alignment)
- 4 autonomous flocks of varying sizes (3-8 birds) flying through city
- Wing flapping animation with sine wave motion
- Waypoint navigation system for flocks to traverse city airspace
- 01-03: Streetlights, car headlights, and window lighting activate at night
- Streetlight poles along roads emit warm light at night (intensity 1.5)
- Car headlights brighten from dim to yellow at night
- Building windows shift from 20% lit (day) to 70% lit (night)
- Bulk window updates during day/night transitions for immediate impact
- 01-02: Sun and moon celestial bodies tracking across sky with time control
- Visible sun during day (0.2-0.8) and moon during night (0.8-0.2)
- Celestial bodies arc from east to west with realistic orbital motion
- Directional light follows sun position for dynamic shadows
- T key cycles time speed: normal, 10x fast, paused
- 01-01: Core time system with sky transitions and dynamic lighting implemented
- Time-of-day variable advances continuously (0-1 cycle)
- Sky colors transition through 5 phases (midnight, dawn, day, dusk, night)
- Lighting adjusts dynamically based on time of day

## Session Notes

### 2026-01-25 - Phase v2-02 Plan 02 (Bellagio and Caesars Palace)
- Created mkBellagio() with 3-section curved facade (center + two angled wings)
- Cream/beige color (0xf5f0e6) with darker accent band (0xc4a777) at roof level
- Tower section (8x35x10) behind main building for hotel tower silhouette
- Fountain lake (35x20) with transparent blue water material (0x4fc3f7, opacity 0.8)
- Lake border with white rim around perimeter
- bellagioFountainLake global reference stored for Phase 4 fountain animation
- Positioned west of Strip at 0.65 Strip length (north-middle area)
- Created mkCaesarsPalace() with white marble appearance (0xf8f8f0)
- 8 Roman columns (radius 0.5, height 10) with capitals and bases
- Entrance portico with triangular pediment (BufferGeometry triangle)
- Gold dome (SphereGeometry half-sphere, 0xd4af37, metalness 0.7) on roof center
- 3-step grand staircase leading to entrance
- Positioned east of Strip at 0.3 Strip length (south-middle area)
- Both landmarks rotated to face Strip (columns/fountain visible from road)
- vegasLandmarks array now has 4 entries for Phase 3 lighting
- 3 tasks completed, 1 commit: 3a26c4f
- Execution time: 2 minutes 13 seconds

### 2026-01-25 - Phase v2-02 Plan 01 (Luxor Pyramid and Paris Eiffel Tower)
- Created mkLuxorPyramid() with ConeGeometry (4 radial segments = true pyramid)
- Black glass material (0x1a1a1a, metalness 0.9, roughness 0.1) for reflective look
- Pyramid height 30 units, base width 25 units, rotated 45 degrees for cardinal alignment
- Sandstone base platform (27 units square, 0xc4a777 color) matching desert theme
- Sphinx hint using two boxes (body 3x1.5x2, head 1x1.2x1) in sandstone color
- Positioned west of Strip: centerX - stripWidth/2 - sidewalkWidth - 15
- Created mkParisEiffelTower() with iron-colored (0x4a4a4a) components
- Four angled legs converging inward over 12-unit base section
- First observation deck at 13 units height, second at 25 units
- Middle tapered section (12 units), spire (10 units), antenna (3 units)
- Total height approximately 38 units (taller than pyramid for variety)
- Positioned east of Strip: centerX + stripWidth/2 + sidewalkWidth + 12
- Added vegasLandmarks[] global array with comment for Phase 3 lighting
- Both landmarks pushed to array with userData (type, hasBeam/hasLights flags)
- Both functions called in init() after mkTemperatureBillboard()
- 3 tasks completed, 1 commit: 27dc086
- Execution time: 2 minutes 7 seconds

### 2026-01-25 - Phase v2-01 Plan 02 (Vegas Strip Infrastructure - PHASE COMPLETE)
- Created mkTheStrip() with 12-unit wide road at end of highway (X=108)
- Strip runs north-south (along Z axis) with 70-unit length
- Double yellow center line (two 0.15-unit strips at ±0.2 offset) indicates no passing
- White edge lines at road boundaries, 4-unit wide sidewalks on both sides
- Gray curbs (0.3x0.15 units) separate road from sidewalks
- Sandy parking lot areas (30 units wide, 0xd4c4a8 color) beside sidewalks
- T-intersection connects highway to Strip cleanly
- Added vegasWeatherState variable (always 'sunny')
- Created isInVegasZone() helper checking if X > 58 (10-unit buffer)
- Modified updRain() to constrain rain particles to Metropolis (X within -48 to +48)
- Updated updateWeatherUI() to show location-aware weather display
- Vegas shows "☀️ Sunny [temp]°F" with randomized hot temperature
- Metropolis shows variable weather (sunny/cloudy/rain/storm)
- Created mkTemperatureBillboard() with Vegas-style LED display
- Two support poles (8 units tall), dark backing (6x3 units)
- Canvas display (512x256) shows TEMPERATURE, temp value (95-115°F), LAS VEGAS
- Temperature updates every 30 seconds with ±2°F fluctuation
- 20 LED border lights with animated chase pattern (sine wave phase)
- Billboard positioned at Strip entrance (east side, near south end)
- 3 tasks completed, 3 commits: a208558, 2677a49, 85e42dc
- Execution time: 3 minutes 13 seconds
- Phase v2-01 complete - Vegas infrastructure ready for landmark construction

### 2026-01-25 - Phase v2-01 Plan 01 (Vegas Infrastructure Foundation)
- Created VEGAS_CFG constant with zone dimensions (100x80 units, zone starts at X=68)
- Implemented mkVegasZoneGround() extending desert terrain east of Metropolis
- Built mkVegasHighway() with dark asphalt, dashed center line, solid edge lines
- Highway 10 units wide (wider than city roads at 8 units) for open feel
- Desert strips (25 units wide) flank highway on both sides
- Created mkRoute66Sign() with canvas-generated shield texture
- Sign shows "ROUTE 66 US" text in classic styling, double-sided visibility
- Positioned at highway start (X=53, Z=-8), offset from road to not obstruct
- All functions integrated into init sequence after mkCityLayout()
- 3 tasks completed, 3 commits: 7229cdb, 80a10d6, e5442a5
- Execution time: 3 minutes 3 seconds
- Plan 01 complete - Vegas infrastructure foundation established

### 2026-01-25 - v2.0 Milestone Initialization
- Initialized Las Vegas expansion milestone
- 5 landmarks selected: Luxor Pyramid, Bellagio + Fountains, Paris Eiffel Tower, Caesars Palace, Excalibur Castle
- 4 activities: Tourists + Photos, Wedding Chapels, Elvis Impersonators, Bellagio Fountain Show
- 2 vehicle types: Exotic Cars, Open-top Tourist Buses
- Special features: Route 66 highway marker, Vegas always sunny, temperature billboard, lights only at night
- Created REQUIREMENTS-v2.md with 24 requirements across 6 categories
- Created ROADMAP-v2.md with 6 phases, 13 plans total
- Updated PROJECT.md for v2.0 scope

### 2026-01-24 - Phase 05 Plan 02 (PHASE COMPLETE, MILESTONE COMPLETE)
- Created ROOFTOP_CFG with partySpawnInterval (60), partySpawnChance (0.4), partyDuration [90, 180]
- Implemented mkRooftopFigure() with colorful body/head and wandering animation userData
- Built mkRooftopParty() with 12 twinkling string lights and 4-8 party figures
- Created spawnRooftopParty() selecting from activeRooftops or tall buildings (h > 30)
- Added updRooftopParties() for spawn timer, light twinkling, figure wandering, despawn
- Added updRooftopFigures() for static garden/pool figure animation
- Integrated static figure placement into mkBuildings() for rooftop features
- Phase 05 complete - all v1.0 visual engagement features implemented

### 2026-01-24 - Phase 05 Plan 01
- Created mkRooftopGarden() with grass patch (0x4a7c4e), 2-4 planters (0x8b4513), 1-3 shrubs (0x2d5a2d)
- Created mkRooftopPool() with water surface (0x4fc3f7, 80% opacity), white rim (0xdddddd), 2 loungers (0xeeeeee)
- Integrated into mkBuilding() with probability checks: 20% gardens (h > 25), 10% pools (h > 20)
- Added activeRooftops[] global array tracking buildings with features
- Each entry stores: building reference, position, dimensions, feature type
- Plan 01 complete - static rooftop features ready for Plan 02 animated figures

### 2026-01-24 - Phase 04 Plan 02 (PHASE COMPLETE)
- Added subwayPassengers array and SUBWAY_MAX_PASSENGERS (12) constant
- Implemented 8% subway attraction chance in setNewPedTarget() for nearby stations
- Added toSubwayStation state: pedestrians walk to station entrance
- Added inSubway state: pedestrians invisible for 8-20 seconds, exit at different station
- Station activity lights glow green when pedestrians using station or train stopped
- Protected subway pedestrians from bus assignment and garbage truck suction
- Phase 04 complete - subway system fully operational with passenger flow

### 2026-01-24 - Phase 04 Plan 01
- Created SUBWAY_CFG with trackHeight (6), trainSpeed (0.12), stopDuration (5)
- Implemented mkSubwayStation() with ground entrance, stairs, elevated platform, shelter
- Created mkSubwayTrack() with beam, rails, guard rails, support columns
- Built mkSubwayTrain() with silver body, windows, AC units, wheels
- Established L-shaped route with 3 stations (North, Central, East)
- Train state machine: moving, stopping with automatic loop
- updSubway(t) added to animate loop for continuous operation

### 2026-01-24 - Phase 03 Plan 02 (PHASE COMPLETE)
- Implemented pedestrian performer attraction with 15% notice chance
- Added towardPerformer and watchingPerformer states to pedestrian state machine
- Calculated semicircle positions around performer (144-degree arc, 3-unit radius)
- Watch duration randomized 10-30 seconds with elapsed time tracking
- Pedestrians face performer continuously while watching
- Performer despawn releases all watchers back to walking state
- Protected watching pedestrians from bus assignment and garbage truck suction
- Phase 03 complete - street performers now draw realistic crowds

### 2026-01-24 - Phase 03 Plan 01
- Implemented street performer system with two performer types
- Created mkMusician() with acoustic guitar, dark red outfit, beret
- Created mkStatue() with silver metallic finish, top hat, dramatic pose
- Performers spawn on random sidewalks facing toward roads
- Spawn interval 45 seconds with 50% chance, max 3 performers
- Performance duration randomized 60-120 seconds per performer
- Musicians animate strumming with sine wave arm movement
- Statues have subtle occasional head movements (living statue effect)
- Minimum 20-unit spacing between performers enforced

### 2026-01-24 - Phase 02 Plan 02 (PHASE COMPLETE)
- Implemented bird landing system with rooftop and sidewalk perch selection
- Added findPerchSpot() helper to calculate valid landing locations
- Created checkPedestrianProximity() for cross-system bird-pedestrian interaction
- Built four-state bird behavior machine (flying, landing, landed, takeoff)
- Landing chance 0.002 per frame provides occasional natural landing
- Scatter distance 3 units balances realism with observation
- Phase 02 complete - birds now interact dynamically with city environment

### 2026-01-24 - Phase 02 Plan 01
- Implemented complete boids flocking algorithm with separation, cohesion, alignment
- Created 4 bird flocks with varying sizes [3, 5, 6, 8] for visual diversity
- Added wing flapping animation using sine wave on wingPhase
- Waypoint navigation allows flocks to autonomously traverse city
- Birds stay within height bounds 15-60 units for optimal visibility
- Turn speed 0.03 creates smooth, organic movement

### 2026-01-24 - Phase 01 Plan 03 (PHASE COMPLETE)
- Created streetlight poles along all roads at 16-unit intervals
- Implemented updStreetlights() for smooth intensity transitions
- Streetlights emit warm yellow light at night with PointLights
- Car headlights tracked in userData.headlights, brighten at night
- Window lighting uses probability (70% night, 20% day)
- Bulk window updates during day/night transitions
- Phase 01 complete - full day/night cycle with all planned effects

### 2026-01-24 - Phase 01 Plan 02
- Created sun and moon celestial body meshes with visual detail
- Sun has glow halo effect, moon has crater detail spots
- Positioned celestial bodies in updDayNight based on timeOfDay
- Directional light tracks sun position for realistic shadow movement
- Added T key time speed control (normal/fast/paused)

### 2026-01-24 - Phase 01 Plan 01
- Implemented core time-of-day system
- Sky color transitions through 5 phases with smooth interpolation
- Dynamic lighting adjustments via sine wave intensity curves
- Fixed weather system to respect day/night cycle when sunny

### 2025-01-23 - Initialization
- Created PROJECT.md with 5 visual engagement features
- Defined requirements for day/night cycle, birds, performers, subway, rooftops
- Created roadmap mapping all requirements to phases

## Open Issues

None currently.

## Key Decisions Log

| Date | Decision | Context |
|------|----------|---------|
| 2026-01-25 | Bellagio curved facade with 3 angled sections | Simpler than actual curve geometry, angled wings suggest curved facade |
| 2026-01-25 | Caesars columns with capitals and bases | Classical authenticity without excessive geometry |
| 2026-01-25 | Triangular pediment on Caesars entrance | Greek/Roman temple aesthetic, recognizable classical element |
| 2026-01-25 | Gold dome on Caesars roof | Vegas signature element, adds visual variety to white building |
| 2026-01-25 | Bellagio at 0.65 Strip length, Caesars at 0.3 | Good spacing between landmarks on opposite sides of Strip |
| 2026-01-25 | bellagioFountainLake global reference | Phase 4 can access fountain directly for animation |
| 2026-01-25 | ConeGeometry with 4 radial segments for pyramid | Creates true pyramid with 4 triangular faces, not a rounded cone |
| 2026-01-25 | Pyramid rotated 45 degrees | Faces align with cardinal directions for natural viewing angles |
| 2026-01-25 | Simplified Eiffel with 4 angled legs | Recognizable silhouette without complex lattice geometry |
| 2026-01-25 | vegasLandmarks[] array for lighting integration | Phase 3 can iterate landmarks without scene graph search |
| 2026-01-25 | Strip perpendicular to highway (north-south) | Creates natural T-intersection, maximizes casino frontage on both sides |
| 2026-01-25 | Double yellow center line on Strip | Indicates no-passing zone, matches real Vegas Strip traffic rules |
| 2026-01-25 | Wide sidewalks (4 units vs city 2 units) | Vegas Strip has very wide sidewalks for tourist crowds |
| 2026-01-25 | Weather zone isolation via position checks | Cleanest implementation, Vegas stays sunny regardless of Metropolis weather |
| 2026-01-25 | Location-aware HUD weather display | User sees accurate local weather, more immersive experience |
| 2026-01-25 | Temperature billboard updates every 30 seconds | Frequent enough to feel dynamic, slow enough to be observable |
| 2026-01-25 | LED chase pattern with sine wave | Classic Vegas billboard aesthetic, visually engaging |
| 2026-01-25 | Vegas zone east of Metropolis (positive X) | Simplifies navigation, clear directional separation (city west, Vegas east) |
| 2026-01-25 | Highway width 10 units (vs city roads 8 units) | Highway should feel wider and more open than city streets |
| 2026-01-25 | Separate mkVegasZoneGround() function | Cleaner separation, Vegas zone extensible without touching core city code |
| 2026-01-25 | Canvas texture for Route 66 sign | No external dependencies, fully customizable, self-contained |
| 2026-01-25 | Sign positioned at X=halfSize+5, Z=-8 | Close to highway start for discovery, offset to not obstruct road |
| 2026-01-24 | Parties spawn every 60 seconds with 40% chance | Occasional but not constant, feels like city life |
| 2026-01-24 | Max 2 simultaneous parties | Prevents performance impact, maintains specialness |
| 2026-01-24 | Party duration 90-180 seconds | Long enough to observe, short enough for variety |
| 2026-01-24 | 12 string lights per party | Visible perimeter without overdoing it |
| 2026-01-24 | 4-8 party figures, 1-3 garden figures, 1-2 pool figures | Balanced density |
| 2026-01-24 | Figure 5-color palette (coral, teal, yellow, mint, pink) | Colorful and distinguishable from above |
| 2026-01-24 | Gardens on 20% of tall buildings (h > 25) | Visual variety without overcrowding, tall buildings more likely to have amenities |
| 2026-01-24 | Pools on 10% of remaining buildings (h > 20) | Rarer premium feature, excluded from buildings with gardens |
| 2026-01-24 | activeRooftops[] tracks building, position, dimensions, type | Enables Plan 02 figure placement with full context |
| 2026-01-24 | Subway attraction chance 8% | Balances against bus (10%), performers (15%), buildings (10%) |
| 2026-01-24 | Subway attraction radius 30 units | Matches performer attraction radius for consistency |
| 2026-01-24 | Subway ride duration 8-20 seconds | Observable transit time, not too long to feel stuck |
| 2026-01-24 | Max 12 subway passengers | Prevents draining pedestrian population |
| 2026-01-24 | Station activity lights green | Consistent with active/go signaling |
| 2026-01-24 | Track height 6 units above ground | Visible elevated transit above street traffic, connected to city |
| 2026-01-24 | Train speed 0.12, stop duration 5 seconds | Observable travel between stations, noticeable pauses |
| 2026-01-24 | L-shaped route with 3 stations | Covers two city edges, extensible to full loop |
| 2026-01-24 | Station positioning 12 units from edge | Accessible while avoiding building collisions |
| 2026-01-24 | Pedestrian attraction chance 15% | Gradual organic crowd growth, ~7-8 notices per target cycle, prevents sudden mobs |
| 2026-01-24 | Semicircle crowd formation 144 degrees | Real crowds form arcs not circles, leaves performer "stage" clear, 0.8π spread |
| 2026-01-24 | Watch duration 10-30 seconds | Visible crowd formation (10s min), dynamic turnover (30s max), staggered departures |
| 2026-01-24 | Protect watchers from bus/garbage | Stable crowds during performances, prevents visual glitches, cross-system coordination |
| 2026-01-24 | Performer types: musician and statue | Musician with guitar (animated), statue with metallic finish (still), both common street performers |
| 2026-01-24 | Performer spawn interval 45 seconds, 50% chance | Average 22.5s spawn rate, maintains 1-3 performers typically, feels occasional not constant |
| 2026-01-24 | Performer duration 60-120 seconds | Long enough to discover, short enough to stay fresh, matches simplified set length |
| 2026-01-24 | Max 3 simultaneous performers | Prevents overcrowding, maintains specialness, low performance impact |
| 2026-01-24 | Performers face toward road | Real performers face traffic for visibility, creates natural stage area for future crowds |
| 2026-01-24 | Bird landing chance 0.002 per frame | Occasional landing without overwhelming flocks, creates natural variety |
| 2026-01-24 | Bird scatter distance 3 units | Pedestrian proximity causes scatter, balances realism with visibility |
| 2026-01-24 | Rooftop landing preference 70% | Creates visual variety while keeping some birds visible on ground |
| 2026-01-24 | Bird land duration 5-15 seconds | Natural perching without birds staying static too long |
| 2026-01-24 | Bird separation weight 1.5 (highest) | Prevents collisions between birds, strongest boids force for safety |
| 2026-01-24 | 4 flocks with sizes [3, 5, 6, 8] | Visual variety without performance impact (~22 total birds) |
| 2026-01-24 | Bird height bounds 15-60 units | Visible above buildings but not too high, optimal viewing range |
| 2026-01-24 | Bird turn speed 0.03 | Smooth organic turns rather than sharp jerky movement |
| 2026-01-24 | Window night probability 70%, day 20% | Creates clear day/night distinction, represents realistic building occupancy |
| 2026-01-24 | Car headlights material color only, no PointLights | Visual effect without performance overhead for 25+ vehicles |
| 2026-01-24 | Streetlight intensity 1.5 at night | Strong road illumination, warm inviting atmosphere |
| 2026-01-24 | Streetlights every 16 units, skip intersections | Consistent illumination without clutter, avoids traffic light conflicts |
| 2026-01-24 | Time speed control: normal -> fast -> paused | Normal (0.005) for observation, fast (0.05) for testing, paused for screenshots |
| 2026-01-24 | Directional light synced to sun position | Realistic shadow movement throughout day enhances time perception |
| 2026-01-24 | Sun orbit radius 150, peak height 120 | Large enough to be visible from anywhere in city, high enough to clear buildings |
| 2026-01-24 | Sun visible 0.2-0.8, moon visible 0.8-0.2 | Corresponds to dawn-dusk and night periods, wrapping handles midnight |
| 2026-01-24 | Time starts at 0.25 (dawn) | Visually interesting orange/pink sky at startup |
| 2026-01-24 | Full day/night cycle in ~200 seconds | Allows observation of full cycle in 3-4 minutes |
| 2026-01-24 | Sine wave for lighting intensity | Natural smooth transition peaking at noon |
| 2026-01-24 | Weather overrides sky only when not sunny | Preserves day/night visibility in normal conditions |
| 2025-01-23 | 5 features chosen for visual variety | Day/night, birds, performers, subway, rooftops |
| 2025-01-23 | Audio out of scope | Focus on visual observation |

## Session Continuity

- **Last session:** 2026-01-25
- **Stopped at:** Completed v2-02-02-PLAN.md (Bellagio and Caesars Palace)
- **Resume file:** None
- **Next:** v2-02-03-PLAN.md (Excalibur Castle) or Phase 3 (Night Lighting)

---
*Last updated: 2026-01-25*
