---
phase: 03-street-performers
plan: 02
type: summary
subsystem: street-performers
tags: [pedestrians, crowds, performer-interaction, state-machine, three.js]
dependencies:
  requires: [03-01-performer-entities]
  provides: [crowd-behavior, performer-attraction, watching-state]
  affects: []
tech-stack:
  added: []
  patterns: [state-machine-extension, semicircle-formation, duration-tracking]
key-files:
  created: []
  modified: [metropolis-3d-city-7.html]
decisions:
  - attraction-chance-15-percent
  - semicircle-crowd-formation
  - watch-duration-10-30-seconds
  - performer-watchers-protected-from-interruption
metrics:
  duration: 128 seconds (~2.1 minutes)
  completed: 2026-01-24
---

# Phase 03 Plan 02: Pedestrian Performer Interaction Summary

**One-liner:** Pedestrians detect nearby performers, form semicircle crowds facing them, watch for 10-30 seconds, then resume walking, creating organic gatherings around street performances.

## What Was Built

Implemented dynamic crowd formation where pedestrians are attracted to street performers and gather to watch them.

### Core Components

1. **Performer Attraction Logic (in setNewPedTarget)**
   - 15% chance for walking pedestrians to notice nearby performers
   - Distance check using PERFORMER_CFG.attractRadius (12 units)
   - Max crowd limit enforcement (skip performers at capacity)
   - Nearest performer selection within attraction radius

2. **Semicircle Formation Calculation**
   - Crowd positions calculated around performer facing direction
   - 144-degree semicircle (0.8π angleSpread) in front of performer
   - Watcher index determines position along semicircle arc
   - crowdRadius (3 units) maintains consistent distance
   - Each pedestrian gets unique angle offset based on arrival order

3. **Pedestrian State Machine Extensions**
   - New state: `towardPerformer` - walking to watching position
   - New state: `watchingPerformer` - standing still facing performer
   - State transitions: walking → towardPerformer → watchingPerformer → walking
   - Watch duration randomized 10-30 seconds per pedestrian

4. **Watch Behavior Implementation**
   - Walking animation while approaching performer
   - Arrival detection (within 0.5 units of target position)
   - Face performer continuously while watching
   - Legs reset to neutral stance when standing
   - Duration tracking with elapsed time check
   - Automatic watcher list cleanup on completion

5. **Performer Disappearance Handling**
   - Check if performer still exists before each update
   - Release watchers back to walking state if performer despawns
   - Null out watchingPerformer reference on release
   - Prevents orphaned pedestrians stuck in watching state

6. **Cross-System Protection**
   - Bus stop assignment excludes performer-watching pedestrians
   - Garbage truck suction skips towardPerformer and watchingPerformer states
   - Ensures crowds remain stable during performances
   - Pedestrians complete watching before other diversions

## Technical Decisions

### Decision: 15% Attraction Chance

**Context:** Need to balance crowd size growth with natural pedestrian flow.

**Chosen:** 15% chance to notice performer when setting new target

**Rationale:**
- 50 pedestrians × 15% = ~7.5 potential notices per target-setting cycle
- Not every notice results in watching (max crowd limit, distance)
- Creates gradual organic crowd growth
- Prevents sudden mob formation
- Maintains majority pedestrian flow continues normally

**Implementation:**
- Check occurs in setNewPedTarget before default sidewalk walking
- Only applies when state === 'walking' and performers exist
- Distance and crowd capacity further filter actual watchers

**Trade-offs:**
- Higher % = faster crowds but less realistic
- Lower % = slow growth, may not reach max crowd
- 15% balances discovery rate with natural appearance

---

### Decision: Semicircle Formation (144 degrees)

**Context:** Watching pedestrians need realistic spatial arrangement around performer.

**Chosen:** Position watchers in semicircle arc facing performer (0.8π spread)

**Rationale:**
- Real street performance crowds form semicircles, not full circles
- Pedestrians face performer, not each other
- 144 degrees (0.8π) provides wide viewing arc
- Leaves back/sides clear for performer "stage" area
- Watcher index determines unique position on arc

**Implementation:**
```javascript
const crowdAngle = performer.rotation.y + Math.PI; // Opposite performer facing
const angleSpread = Math.PI * 0.8; // 144 degree arc
const angleOffset = (watcherIndex / maxCrowd - 0.5) * angleSpread;
const watchAngle = crowdAngle + angleOffset;
```

**Trade-offs:**
- Full circle (2π) = surrounds performer but unrealistic
- Narrower arc = more crowded, less variety
- 144° balances realism with visual spacing

---

### Decision: Watch Duration 10-30 Seconds

**Context:** How long pedestrians observe performer before resuming walking.

**Chosen:** Random duration between 10-30 seconds per pedestrian

**Rationale:**
- 10s minimum = enough time to clearly see crowd formation
- 30s maximum = prevents static unchanging crowds
- Randomization creates natural turnover
- Matches real street performance attention spans (simplified)
- Different pedestrians leave at different times

