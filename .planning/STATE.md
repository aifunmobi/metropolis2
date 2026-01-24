# Project State: Metropolis

## Project Reference

See: .planning/PROJECT.md (updated 2025-01-23)

**Core value:** The city feels alive and worth watching
**Current focus:** Phase 3 - Street Performers

## Current Position

- **Milestone:** v1.0 - Visual Engagement Features
- **Phase:** 3 of 5 (Street Performers)
- **Plan:** 1 of 3 completed
- **Status:** In progress
- **Last activity:** 2026-01-24 - Completed 03-01-PLAN.md

**Progress:** ██████░░░░░░░░ 43% (6/14 plans across all phases)

## Recent Progress

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

- **Last session:** 2026-01-24 03:41 UTC
- **Stopped at:** Completed 03-01-PLAN.md
- **Resume file:** None

---
*Last updated: 2026-01-24*
