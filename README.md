# metropolis
metropolis
# 🌆 METROPOLIS - 3D City Simulation

## What It Is
A fully interactive 3D city simulation built in a single HTML file using Three.js. Fly through a living, breathing miniature city and watch the urban life unfold below.

## Core Features

### 🏙️ The City
- **4×4 block grid** with realistic roads, sidewalks, and crosswalks
- **Dynamic buildings** (1-2 per block) with lit windows that flicker on/off
- **Animated billboards** on rooftops with chasing lights
- **Traffic light system** with proper 4-way signaling

### 🚗 Vehicles
- **Regular cars** that obey traffic laws, stop for pedestrians and red lights
- **Double-decker tourist buses** with "HOP ON HOP OFF" signs and visible passengers
- **Jitney minibuses** in colorful route liveries
- **Vintage omnibus** running a fixed route with 4 stops - passengers board and alight!
- **Emergency vehicles** (police, fire, ambulance) with flashing lights that weave through traffic
- **Bicycles** that ignore red lights and get chased by police

### 🚶 Pedestrians
- **50 citizens** walking on sidewalks, entering/exiting buildings through doors
- Cross streets at crosswalks (walk faster when crossing!)
- Wait at bus stops and ride the omnibus
- React to vehicles - stop when cars are near

### 🎭 Random Events
- **🚛 Garbage Truck** - Giant truck with suction nozzle that "collects" pedestrians
- **😱 Falling Person** - Window flashes red, person falls, ambulance responds
- **🎪 Parade** - Floats, clown car, marching band, balloon seller
- **🚚 Semi Truck** - "WIDE LOAD" convoy with escort vehicles
- **🍦 Ice Cream Truck** - Plays music, attracts kids
- **💒 Wedding Cortege** - White limo with decorated cars
- **🏃 Streaker** - Runs through city, police give chase
- **🔧 Broken Down Car** - Steaming car blocks traffic, hazard triangles out

### 🌦️ Dynamic Weather
- **☀️ Sunny** - Clear blue skies (most common)
- **☁️ Cloudy** - Overcast, light wind
- **🌧️ Rain** - 6,000 rain particles affected by wind
- **⛈️ Storm** - Heavy rain, lightning flashes, flying debris (newspapers, leaves, plastic bags tumbling through the air!)

### 🔍 Hidden Secrets
- **🛸 UFO** flying in a figure-8 pattern
- **🎈 Hot Air Balloon** drifting peacefully
- **🚁 Helicopter** with spinning rotors

### 🎮 Controls
- **WASD/Arrows** - Move
- **Mouse** - Look around
- **Q/E** - Up/Down
- **Space** - Speed boost
- **Scroll** - Zoom
- **R** - Cycle weather

---

## Why It's Fun to Expand

### 1. **Single-File Simplicity**
Everything lives in one HTML file. No build tools, no dependencies to install - just open and go. Add a feature, refresh, see it immediately.

### 2. **Modular Architecture**
Each system is self-contained:
- `mkCars()`, `updCars()` - Vehicle system
- `mkPeds()`, `updPeds()` - Pedestrian system
- `updWeather()` - Weather system
- `updSpecialEvents()` - Random events

Adding a new vehicle type? Copy an existing one and tweak. New event? Add it to the events array.

### 3. **Easy Extension Ideas**

**Quick Wins (30 min):**
- New car colors/types
- More billboard messages
- Additional pedestrian behaviors
- New weather effects (snow, fog)

**Medium Projects (1-2 hours):**
- Subway system with underground stations
- Day/night cycle with streetlights
- Taxi system that picks up pedestrians
- Construction sites with cranes

**Ambitious Features:**
- Multiple city districts with different architecture
- Economy system (shops, offices, homes)
- Traffic accidents with emergency response
- Seasonal changes
- Sound effects and ambient audio

### 4. **Learning Playground**
Great for learning:
- **Three.js** basics (meshes, materials, lighting)
- **Game loops** and state management
- **Collision detection** algorithms
- **Finite state machines** (pedestrian states, vehicle behaviors)
- **Particle systems** (rain, debris)

### 5. **Satisfying to Watch**
There's something mesmerizing about watching a tiny city operate. The emergent behavior from simple rules creates endless entertainment - a police chase here, a parade there, a storm rolling in while the omnibus makes its rounds.

---

## Get Started
```bash
# Clone and open
git clone https://github.com/aifunmobi/metropolis.git
open metropolis-3d-city.html
```

Or just download the HTML file and double-click it. That's it. Welcome to Metropolis! 🌆
