# Project State: Metropolis

## Project Reference

See: .planning/PROJECT.md (updated 2025-01-23)

**Core value:** The city feels alive and worth watching
**Current focus:** Phase 1 - Day/Night Cycle

## Current Position

- **Milestone:** v1.0 - Visual Engagement Features
- **Phase:** 1 of 5 (Day/Night Cycle)
- **Plan:** 2 of 3 completed
- **Status:** In progress
- **Last activity:** 2026-01-24 - Completed 01-02-PLAN.md

**Progress:** ██░ 67% (2/3 plans in phase 01)

## Recent Progress

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

None yet.

## Key Decisions Log

| Date | Decision | Context |
|------|----------|---------|
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

- **Last session:** 2026-01-24 02:37 UTC
- **Stopped at:** Completed 01-02-PLAN.md
- **Resume file:** None - plan complete

---
*Last updated: 2026-01-24*
