---
phase: 01-day-night-cycle
plan: 03
subsystem: lighting
tags: [threejs, streetlights, headlights, window-lighting, night-illumination]

# Dependency graph
requires:
  - phase: 01-01
    provides: Time-of-day system with isNight flag, updDayNight function
provides:
  - Streetlight poles along all roads with night-time activation
  - Streetlight PointLights illuminating road surfaces at night
  - Car headlight activation synchronized with day/night cycle
  - Window lighting probability adjusted by time (70% night, 20% day)
  - Bulk window updates during day/night transitions
affects: [01-04, future lighting features]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Streetlights use smooth intensity transitions (0.05 lerp factor)
    - Car headlights tracked in userData.headlights array
    - Window lighting uses probability-based state changes
    - Bulk updates on transition for immediate visual impact

key-files:
  created: []
  modified:
    - metropolis-3d-city-7.html

key-decisions:
  - "Streetlights placed every 16 units along roads, avoiding intersections"
  - "Streetlight intensity 1.5 at night for warm road illumination"
  - "Car headlights change material color rather than adding PointLights"
  - "Window night probability 70%, day probability 20%"
  - "30% of windows bulk-update during day/night transitions"

patterns-established:
  - "mkStreetlights() creates poles with userData.light and userData.bulb references"
  - "updStreetlights() smoothly transitions intensity and bulb color"
  - "Car headlights cloned from shared material for individual control"
  - "Window lighting uses probability checks vs simple toggle"

# Metrics
duration: 5min
completed: 2026-01-24
---

# Phase 01 Plan 03: Lighting Effects Summary

**Streetlights, car headlights, and building windows activate at night creating a vibrant illuminated cityscape**

## Performance

- **Duration:** 5 min
- **Started:** 2026-01-24T02:35:49Z
- **Completed:** 2026-01-24T02:40:30Z
- **Tasks:** 4 (3 implementation + 1 verification checkpoint)
- **Files modified:** 1

## Accomplishments
- Streetlight poles placed along all roads at regular 16-unit intervals
- Streetlights emit warm yellow-white light (0xffeeaa) at night with intensity 1.5
- Car headlights brighten from dim (0x333322) to bright yellow (0xffffee) at night
- Building windows shift from 20% lit during day to 70% lit at night
- Day/night transitions trigger immediate bulk updates for 30% of all windows
- Complete nighttime city ambiance with multiple light sources

## Task Commits

Each task was committed atomically:

1. **Task 1: Create streetlights along roads** - `8db0415` (feat)
2. **Task 2: Create updStreetlights and update headlights** - `110fd93` (feat)
3. **Task 3: Adjust window light probability** - `ba4ec93` (feat)
4. **Task 4: Human verification checkpoint** - Approved by user

## Files Created/Modified
- `metropolis-3d-city-7.html` - Added streetlights array, mkStreetlights() function, updStreetlights() function, headlight tracking system, probability-based window lighting

## Decisions Made

**1. Streetlight placement pattern**
- Rationale: Every 16 units provides consistent illumination without clutter, skipping intersections avoids conflicts with traffic lights

**2. Streetlight PointLight intensity of 1.5**
- Rationale: Strong enough to visibly illuminate road surface, warm enough to create inviting nighttime atmosphere

**3. Car headlights use material color change only**
- Rationale: Adding PointLights for each car (25+ vehicles) would impact performance; material color provides visual effect without overhead

**4. Window probability 70% night vs 20% day**
- Rationale: Creates clear visual distinction between day/night, represents realistic building occupancy patterns

**5. 30% bulk window update on transitions**
- Rationale: Immediate visual impact when crossing day/night threshold, combined with gradual changes for organic feel

## Deviations from Plan

None - plan executed exactly as written.

## Issues Encountered

None - plan executed smoothly. All three lighting systems integrated seamlessly with existing day/night cycle.

## User Setup Required

None - no external service configuration required.

## Next Phase Readiness

**Complete day/night cycle foundation:**
- All three planned lighting effects implemented and verified
- Streetlights illuminate roads at night
- Vehicles show active headlights at night
- Buildings display occupancy patterns through window lighting
- Combined with Plans 01-02: complete 24-hour cycle with sky, sun, moon, and lighting

**Phase 01 complete - ready for next visual features:**
- Day/night cycle fully functional with all planned effects
- Time control (T key) allows rapid testing of transitions
- Weather system (R key) still functional, respects day/night when sunny
- Foundation established for future time-dependent features (birds, performers, etc.)

**No blockers** - all lighting effects working as designed with smooth transitions and no performance issues.

---
*Phase: 01-day-night-cycle*
*Completed: 2026-01-24*
