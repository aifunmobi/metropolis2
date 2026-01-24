---
phase: 02-bird-flocks
plan: 01
subsystem: visual-effects
tags: [three.js, boids-algorithm, animation, flocking-behavior]

# Dependency graph
requires:
  - phase: 01-day-night-cycle
    provides: Day/night cycle, time system, and existing 3D city scene
provides:
  - Bird flock system with 4 flocks of varying sizes (3-8 birds each)
  - Boids flocking algorithm (separation, cohesion, alignment)
  - Wing flapping animation
  - Waypoint-based navigation system
affects: [rooftop-activities, visual-enhancements]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Boids algorithm for emergent group behavior
    - Entity userData pattern for bird state (velocity, wingPhase, state)
    - Flock objects containing bird arrays with shared navigation

key-files:
  created: []
  modified:
    - metropolis-3d-city-7.html

key-decisions:
  - "4 flocks with sizes [3, 5, 6, 8] for visual variety"
  - "Separation weight 1.5 (strongest) to prevent collision"
  - "Cohesion weight 0.8, alignment weight 1.0 for natural flocking"
  - "Height bounds 15-60 units keeps birds visible but not obstructive"
  - "Turn speed 0.03 creates smooth, organic turns rather than jerky movement"

patterns-established:
  - "Flocks array containing flock objects, each with birds[] and navigation data"
  - "getRandomWaypoint() for autonomous navigation across city"
  - "Wing animation via sine wave on userData.wingPhase for continuous flapping"

# Metrics
duration: 3min
completed: 2026-01-24
---

# Phase 2 Plan 1: Bird Flocks Summary

**Four bird flocks (3-8 birds each) flying through city sky with boids algorithm creating natural cohesion, separation, and alignment behavior**

## Performance

- **Duration:** 3 min
- **Started:** 2026-01-24T03:11:53Z
- **Completed:** 2026-01-24T03:14:53Z
- **Tasks:** 3
- **Files modified:** 1

## Accomplishments
- Implemented complete boids flocking algorithm with three core forces (separation, cohesion, alignment)
- Created 4 autonomous bird flocks with varying sizes for visual diversity
- Added wing flapping animation synchronized to bird movement
- Waypoint navigation system allows flocks to traverse entire city airspace

## Task Commits

Each task was committed atomically:

1. **Task 1: Add bird system global variables and configuration** - `3fb40ff` (feat)
2. **Task 2: Create bird mesh and flock creation functions** - `f2681e8` (feat)
3. **Task 3: Implement boids flocking algorithm in updBirds()** - `01a5d4c` (feat)

## Files Created/Modified
- `metropolis-3d-city-7.html` - Added complete bird flock system with boids algorithm and wing animation

## Decisions Made

**Boids algorithm weights:**
- Separation weight 1.5 (highest priority) prevents bird collisions
- Cohesion weight 0.8 keeps flocks together without over-clustering
- Alignment weight 1.0 creates smooth group movement
- Wander weight 0.3 adds organic unpredictability

**Flock configuration:**
- 4 flocks with sizes [3, 5, 6, 8] creates visual variety without performance impact
- Height bounds 15-60 units keeps birds visible above buildings but not too high
- Boundary margin 50 units allows birds to roam beyond city grid

**Movement parameters:**
- Base speed 0.15 provides visible motion without seeming frantic
- Turn speed 0.03 creates smooth, natural turns rather than sharp angles
- Speed limits (0.5x to 1.5x base) prevent unrealistic fast/slow movement

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

Bird flock system complete and ready for integration with other visual effects:
- Birds visible during all times of day (interact with day/night cycle from phase 01)
- Flocks navigate autonomously without user intervention
- Can be extended with perching behavior (future: rooftop activities)
- Performance tested: 4 flocks × average 5.5 birds = 22 entities with no lag

No blockers for next phase.

---
*Phase: 02-bird-flocks*
*Completed: 2026-01-24*
