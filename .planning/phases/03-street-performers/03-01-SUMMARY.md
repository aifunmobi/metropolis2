---
phase: 03-street-performers
plan: 01
type: summary
subsystem: street-performers
tags: [performers, musicians, statues, sidewalk, animation, three.js]
dependencies:
  requires: [02-02-bird-landing]
  provides: [performer-entities, performer-spawn-system, performer-animations]
  affects: []
tech-stack:
  added: []
  patterns: [entity-spawn, timed-despawn, animation-state]
key-files:
  created: []
  modified: [metropolis-3d-city-7.html]
decisions:
  - performer-types-musician-statue
  - spawn-interval-45-seconds
  - performance-duration-60-120-seconds
  - max-3-simultaneous-performers
  - sidewalk-facing-road-orientation
metrics:
  duration: 262 seconds (~4.4 minutes)
  completed: 2026-01-24
---

# Phase 03 Plan 01: Street Performer System Summary

**One-liner:** Street performers (musicians with guitars, silver living statues) spawn periodically on sidewalks, perform for 60-120 seconds with animations, creating focal points for pedestrian attention.

## What Was Built

Implemented the foundational street performer system with two distinct performer types that appear on city sidewalks.

### Core Components

1. **Performer Configuration (PERFORMER_CFG)**
   - Maximum 3 simultaneous performers
   - Spawn check every 45 seconds with 50% spawn chance
   - Performance duration randomized 60-120 seconds
   - Crowd attraction settings (12-unit radius, max 8 watchers)

2. **Musician Performer**
   - Dark red outfit with black beret
   - Acoustic guitar with brown wood body and neck
   - Strumming animation using sine wave arm rotation
   - Guitar held in proper playing position with arms positioned accordingly

3. **Statue Performer**
   - Metallic silver appearance (metalness: 0.7, roughness: 0.3)
   - Top hat and dramatic raised-arm pose
   - Small pedestal base and tip jar on ground
   - Subtle occasional head movement for "living statue" effect

4. **Spawn System**
   - Random block and sidewalk side selection
   - Performers positioned on sidewalks facing toward road
   - Proper orientation calculation per sidewalk direction (N/S/E/W)
   - 20-unit minimum spacing between performers
   - 50/50 random split between musician and statue types

5. **Update System**
   - Periodic spawn checks based on configured interval
   - Duration-based despawn with automatic cleanup
   - Musician strumming animation (continuous arm movement)
   - Statue occasional micro-movements (0.1% chance per frame)
   - Watcher release on despawn (prepared for future crowd system)

## Technical Decisions

### Decision: Two Performer Types (Musician and Statue)

**Context:** Need visually distinct performers that represent different street performance styles.

**Chosen:** Musician with guitar and living statue with metallic finish

**Rationale:**
- Musicians are recognizable with instrument props
- Statues provide contrast (still vs. animated)
- Both are common real-world street performers
- Different animation requirements exercise variety

**Implementation:**
- mkMusician() creates guitarist with instrument geometry
- mkStatue() creates silver performer with pedestal
- Type stored in userData.type for behavior differentiation

**Trade-offs:**
- More types = more visual variety but more code complexity
- Two types balance variety with maintainability
- Future performers (jugglers, dancers) can follow same pattern

---

### Decision: 45-Second Spawn Interval with 50% Chance

**Context:** Balance performer presence without overcrowding sidewalks.

**Chosen:** Check every 45 seconds, 50% chance to spawn if under max

**Rationale:**
- 45 seconds = ~22.5 second average spawn rate
- With 60-120 second durations, maintains 1-3 performers typically
- Spawn chance prevents predictable timing
- Natural variation in performer density

**Implementation:**
- lastPerformerCheck tracks timing
- Random check prevents every-45-second spawn
- Max cap (3) prevents overflow regardless of timing

**Trade-offs:**
- Longer interval = rarer performers but more noticeable
- Shorter interval = more consistent presence but less special
- 45s chosen to make performers feel occasional, not constant

