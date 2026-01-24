# Roadmap: Metropolis City Features

**Created:** 2025-01-23
**Milestone:** v1.0 - Visual Engagement Features

## Overview

5 phases delivering 24 requirements to make watching the city more interesting.

| # | Phase | Goal | Requirements | Status |
|---|-------|------|--------------|--------|
| 1 | Day/Night Cycle | City transitions through time with dynamic lighting | DAY-01 to DAY-06 | ○ Pending |
| 2 | Bird Flocks | Organic bird movement adds life to the sky | BIRD-01 to BIRD-04 | ○ Pending |
| 3 | Street Performers | Sidewalk entertainment draws crowds | PERF-01 to PERF-05 | ○ Pending |
| 4 | Subway System | Underground transit adds infrastructure depth | SUB-01 to SUB-05 | ○ Pending |
| 5 | Rooftop Life | Activity visible from above | ROOF-01 to ROOF-04 | ○ Pending |

---

## Phase 1: Day/Night Cycle

**Goal:** The city transitions through time of day with dramatic lighting changes that transform the visual experience.

**Requirements:** DAY-01, DAY-02, DAY-03, DAY-04, DAY-05, DAY-06

**Plans:** 3 plans

Plans:
- [ ] 01-01-PLAN.md — Time system with sky color and lighting transitions
- [ ] 01-02-PLAN.md — Sun and moon positioning in sky
- [ ] 01-03-PLAN.md — Streetlights, headlights, and window light adjustment

**Success Criteria:**
1. User observes gradual sky color change from blue (day) to orange (dusk) to dark blue (night)
2. Sun visible during day, moon during night, positioned correctly in sky
3. Streetlight poles emit light only during night hours
4. Cars have visible headlight beams during night
5. Building windows show more lit windows at night vs day

**Dependencies:** None (foundational feature)

---

## Phase 2: Bird Flocks

**Goal:** Flocks of birds add organic, unpredictable movement to the city sky and ground.

**Requirements:** BIRD-01, BIRD-02, BIRD-03, BIRD-04

**Success Criteria:**
1. Multiple bird flocks visible flying through city airspace
2. Flocks exhibit natural flocking behavior (cohesion, alignment, separation)
3. Birds periodically land on rooftops and sidewalks
4. Landed birds take flight when pedestrians approach within ~3 units
5. Different flock sizes create visual variety

**Dependencies:** None

---

## Phase 3: Street Performers

**Goal:** Street performers create sidewalk gatherings that add human interest and crowd dynamics.

**Requirements:** PERF-01, PERF-02, PERF-03, PERF-04, PERF-05

**Success Criteria:**
1. Performers spawn at random sidewalk locations periodically
2. Nearby pedestrians change behavior to approach performer
3. Watching pedestrians form semicircle facing performer
4. After watching duration, pedestrians resume normal walking
5. At least 2 performer types distinguishable visually (musician with instrument, statue performer)

**Dependencies:** Builds on existing pedestrian state machine

---

## Phase 4: Subway System

**Goal:** Subway trains and stations add another transportation layer and infrastructure feel.

**Requirements:** SUB-01, SUB-02, SUB-03, SUB-04, SUB-05

**Success Criteria:**
1. Visible station entrances at street level (stairs down or covered entrance)
2. Trains emerge from underground at designated points
3. Trains pause at stations for ~5 seconds before continuing
4. Pedestrians enter/exit near station entrances
5. Train travels visible route between at least 2 stations

**Dependencies:** None

---

## Phase 5: Rooftop Life

**Goal:** Building rooftops have visible activity to observe from above.

**Requirements:** ROOF-01, ROOF-02, ROOF-03, ROOF-04

**Success Criteria:**
1. ~20% of tall buildings have visible rooftop gardens (green patches, planters)
2. ~10% of buildings have visible rooftop pools (blue rectangles)
3. Occasional rooftop party spawns with string lights visible
4. Small figures visible on rooftops with active features

**Dependencies:** None

---

## Progress

```
Phase 1: ░░░░░░░░░░ 0%
Phase 2: ░░░░░░░░░░ 0%
Phase 3: ░░░░░░░░░░ 0%
Phase 4: ░░░░░░░░░░ 0%
Phase 5: ░░░░░░░░░░ 0%
─────────────────────
Overall: ░░░░░░░░░░ 0%
```

---
*Roadmap created: 2025-01-23*
*Last updated: 2025-01-23*
