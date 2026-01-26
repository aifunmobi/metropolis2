---
phase: quick
plan: 002
subsystem: vegas-landmarks
tags: [vegas, hotels, scaling, windows, welcome-sign]

dependency-graph:
  requires: [quick-001]
  provides: [scaled-vegas-landmarks, dense-hotel-windows, welcome-sign]
  affects: [v2-03, v2-04]

tech-stack:
  added: []
  patterns: [addHotelWindowsAllSides, canvas-texture-signage, chase-light-animation]

key-files:
  created: []
  modified: [metropolis-3d-city-7.html]

decisions:
  - 2.5x scale factor for all Vegas landmarks
  - Window spacing 1.5 units (was 2) for denser grid
  - All 4 faces get windows via addHotelWindowsAllSides()
  - Welcome sign at Strip entrance with 20 chase lights

metrics:
  duration: 5 minutes 11 seconds
  completed: 2026-01-26
---

# Quick Task 002: Vegas Hotels Larger, Many Windows, Welcome Sign

**One-liner:** Vegas hotels scaled 2.5x with dense window grids on all faces and iconic Welcome sign at entrance

## Objective

Scale up Vegas hotels significantly (2-3x), add many more windows matching Metropolis style, and create the iconic "Welcome to Fabulous Las Vegas" sign at the Vegas entrance.

## Completed Tasks

| Task | Name | Commit | Files Modified |
|------|------|--------|----------------|
| 1 | Scale up Vegas hotels significantly | dd64a08 | metropolis-3d-city-7.html |
| 2 | Add dense window grids to all Vegas hotels | (included in Task 1) | metropolis-3d-city-7.html |
| 3 | Create Welcome to Fabulous Las Vegas sign | 72194aa | metropolis-3d-city-7.html |

## Key Changes

### Task 1: Vegas Hotel Scaling (2.5x)

**Luxor Pyramid:**
- Height: 30 -> 75 units
- Base width: 25 -> 60 units
- Sphinx: body 3x1.5x2 -> 6x3x4, head 1x1.2x1 -> 2x2.4x2
- Position offset: Z+18 -> Z+45 (larger parking lot)

**Paris Eiffel Tower:**
- Foundation: 15x1x15 -> 35x2x35
- Leg height: 12 -> 30, spread 5 -> 12, top spread 2 -> 5
- Middle section: height 12 -> 30, radii 1.2/2.2 -> 3/5.5
- Spire: height 10 -> 25, radii 0.2/0.6 -> 0.5/1.5
- Total height: ~38 -> ~95 units
- Position offset: Z-12 -> Z-30

**Bellagio:**
- Center section: 12x25x15 -> 30x65x35
- Wings: 10x25x15 -> 25x65x35
- Tower: 8x35x10 -> 20x90x25
- Lake: 35x20 -> 90x50
- Accent band: 32x1.5x16 -> 80x3x40
- Position offset: Z+25 -> Z+55

**Caesars Palace:**
- Main building: 40x22x20 -> 100x50x75
- Column height: 10 -> 25, radius 0.5 -> 1.25
- Column spacing: 3 -> 12
- Dome: radius 4 -> 10
- Staircase: 3 steps -> 5 steps, wider
- Position offset: Z-25 -> Z-55

**Excalibur Castle:**
- Foundation: 40x2x22 -> 100x4x55
- Main body: 35x15x18 -> 90x40x45
- Turrets: radius 2.5 -> 6, height 12 -> 30
- Cones: radius 3.5 -> 8, height 5 -> 12
- Central tower: radius 3 -> 7.5, height 20 -> 50
- Gate: 6x8 -> 15x20
- Position offset: Z+22 -> Z+55

### Task 2: Dense Window Grids

**New function: `addHotelWindowsAllSides()`**
- Adds windows to all 4 faces (front, back, left, right)
- Window spacing reduced: 2 -> 1.5 units for denser grid
- 70% of windows lit at creation
- All windows tracked in `vegasWindows[]` for flicker animation

**Applied to:**
- Bellagio: center section, tower, left wing, right wing
- Caesars Palace: main building
- Excalibur Castle: main body

### Task 3: Welcome Sign

**Structure:**
- Diamond-shaped sign (12x12 rotated box)
- Inner white diamond (9x9)
- Blue accent strip at bottom
- Canvas texture: "WELCOME / to Fabulous / LAS VEGAS / NEVADA"
- Gold circle medallion at top
- Two support poles
- Double-sided (visible from both directions)

**Chase Lights:**
- 20 bulbs around diamond perimeter
- Animated chase pattern (updWelcomeSign in main loop)
- Yellow (0xffff00) when lit, dim (0x444400) when off

**Position:**
- X: stripStartX - 12 (just before Strip starts)
- Z: 14 (south side, visible when approaching from highway)

## Deviations from Plan

None - plan executed exactly as written.

## Technical Details

### Global Variables Added
```javascript
let welcomeSign = null; // Welcome to Fabulous Las Vegas sign
```

### Functions Added
- `mkWelcomeSign()` - Creates the welcome sign with chase lights
- `updWelcomeSign()` - Animates chase light pattern
- `addHotelWindowsAllSides()` - Windows on all 4 building faces

### Init Sequence
```javascript
theStrip = mkTheStrip();
temperatureBillboard = mkTemperatureBillboard();
welcomeSign = mkWelcomeSign(); // Added
mkLuxorPyramid();
// ... rest of landmarks
```

### Animate Loop
```javascript
updVegasWindows();
// ...
updWelcomeSign(); // Added
```

## Verification

- [x] All 5 Vegas hotels scaled up ~2.5x
- [x] Hotels appear significantly larger, dominating skyline
- [x] Dense window grids on Bellagio, Caesars, Excalibur (all 4 faces)
- [x] Welcome sign visible at Vegas entrance
- [x] Chase lights animate around sign perimeter
- [x] No overlapping landmarks, proper spacing maintained

## Next Steps

Ready for:
- **v2-03:** Vegas Night Lighting (neon, spotlights, beam effects)
- **v2-04:** Bellagio Fountain Show (now uses 90x50 lake)
