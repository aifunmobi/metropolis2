# Project State: Metropolis

## Project Reference

See: .planning/PROJECT.md (updated 2025-01-23)

**Core value:** The city feels alive and worth watching
**Current focus:** Phase 2 - Bird Flocks

## Current Position

- **Milestone:** v1.0 - Visual Engagement Features
- **Phase:** 2 of 5 (Bird Flocks)
- **Plan:** 1 of 2 completed
- **Status:** In progress
- **Last activity:** 2026-01-24 - Completed 02-01-PLAN.md

**Progress:** ████ 80% (4/5 plans across all phases)

## Recent Progress

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

- **Last session:** 2026-01-24 03:14 UTC
- **Stopped at:** Completed 02-01-PLAN.md
- **Resume file:** None

---
*Last updated: 2026-01-24*
