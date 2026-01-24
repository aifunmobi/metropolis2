---
phase: 04-subway-system
plan: 02
subsystem: transportation
tags: [three.js, subway, pedestrians, state-machine, crowd-behavior]

# Dependency graph
requires:
  - phase: 04-subway-system
    plan: 01
    provides: subway infrastructure, stations, train, updSubway
provides:
  - Pedestrian subway ridership behavior
  - Station activity indicators
  - Subway passenger tracking
affects: [future pedestrian systems, rooftop phase may reference pedestrian patterns]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - "Subway pedestrian states follow existing bus/performer patterns"
    - "Cross-system protection for subway passengers (bus, garbage)"
    - "Activity light indicator pattern for visual feedback"

key-files:
  created: []
  modified:
    - metropolis-3d-city-7.html

key-decisions:
  - "8% subway attraction chance balances against other diversions"
  - "30-unit attraction radius matches performer radius"
  - "8-20 second ride duration for observable transit time"
  - "Max 12 subway passengers to prevent overcrowding"
  - "Activity lights show green when station active"

patterns-established:
  - "Pedestrian diversion: setNewPedTarget() handles attraction, updPeds() handles state"
  - "Cross-system protection: filter in assignPedToStop, skip in garbage suction"
  - "Visual feedback: activity light on station mesh, updated in system updater"

# Metrics
duration: 2min
completed: 2026-01-24
---

# Phase 4 Plan 2: Subway Pedestrian Interaction Summary

**Pedestrians walk to nearby subway stations, disappear into entrances, ride for 8-20 seconds, and emerge at different stations with activity indicator lights**

## Performance

- **Duration:** 2 min (123 seconds)
- **Started:** 2026-01-24T04:12:14Z
- **Completed:** 2026-01-24T04:14:17Z
- **Tasks:** 3
- **Files modified:** 1

## Accomplishments
- Pedestrians within 30 units of subway stations have 8% chance to walk toward entrance
- Pedestrians disappear when entering station, reappear at different station after 8-20 seconds
- Station entrance lights glow green when pedestrians are entering/exiting or train stopped
- Subway-bound pedestrians protected from bus assignment and garbage truck suction

## Task Commits

Each task was committed atomically:

1. **Task 1: Add subway passenger tracking and pedestrian state** - `f7b15a4` (feat)
2. **Task 2: Implement subway pedestrian states in updPeds** - `72ebc21` (feat)
3. **Task 3: Add visual activity indicators to subway stations** - `5a93bc9` (feat)

## Files Created/Modified
- `metropolis-3d-city-7.html` - Added subwayPassengers array, SUBWAY_MAX_PASSENGERS constant, toSubwayStation/inSubway state handling in setNewPedTarget() and updPeds(), activity light in mkSubwayStation(), activity update in updSubway(), protection in assignPedToStop() and garbage truck suction

## Decisions Made
- 8% attraction chance chosen to balance subway usage against bus (10%), performers (15%), and buildings (10%)
- 30-unit attraction radius matches performer attraction for consistent pedestrian behavior
- 8-20 second ride duration provides observable transit without excessive wait
- Max 12 passengers prevents subway from draining pedestrian population
- Activity lights use green color consistent with "active/go" signaling

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness
- Phase 04 (Subway System) complete
- Subway infrastructure operational with passenger flow
- Ready for Phase 05: Rooftop Features
- All pedestrian state patterns documented for future extensions

---
*Phase: 04-subway-system*
*Completed: 2026-01-24*