**Implementation:**
- Set on attraction: `watchDuration = 10 + Math.random() * 20`
- Tracked via `watchStartTime` set on arrival
- Checked each frame: `t - watchStartTime > watchDuration`
- On completion: remove from watchers, resume walking

**Trade-offs:**
- Longer = more stable crowds but less dynamic
- Shorter = high turnover but harder to observe
- 10-30s balances visibility with dynamism

---

### Decision: Protect Watchers from Bus/Garbage Interruption

**Context:** Other city systems can disrupt crowd formation by assigning pedestrians.

**Chosen:** Filter out performer-watching pedestrians from bus and garbage truck systems

**Rationale:**
- Bus stop assignment would break crowd formation mid-watch
- Garbage truck suction would vacuum watching pedestrians
- Performers deserve stable audience for their duration
- Pedestrians can resume normal behavior after watching completes
- Cross-system coordination prevents visual glitches

**Implementation:**
- Bus: Added `!p.userData.watchingPerformer` to eligibility filter
- Garbage: Skip loop iteration for towardPerformer and watchingPerformer states
- Simple state checks prevent complex priority systems

**Trade-offs:**
- Watching pedestrians become "locked" temporarily
- Bus/garbage have smaller eligible pool
- Better visual coherence worth the constraint
- Alternative: priority system would be more complex

---

## Implementation Notes

### Semicircle Position Calculation

Watchers are positioned in front of performer based on rotation:

```javascript
// Performer faces rotation.y direction
// Crowd stands opposite (rotation.y + π)
const crowdAngle = performer.rotation.y + Math.PI;

// Spread 144° arc centered on performer's front
const angleSpread = Math.PI * 0.8;

// Watcher 0 at left edge, watcher 7 at right edge
const angleOffset = (watcherIndex / 8 - 0.5) * angleSpread;

// Final position 3 units from performer
const watchX = performer.x + sin(crowdAngle + angleOffset) * 3;
const watchZ = performer.z + cos(crowdAngle + angleOffset) * 3;
```

### State Machine Flow

```
walking
  ↓ (15% chance, performer nearby, crowd < max)
towardPerformer (walking animation)
  ↓ (distance < 0.5 units)
watchingPerformer (standing, facing performer)
  ↓ (elapsed > duration OR performer despawns)
walking (resume normal behavior)
```

### Performer Reference Tracking

- `p.userData.watchingPerformer` stores reference to performer object
- `performer.userData.watchers[]` array tracks all watching pedestrians
- Bidirectional tracking enables:
  - Pedestrian checks if performer still exists
  - Performer releases all watchers on despawn
  - Watcher removal from array on completion

### Cross-System Filtering

**Bus stop assignment:**
```javascript
const eligiblePeds = peds.filter(p =>
    p.userData.state === 'walking' &&
    !p.userData.waitingForBus &&
    !p.userData.watchingPerformer  // NEW
);
```

**Garbage truck suction:**
```javascript
for (let i = peds.length - 1; i >= 0; i--) {
    const ped = peds[i];
    if (!ped.visible) continue;
    // Skip watching/approaching performers
    if (ped.userData.state === 'watchingPerformer' ||
        ped.userData.state === 'towardPerformer') continue;
    // ... suction logic
}
```

## Deviations from Plan

None - plan executed exactly as written.

## Next Phase Readiness

**Phase 03 Complete**
- Street performer system fully functional with crowd interaction
- Pedestrians form realistic crowds around performers
- Organic discovery and watching behavior implemented
- Cross-system coordination prevents disruption
- No additional performer enhancements planned in current roadmap

**Blockers:** None

**Concerns:** None

**Ready to proceed:** Yes - Phase 03 complete, ready for Phase 04 (Subway System)

## Files Modified

### metropolis-3d-city-7.html
**Lines changed:** ~137 additions

**Changes:**
- Modified setNewPedTarget() to add performer attraction logic (lines 2014-2056, +43 lines)
- Added towardPerformer state handling in updPeds() (lines 6222-6263, +42 lines)
- Added watchingPerformer state handling in updPeds() (lines 6265-6303, +39 lines)
- Modified assignPedToStop() bus filter to exclude watching pedestrians (line 1424, +1 line)
- Modified garbage truck suction loop to skip watching pedestrians (lines 2692-2693, +3 lines)
- Modified updPerformers() watcher cleanup on despawn (existing, verified)

## Commits

| Commit | Message | Files |
|--------|---------|-------|
| b546853 | feat(03-02): add performer attraction logic to pedestrian targeting | metropolis-3d-city-7.html |
| 2a0f442 | feat(03-02): add performer watching states to pedestrian update logic | metropolis-3d-city-7.html |
| 5aca466 | feat(03-02): protect performer-watching pedestrians from interruption | metropolis-3d-city-7.html |

## Testing Notes

To verify implementation:

