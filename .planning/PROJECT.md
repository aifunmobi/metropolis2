# Metropolis 3D City Simulation

## What This Is

An interactive 3D city simulation built as a single HTML file using Three.js. Users fly through a living city observing urban life — vehicles, pedestrians, weather, and random events. This milestone adds 5 new features to make watching the city more visually interesting and engaging.

## Core Value

The city feels alive and worth watching — there's always something happening that catches your eye.

## Requirements

### Validated

- ✓ 3D city with buildings, roads, sidewalks, crosswalks — existing
- ✓ Vehicle traffic system with cars, buses, emergency vehicles — existing
- ✓ Pedestrian system with state machine behaviors — existing
- ✓ Traffic light system at intersections — existing
- ✓ Weather system (sunny, cloudy, rain, storm) — existing
- ✓ Random special events (parade, ice cream truck, etc.) — existing
- ✓ Flying camera controls — existing

### Active

- [ ] Day/night cycle with dynamic lighting
- [ ] Bird flocks with organic movement
- [ ] Street performers that attract crowds
- [ ] Subway system with trains and stations
- [ ] Rooftop activity (gardens, pools, parties)

### Out of Scope

- Sound/audio — visual focus only
- User interaction with entities — observation only
- Multiplayer — single user experience
- Save/load state — session-based

## Context

The entire application is contained in a single HTML file (~5000 lines) using Three.js loaded from CDN. All systems follow a make/update pattern: `mk*()` functions create objects, `upd*()` functions update them each frame.

Existing systems provide good patterns to follow:
- Weather system for environmental effects
- Special events system for temporary activities
- Pedestrian state machine for crowd behaviors

## Constraints

- **Single file**: All code must remain in metropolis-3d-city-7.html
- **No dependencies**: Only Three.js from CDN, no additional libraries
- **Performance**: Must maintain smooth framerate with existing entity counts

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 5 visual features over interactivity | User wants to observe, not control | — Pending |
| Build on existing patterns | Consistent codebase, faster development | — Pending |

---
*Last updated: 2025-01-23 after initialization*