---

### Decision: Sidewalk Facing Road Orientation

**Context:** Performers need natural positioning that makes sense for attracting pedestrians.

**Chosen:** Face toward the road (away from buildings)

**Rationale:**
- Real performers face traffic for visibility
- Creates natural "stage" area on sidewalk
- Aligns with future crowd-gathering mechanic
- Matches pedestrian flow patterns (walking along sidewalk)

**Implementation:**
- Side 0 (north): facing = Math.PI (south toward road)
- Side 1 (south): facing = 0 (north toward road)
- Side 2 (west): facing = Math.PI/2 (east toward road)
- Side 3 (east): facing = -Math.PI/2 (west toward road)

**Trade-offs:**
- Could face random directions for variety
- Road-facing is more realistic and functional
- Supports future pedestrian-watching behavior

---

### Decision: Duration 60-120 Seconds

**Context:** Balance performer lifetime between too fleeting and overstaying.

**Chosen:** Random duration between 1-2 minutes per performance

**Rationale:**
- 60 seconds minimum = enough time for player to discover and observe
- 120 seconds maximum = doesn't become stale or static
- Randomization prevents predictable timing
- Matches real street performer set lengths (simplified)

**Implementation:**
- Calculated on spawn: duration = min + random * (max - min)
- Checked in updPerformers: elapsed > duration triggers despawn
- userData.spawnTime and duration track lifetime

**Trade-offs:**
- Longer = more chance to observe but less turnover
- Shorter = more dynamic but harder to find
- 60-120s balances discoverability with freshness

---

## Implementation Notes

### Sidewalk Positioning Calculation

Performers use the same sidewalk positioning as other entities:
- `innerSize = GRID.cellSize - GRID.roadWidth = 16` (building area)
- `swOffset = GRID.sidewalkWidth / 2 = 1` (sidewalk edge offset)
- Position calculated from block center ± innerSize/2 ± swOffset
- alongOffset provides variation along the sidewalk (avoids corners)

### Animation Patterns

**Musician strumming:**
```javascript
performer.userData.animPhase += 0.1;
const strum = Math.sin(animPhase * 3) * 0.15;
strumArm.rotation.x = 0.3 + strum;
```
- Base rotation 0.3 maintains hold position
- Sine wave (frequency 3) creates rhythmic strumming
- Amplitude 0.15 provides visible but realistic movement

**Statue micro-movement:**
```javascript
if (Math.random() < 0.001) {
    head.rotation.y = (Math.random() - 0.5) * 0.1;
}
```
- 0.1% chance per frame = ~1-2 movements during 60-120s performance
- Small rotation (±0.05 radians) = subtle "living statue" effect
- Infrequent enough to surprise, common enough to notice

### Watcher System Preparation

Although pedestrian crowd-watching is not yet implemented, the system is prepared:
- `userData.watchers = []` array tracks watching pedestrians
- On despawn, watchers are released back to walking state
- PERFORMER_CFG includes crowd settings (radius, max count)
- Future plan will implement pedestrian attraction and watching behavior

## Deviations from Plan

None - plan executed exactly as written.

## Next Phase Readiness

**Phase 03 Plan 02: Pedestrian Performer Interaction**
- Performers now exist and are trackable
- userData.watchers array prepared for crowd assignment
- PERFORMER_CFG contains all necessary crowd parameters
- Performer position and duration accessible for pedestrian decision-making

**Blockers:** None

**Concerns:** None

**Ready to proceed:** Yes

## Files Modified

### metropolis-3d-city-7.html
**Lines changed:** ~292 additions

**Changes:**
- Added PERFORMER_CFG configuration object (lines 129-136)
- Added performers[] global array (line 177)
- Added lastPerformerCheck timing variable (line 193)
- Added mkMusician() function (lines 4136-4211)
- Added mkStatue() function (lines 4213-4287)
- Added spawnPerformer() function (lines 4425-4492)
- Added updPerformers() function (lines 5296-5342)
- Added updPerformers(t) call in animate() (line 5375)
- Added spawnPerformer() call in init() (line 270)