1. **Open metropolis-3d-city-7.html in browser**
2. **Wait for performer to spawn** (within 45 seconds)
3. **Observe pedestrian attraction:**
   - Nearby pedestrians stop and turn toward performer
   - Some pedestrians start walking toward performer
   - Not all pedestrians attracted (15% chance when retargeting)
4. **Verify semicircle formation:**
   - Watching pedestrians form arc in front of performer
   - Pedestrians face performer, not each other
   - Maximum 8 pedestrians watch simultaneously
   - Each pedestrian in unique position along arc
5. **Watch duration behavior:**
   - Pedestrians stand still watching for ~10-30 seconds
   - Different pedestrians leave at different times
   - Legs in neutral stance (not walking animation)
6. **Crowd turnover:**
   - As some pedestrians leave, new ones may join
   - Crowd size fluctuates naturally over time
   - Semicircle positions reassigned as watchers change
7. **Performer despawn handling:**
   - When performer disappears, all watchers resume walking
   - No orphaned pedestrians stuck in watching pose
8. **System protection:**
   - Watching pedestrians not assigned to bus stops
   - Garbage truck suction doesn't vacuum watchers
   - Crowds remain stable during performances

**Visual Checks:**
- Semicircle arc clearly visible (not full circle)
- Pedestrians face performer (rotation matches direction)
- 3-unit distance maintained from performer
- Smooth walking animation approaching performer
- Clean transition to standing still when watching
- Natural crowd growth and turnover over time

**Behavioral Checks:**
- Not all pedestrians attracted (15% rate observable)
- Max crowd limit enforced (never more than 8 watchers)
- Watch duration varies per pedestrian (staggered departures)
- Performer with no nearby pedestrians has empty crowd
- High-traffic sidewalks generate larger crowds faster

## Performance Impact

**New state tracking:**
- 2 new pedestrian states (towardPerformer, watchingPerformer)
- 3 new userData properties per pedestrian: watchingPerformer, watchDuration, watchStartTime
- Minimal memory overhead (references + 2 numbers)

**Per-frame computation:**
- Attraction check: only when pedestrian sets new target (infrequent)
- Distance calculations: only for nearby performers (max 3)
- State handling: ~10 operations per watching pedestrian
- Maximum ~80 operations (8 watchers × 10 ops)
- Negligible performance impact

**Added filtering:**
- Bus stop assignment: one additional filter condition
- Garbage truck: one state check per pedestrian
- No measurable performance change

## Knowledge for Future Phases

### Pattern: Cross-System State Coordination

When adding new pedestrian diversions (subway, rooftop access, etc.):

**Remember to filter out performer-watching pedestrians:**
```javascript
// When selecting eligible pedestrians
const eligible = peds.filter(p =>
    p.userData.state === 'walking' &&
    !p.userData.watchingPerformer &&
    // ... other conditions
);
```

**Or skip in loops:**
```javascript
for (const ped of peds) {
    if (ped.userData.state === 'watchingPerformer' ||
        ped.userData.state === 'towardPerformer') continue;
    // ... process pedestrian
}
```

### Pattern: Bidirectional Entity Tracking

Performers track watchers, watchers reference performer:

**Benefits:**
- Performer can release watchers on despawn
- Watchers can check if performer still exists
- Easy cleanup from both directions

**Cleanup considerations:**
- Always check `performers.includes(performer)` before using reference
- Remove from watcher array with `indexOf` + `splice`
- Null out references to prevent memory leaks

### Pattern: Spatial Arrangement Around Entity

Semicircle formation pattern reusable for:
- Ice cream truck customer queues
- Subway entrance crowds
- Building entrance gatherings

**Formula:**
```javascript
const baseAngle = entity.rotation.y + offset; // Direction to face
const spread = Math.PI * factor; // Arc width (0.8 for semicircle)
const index = entity.userData.crowd.length;
const angleOffset = (index / maxCrowd - 0.5) * spread;
const finalAngle = baseAngle + angleOffset;
const x = entity.x + sin(finalAngle) * radius;
const z = entity.z + cos(finalAngle) * radius;
```

### Future Enhancement Ideas

**Quality-based crowd size:**
- Add `performer.userData.quality` (poor, good, amazing)
- Adjust attractRadius and maxCrowd based on quality
- Better performers draw larger crowds from farther away

**Tipping behavior:**
- Some leaving watchers walk to tip jar
- Drop coin animation (small yellow sphere)
- Tip jar fills over time, visual feedback

**Performer reactions:**
- Bow when crowd reaches max capacity
- Wave when crowd disperses
- Adjust animation intensity based on crowd size

**Crowd density visualization:**
- Watchers arrive closer/farther based on crowd size
- Early arrivals get front positions, latecomers in back
- Multi-row semicircle for crowds exceeding single arc

**Applause animation:**
- When watch duration ends, brief clap animation
- Hands move together/apart before leaving
- Audio trigger point (if audio added later)

---

**Summary created:** 2026-01-24
**Phase status:** Complete (2/2 plans complete)
**Next phase:** 04-subway-system (Phase 4 - Subway Entrances and Transit)
