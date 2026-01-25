# Roadmap: Metropolis v2.0 - Las Vegas Expansion

**Created:** 2026-01-25
**Milestone:** v2.0 - Las Vegas Strip
**Phases:** 6
**Requirements:** 24

## Overview

| # | Phase | Goal | Requirements | Plans | Status |
|---|-------|------|--------------|-------|--------|
| 1 | Vegas Infrastructure | Highway connection and Strip layout | INFRA-01, INFRA-02, INFRA-03, INFRA-04 | 2 | ✓ Complete |
| 2 | Iconic Landmarks | 5 recognizable casino buildings | LAND-01, LAND-02, LAND-03, LAND-04, LAND-05 | 3 | Pending |
| 3 | Vegas Lights | Dramatic night lighting | LITE-01, LITE-02, LITE-03, LITE-04 | 2 | Pending |
| 4 | Entertainment | Fountain show, chapels, Elvis | ENTR-01, ENTR-02, ENTR-03, ENTR-04 | 2 | Pending |
| 5 | Tourists | Photo-taking visitors | PED-01, PED-02, PED-03, PED-04 | 2 | Pending |
| 6 | Vegas Vehicles | Exotic cars and tour buses | VEH-01, VEH-02, VEH-03, VEH-04 | 2 | Pending |

## Phase Details

### Phase 1: Vegas Infrastructure

**Goal:** Create Route 66 highway connecting Metropolis to a new Vegas zone with The Strip

**Requirements:**
- INFRA-01: Route 66 highway with marker sign
- INFRA-02: The Strip main road layout
- INFRA-03: Independent sunny weather for Vegas
- INFRA-04: Temperature billboard

**Success Criteria:**
1. Highway extends from Metropolis edge with Route 66 sign visible
2. The Strip road is traversable with sidewalks
3. Vegas zone remains sunny regardless of Metropolis weather
4. Temperature billboard displays 95-115°F range
5. Camera can fly smoothly between Metropolis and Vegas

**Plans:** 2 plans in 2 waves ✓ Complete

Plans:
- [x] v2-01-01-PLAN.md — Highway connection, Route 66 marker, Vegas ground extension (Wave 1)
- [x] v2-01-02-PLAN.md — Strip layout, weather zone, temperature billboard (Wave 2)

---

### Phase 2: Iconic Landmarks

**Goal:** Build 5 recognizable Vegas casino landmarks with distinctive silhouettes

**Requirements:**
- LAND-01: Luxor Pyramid
- LAND-02: Bellagio with fountain lake
- LAND-03: Paris Eiffel Tower
- LAND-04: Caesars Palace
- LAND-05: Excalibur Castle

**Success Criteria:**
1. Each landmark is identifiable from silhouette alone
2. Architectural details visible at close range
3. Buildings positioned appropriately along The Strip
4. Bellagio has visible fountain lake (water surface)
5. Scale feels appropriate relative to each other

**Plans:**
- 02-01: Luxor Pyramid and Paris Eiffel Tower
- 02-02: Bellagio with fountain lake and Caesars Palace
- 02-03: Excalibur Castle

---

### Phase 3: Vegas Lights

**Goal:** Create dramatic lighting that activates at night

**Requirements:**
- LITE-01: Casino exterior lights (day: off)
- LITE-02: Night activation with Vegas brightness
- LITE-03: Luxor sky beam
- LITE-04: Per-building accent colors

**Success Criteria:**
1. Casinos look relatively plain during day
2. Night transformation is dramatic and visible from distance
3. Luxor beam shoots visibly into sky at night
4. Each landmark has distinctive light color scheme
5. Lights respond to existing day/night cycle

**Plans:**
- 03-01: Base casino lighting system tied to day/night
- 03-02: Luxor sky beam and landmark-specific accents

---

### Phase 4: Entertainment

**Goal:** Add Vegas-specific entertainment activities

**Requirements:**
- ENTR-01: Bellagio fountain show (periodic)
- ENTR-02: Fountain draws crowds
- ENTR-03: Wedding chapels with couples
- ENTR-04: Elvis impersonators

**Success Criteria:**
1. Fountain show triggers every 2-3 minutes
2. Fountains have visible water jet animation
3. Nearby tourists gather to watch fountain show
4. Wedding couples exit chapel periodically
5. Elvis impersonators walk The Strip recognizably

**Plans:**
- 04-01: Bellagio fountain show with crowd attraction
- 04-02: Wedding chapels and Elvis impersonators

---

### Phase 5: Tourists

**Goal:** Create distinct tourist pedestrians with Vegas behaviors

**Requirements:**
- PED-01: Tourist appearance distinct from regular peds
- PED-02: Slower walking speed
- PED-03: Photo-taking stops at landmarks
- PED-04: Fountain show gathering

**Success Criteria:**
1. Tourists visually distinguishable (clothing, cameras)
2. Tourists walk noticeably slower than Metropolis peds
3. Tourists stop near landmarks and "take photos"
4. Tourists move toward fountain during shows
5. Tourist density feels appropriate for The Strip

**Plans:**
- 05-01: Tourist appearance and movement
- 05-02: Photo-taking and show-watching behaviors

---

### Phase 6: Vegas Vehicles

**Goal:** Add exotic cars and tourist buses to The Strip

**Requirements:**
- VEH-01: Exotic car shapes (Lamborghini, Ferrari style)
- VEH-02: Flashy colors on Strip
- VEH-03: Open-top tourist buses
- VEH-04: Bus route along Strip

**Success Criteria:**
1. Exotic cars have low, angular sports car profiles
2. Colors are bright/flashy (red, yellow, orange)
3. Tourist buses have open top deck with visible seats
4. Buses follow Strip route appropriately
5. Vehicle mix feels distinct from Metropolis traffic

**Plans:**
- 06-01: Exotic cars with distinctive shapes
- 06-02: Open-top tourist buses with route

---

## Dependency Graph

```
Phase 1 (Infrastructure)
    ↓
Phase 2 (Landmarks) ──→ Phase 3 (Lights)
    ↓                       ↓
Phase 4 (Entertainment) ←───┘
    ↓
Phase 5 (Tourists)
    ↓
Phase 6 (Vehicles)
```

**Critical path:** 1 → 2 → 3 → 4 → 5 → 6

Phases must be sequential because:
- Landmarks need infrastructure (Strip layout)
- Lights need landmarks to attach to
- Entertainment needs landmarks and lights for context
- Tourists need landmarks for photo targets
- Vehicles need roads and context

---

## Milestone Success Criteria

When v2.0 is complete:

1. **Seamless connection**: Player can fly from Metropolis to Vegas via Route 66
2. **Recognizable Vegas**: All 5 landmarks identifiable at a glance
3. **Day/night drama**: Vegas transforms dramatically at night with lights
4. **Vegas vibe**: Tourists, exotic cars, Elvis, fountain shows create atmosphere
5. **Independent weather**: Vegas stays sunny while Metropolis may have storms

## Progress

```
Phase 1: ██████████ 100% ✓
Phase 2: ░░░░░░░░░░ 0%
Phase 3: ░░░░░░░░░░ 0%
Phase 4: ░░░░░░░░░░ 0%
Phase 5: ░░░░░░░░░░ 0%
Phase 6: ░░░░░░░░░░ 0%
─────────────────────
Overall: █░░░░░░░░░ 17% (1/6 phases)
```

---
*Roadmap created: 2026-01-25*
*Last updated: 2026-01-25 after Phase 1 complete*