## Commits

| Commit | Message | Files |
|--------|---------|-------|
| 724dcc3 | feat(03-01): add performer system configuration and global variables | metropolis-3d-city-7.html |
| 75cec1d | feat(03-01): create musician and statue performer mesh functions | metropolis-3d-city-7.html |
| eccaf36 | feat(03-01): add performer spawn and update system | metropolis-3d-city-7.html |

## Testing Notes

To verify implementation:
1. Open metropolis-3d-city-7.html in browser
2. Within 45 seconds, observe first performer spawn on a sidewalk
3. Verify performer type (guitarist with red outfit OR silver statue with top hat)
4. If musician: observe strumming arm animation
5. If statue: wait for subtle head movements (occasional)
6. Wait 60-120 seconds and verify performer disappears
7. Over time, verify maximum 3 performers appear simultaneously
8. Verify performers appear on different sidewalks around the city

**Visual Checks:**
- Musicians clearly identifiable by guitar and dark red outfit
- Statues clearly identifiable by silver metallic finish and top hat
- Performers positioned on sidewalks (not in roads or on buildings)
- Performers facing toward roads (away from buildings)
- Minimum 20-unit spacing maintained between performers

**Animation Checks:**
- Musician arm continuously moves in strumming motion
- Statue mostly still with very occasional subtle head turn
- No other unexpected movements or rotations

## Performance Impact

**Added entities:** 0-3 performers maximum (lightweight compared to 50 pedestrians)

**Added geometry:**
- Musician: ~12 meshes (body, head, hat, legs, arms, guitar parts)
- Statue: ~11 meshes (body, head, hat parts, legs, arms, base, jar)
- Total: ~23-35 meshes maximum

**Per-frame updates:**
- Spawn check: once per 45 seconds (negligible)
- Per-performer update: ~5 operations (duration check, animation)
- Maximum 3 performers = ~15 operations per frame
- Minimal performance impact

**Memory:**
- Performers array: 3 objects maximum
- Each performer: standard THREE.Group with userData
- Negligible memory footprint

## Knowledge for Future Phases

### For Phase 03-02 (Pedestrian Interaction)

**Performer Detection:**
- Iterate `performers` array to find nearby performers
- Check distance from pedestrian to `performer.position`
- Use `PERFORMER_CFG.attractRadius` (12 units) for attraction range

**Crowd Positioning:**
- Position pedestrians at `PERFORMER_CFG.crowdRadius` (3 units) from performer
- Respect `PERFORMER_CFG.maxCrowd` (8) limit
- Add pedestrians to `performer.userData.watchers` array

**State Management:**
- Set pedestrian `userData.state = 'watchingPerformer'`
- Store reference `userData.watchingPerformer = performer`
- On performer despawn, watchers automatically released (already implemented)

**Considerations:**
- Performers can despawn while pedestrians watching (cleanup already handles this)
- Multiple pedestrians may target same performer (need crowd positioning logic)
- Pedestrians need path to performer (may need navigation)

### For Phase 03-03+ (Future Enhancements)

**Additional Performer Types:**
- Follow mkMusician/mkStatue pattern
- Add to random selection in spawnPerformer()
- Define type-specific animations in updPerformers()

**Performance Quality:**
- Could add userData.performanceQuality affecting crowd size
- Could implement tips/earnings visual feedback
- Could add performer fatigue/energy affecting duration

**Spawn Intelligence:**
- Could prefer high-traffic sidewalks (near crosswalks, bus stops)
- Could avoid spawning near other events (ice cream truck, etc.)
- Could spawn in pairs/groups for collaborative performances

---

**Summary created:** 2026-01-24
**Phase status:** In progress (1/3 plans complete)
**Next plan:** 03-02-PLAN.md (Pedestrian Performer Interaction)
