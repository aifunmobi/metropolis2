---
phase: 01-day-night-cycle
plan: 01
subsystem: lighting
tags: [threejs, lighting, time-system, sky-transitions]

# Dependency graph
requires:
  - phase: initialization
    provides: Basic metropolis-3d-city-7.html structure
provides:
  - Time-of-day system with continuous 0-1 cycle
  - Sky color transitions through 5 phases (midnight, dawn, day, dusk, night)
  - Dynamic lighting adjustments based on time
  - isNight flag for other systems to reference
affects: [01-02, 01-03, 01-04]

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Time system using normalized 0-1 value for 24-hour cycle
    - Color interpolation using Three.js Color.lerpColors
    - Sine wave for smooth lighting intensity transitions

key-files:
  created: []
  modified:
    - metropolis-3d-city-7.html

key-decisions:
  - "Start time at 0.25 (dawn) for visually interesting initial state"
  - "Full day/night cycle completes in ~200 seconds at 60fps"
  - "Weather system overrides sky colors when not sunny"
  - "Light references stored globally for dynamic updates"

patterns-established:
  - "updDayNight(dt) function follows make/update pattern"
  - "Lighting intensities adjust via sine wave (0 at midnight, 1 at noon)"
  - "Sky colors transition through 5 distinct phases with smooth interpolation"

# Metrics
duration: 3min
completed: 2026-01-24
---

# Phase 01 Plan 01: Core Time System Summary

**Time-of-day system with smooth sky transitions through 5 phases and dynamic lighting using sine-based intensity curves**

## Performance

- **Duration:** 3 min
- **Started:** 2026-01-24T02:28:15Z
- **Completed:** 2026-01-24T02:31:14Z
- **Tasks:** 3
- **Files modified:** 1

## Accomplishments
- Time-of-day state advances continuously 0-1 representing full 24-hour cycle
- Sky and fog colors smoothly transition through midnight, dawn, day, dusk, night phases
- Directional light (sun) intensity and color adjust dynamically based on time
- Ambient and hemisphere lights dim at night, brighten during day
- Weather system integration - day/night cycle respected when weather is sunny

## Task Commits

Each task was committed atomically:

1. **Task 1: Add time-of-day state and configuration** - `d1c3864` (feat)
2. **Task 2: Implement updDayNight() with smooth transitions** - `a207acf` (feat)
3. **Task 3: Wire updDayNight into main loop and test** - `dd7c58c` (feat)

## Files Created/Modified
- `metropolis-3d-city-7.html` - Added time-of-day system with SKY_COLORS palette, updDayNight function, light references, and main loop integration

## Decisions Made

**1. Time starts at 0.25 (dawn)**
- Rationale: Provides visually interesting orange/pink sky at startup instead of plain blue

**2. Full cycle in ~200 seconds**
- Rationale: dayNightSpeed of 0.005 allows users to observe full day/night within 3-4 minutes of watching

**3. Weather overrides only when not sunny**
- Rationale: Preserves day/night cycle visibility during normal sunny conditions, but allows dramatic weather effects to take precedence

**4. Sine wave for lighting intensity**
- Rationale: `Math.sin(t * Math.PI)` provides natural smooth transition peaking at noon, zero at midnight

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 2 - Missing Critical] Fixed weather system to respect day/night cycle**
- **Found during:** Task 3 (Main loop integration)
- **Issue:** applyWeatherEffects() was setting fixed sky color for sunny weather, overriding day/night transitions
- **Fix:** Modified sunny case to only initialize fog, allowing updDayNight to control background and fog colors
- **Files modified:** metropolis-3d-city-7.html
- **Verification:** Weather changes preserve day/night cycle when returning to sunny
- **Committed in:** dd7c58c (Task 3 commit)

---

**Total deviations:** 1 auto-fixed (1 missing critical)
**Impact on plan:** Auto-fix necessary for day/night cycle to remain visible. Without it, pressing 'R' to cycle weather would break the time system.

## Issues Encountered
None - plan executed smoothly.

## User Setup Required
None - no external service configuration required.

## Next Phase Readiness

**Ready for next phases:**
- Sun/moon positioning (01-02) can now use timeOfDay variable
- Streetlight system (01-03) can use isNight flag for activation
- Headlight/window lights (01-04) can use isNight flag for activation

**Foundation established:**
- timeOfDay (0-1) - normalized time reference for all time-dependent features
- isNight (boolean) - quick check for night-specific behaviors
- SKY_COLORS palette - consistent color scheme for future sky enhancements
- Light references (sunLight, ambientLight, hemiLight) - available for further manipulation

**No blockers** - system working as designed with smooth transitions and weather integration.

---
*Phase: 01-day-night-cycle*
*Completed: 2026-01-24*
