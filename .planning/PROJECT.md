# Metropolis 3D City Simulation

## What This Is

An interactive 3D city simulation built as a single HTML file using Three.js. Users fly through a living city observing urban life — vehicles, pedestrians, weather, and random events. This milestone expands the world with Las Vegas connected via Route 66, featuring The Strip with iconic casino landmarks, flashy lights, tourists, and Vegas-style entertainment.

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
- ✓ Day/night cycle with dynamic lighting — v1.0
- ✓ Bird flocks with organic movement — v1.0
- ✓ Street performers that attract crowds — v1.0
- ✓ Subway system with trains and stations — v1.0
- ✓ Rooftop activity (gardens, pools, parties) — v1.0

### Active

- [ ] Route 66 highway connecting Metropolis to Vegas
- [ ] The Strip main road with Vegas layout
- [ ] Luxor Pyramid with sky beam
- [ ] Bellagio with fountain show
- [ ] Paris Eiffel Tower replica
- [ ] Caesars Palace
- [ ] Excalibur Castle
- [ ] Vegas always sunny with temperature billboard
- [ ] Casino lights active only at night
- [ ] Tourist pedestrians taking photos
- [ ] Wedding chapels with couples
- [ ] Elvis impersonators
- [ ] Exotic cars (Lamborghinis, Ferraris)
- [ ] Open-top tourist buses

### Out of Scope

- Sound/audio — visual focus only
- User interaction with entities — observation only
- Multiplayer — single user experience
- Save/load state — session-based
- Interior casino scenes — exterior only
- Gambling mechanics — visual observation only
- Real-time crowd dynamics for shows — simplified attraction system

## Context

The entire application is contained in a single HTML file (~5000 lines) using Three.js loaded from CDN. All systems follow a make/update pattern: `mk*()` functions create objects, `upd*()` functions update them each frame.

Existing systems provide good patterns to follow:
- Day/night cycle for Vegas lights timing
- Pedestrian state machine for tourist behaviors
- Special events system for fountain shows
- Street performer crowds for tourist photo-taking

The v1.0 milestone added day/night cycle, birds, performers, subway, and rooftops. Vegas expansion builds on these patterns, particularly using the day/night system for dramatic casino lighting effects.

## Constraints

- **Single file**: All code must remain in metropolis-3d-city-7.html
- **No dependencies**: Only Three.js from CDN, no additional libraries
- **Performance**: Must maintain smooth framerate with expanded world
- **Visual fidelity**: Vegas landmarks must have recognizable silhouettes AND architectural detail

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 5 visual features over interactivity | User wants to observe, not control | ✓ Good |
| Build on existing patterns | Consistent codebase, faster development | ✓ Good |
| 5 Vegas landmarks (Luxor, Bellagio, Paris, Caesars, Excalibur) | Iconic and recognizable, manageable scope | — Pending |
| Route 66 highway connection | Extends existing road, no flying needed | — Pending |
| Vegas always sunny | Distinct from Metropolis variable weather | — Pending |
| Lights only on at night | Dramatic transformation using day/night cycle | — Pending |

---
*Last updated: 2026-01-25 after v2.0 Vegas milestone initialization*
