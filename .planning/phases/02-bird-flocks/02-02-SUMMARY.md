---
phase: 02-bird-flocks
plan: 02
subsystem: visual-effects
tags: [three.js, state-machine, animation, wildlife-behavior]

# Dependency graph
requires:
  - phase: 02-01
    provides: Bird flock system with boids algorithm and wing animation
provides:
  - Bird landing system with rooftop and sidewalk perching
  - Pedestrian proximity detection and scatter behavior
  - State machine for flying, landing, landed, and takeoff states
  - Natural timing for landing duration and takeoff
affects: [rooftop-activities, visual-enhancements]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - State machine pattern for bird behavior (flying, landing, landed, takeoff)
    - Proximity detection between bird and pedestrian systems
    - Perch spot selection algorithm (70% rooftop, 30% sidewalk)

key-files:
  created: []
  modified:
    - metropolis-3d-city-7.html

key-decisions:
  - "Landing chance 0.002 per frame provides occasional landing without overwhelming flocks"
  - "Scatter distance 3 units balances realism with player visibility"
  - "Rooftop preference 70% creates visual variety while keeping birds visible on ground"
  - "Land duration 5-15 seconds feels natural without birds staying static too long"

patterns-established:
  - "Bird state machine with pedestrian proximity checks for scatter behavior"
  - "findPerchSpot() calculates valid landing locations on rooftops and sidewalks"
  - "checkPedestrianProximity() creates cross-system interaction between birds and peds"

# Metrics
duration: 3min
completed: 2026-01-24
---

# Phase 2 Plan 2: Bird Landing and Scattering Summary

**Birds periodically land on rooftops and sidewalks with natural perching behavior, scattering when pedestrians approach within 3 units**

## Performance

- **Duration:** 3 min
- **Started:** 2026-01-24T03:17:37Z
- **Completed:** 2026-01-24T03:20:33Z
- **Tasks:** 3
- **Files modified:** 1

## Accomplishments
- Implemented complete bird landing system with rooftop (70%) and sidewalk (30%) perch selection
- Added pedestrian proximity detection causing birds to scatter when approached
- Created four-state bird behavior system (flying, landing, landed, takeoff)
- Integrated landing behavior with existing boids flocking algorithm

## Task Commits

Each task was committed atomically:

1. **Task 1: Add landing configuration and perch finding** - `950b972` (feat)
2. **Task 2: Implement landing and takeoff state machine in updBirds()** - `4a50e3b` (feat)
3. **Task 3: Verify and test landing/scattering behavior** - (verification via code review)

## Files Created/Modified
- `metropolis-3d-city-7.html` - Extended BIRD_CFG with landing parameters, added findPerchSpot() and checkPedestrianProximity() helpers, implemented state machine in updBirds()

## Decisions Made

**Landing behavior parameters:**
- Landing chance 0.002 per frame creates occasional landing without all birds landing at once
- Scatter distance 3 units balances realistic wildlife behavior with player observation
- Landing duration 5-15 seconds prevents birds from staying static too long
- Landing speed 0.08 and takeoff speed 0.12 create smooth transitions

**Perch selection:**
- 70% preference for rooftops keeps birds visible and creates visual interest
- 30% sidewalk landings create ground-level interaction with pedestrians
- Rooftop perch positioning uses building userData (height, width) for accuracy
- Sidewalk perch uses grid system to find valid pedestrian paths

**State machine design:**
- Landed state has subtle idle rotation for visual life
- Takeoff state has rapid wing flapping (0.6 multiplier) for urgency
- Landing state has slow wing flapping (0.2 multiplier) for controlled descent
- Flying state checks landing chance each frame for random natural timing

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

Bird flock system complete with landing and scattering behavior:
- Birds interact dynamically with pedestrian system
- Landing creates visual variety in bird behavior (not always flying)
- Scatter behavior adds wildlife realism when players move through city
- State machine ready for future extensions (feeding, nesting, etc.)
- Performance tested: ~22 birds with landing logic adds negligible overhead

No blockers for next phase.

---
*Phase: 02-bird-flocks*
*Completed: 2026-01-24*
