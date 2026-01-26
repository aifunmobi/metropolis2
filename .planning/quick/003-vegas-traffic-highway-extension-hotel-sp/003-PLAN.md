---
phase: quick-003
plan: 01
type: execute
wave: 1
depends_on: []
files_modified: [metropolis-3d-city-7.html]
autonomous: true

must_haves:
  truths:
    - "Cars travel on highway between Metropolis and Vegas in both directions"
    - "Highway continues past Vegas into the distance"
    - "Vegas hotels are spread apart like real Vegas Strip"
  artifacts:
    - path: "metropolis-3d-city-7.html"
      provides: "Highway traffic, extended highway, spread hotels"
      contains: "mkHighwayCars|highwayCars|stripLength.*140"
  key_links:
    - from: "mkHighwayCars()"
      to: "animate loop"
      via: "updHighwayCars() call"
      pattern: "updHighwayCars"
---

<objective>
Vegas improvements: Add highway traffic between Metropolis and Vegas, extend highway past Vegas into distance, spread hotels further apart on The Strip.

Purpose: Make the Vegas connection feel alive with traffic and give Vegas the expansive real-Strip feel with hotels spread along a longer road.
Output: Highway with bidirectional traffic, road continuing into desert horizon, hotels with realistic Vegas spacing.
</objective>

<execution_context>
@/Users/peter/.claude/get-shit-done/workflows/execute-plan.md
@/Users/peter/.claude/get-shit-done/templates/summary.md
</execution_context>

<context>
@metropolis-3d-city-7.html

Key existing code:
- VEGAS_CFG at line ~278: zoneStartX, stripLength (70), highwayLength (100)
- mkVegasHighway() at line ~597: Creates highway from Metropolis to Vegas
- mkTheStrip() at line ~749: Creates Strip road, stores userData.startX/endX
- mkLuxorPyramid(), mkParisEiffelTower(), mkBellagio(), mkCaesarsPalace(), mkExcaliburCastle(): Position hotels using stripLength fractions (0.15, 0.3, 0.4, 0.5, 0.65)
- placeCarOnRoad() at line ~5833: Places cars on Metropolis city roads only
- cars[] array and updCars() for car movement
</context>

<tasks>

<task type="auto">
  <name>Task 1: Highway traffic system</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Create highway traffic that travels between Metropolis and Vegas:

1. Add global array `highwayCars = []` near other vehicle arrays (~line 182)

2. Create `mkHighwayCars()` function (after mkVegasHighway):
   - Spawn 6-8 highway cars using existing mkCar() with random colors
   - For each car:
     - 50% chance eastbound (toward Vegas), 50% westbound (toward Metropolis)
     - Position on highway (Y=0, Z=0 for center with lane offsets +2.5/-2.5 for each direction)
     - X position spread along highway length
     - Set userData: isHighwayCar=true, highwayDir (1 or -1), highwaySpeed (0.3-0.4, faster than city cars)
     - Rotation: dir=1 faces east (rotation.y=0), dir=-1 faces west (rotation.y=PI)
   - Push to highwayCars[] and scene.add()

3. Create `updHighwayCars()` function:
   - For each highway car:
     - Move: car.position.x += car.userData.highwayDir * car.userData.highwaySpeed
     - Wrap around:
       - If eastbound and x > VEGAS_CFG.zoneStartX + VEGAS_CFG.highwayLength + VEGAS_CFG.stripLength + 50: reset to halfSize - 10
       - If westbound and x < halfSize - 10: reset to VEGAS_CFG.zoneStartX + VEGAS_CFG.highwayLength + VEGAS_CFG.stripLength + 50

4. Call mkHighwayCars() in init() after mkVegasHighway() call (~line 321)

5. Call updHighwayCars() in animate() loop, add to vehicle updates section (~line 9510)
  </action>
  <verify>Open in browser, observe cars traveling on highway in both directions between Metropolis and Vegas</verify>
  <done>Highway has 6-8 cars traveling both directions, wrapping around when they reach ends</done>
</task>

<task type="auto">
  <name>Task 2: Extend highway past Vegas and spread hotels</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Extend highway and double Strip length for hotel spacing:

1. Update VEGAS_CFG (~line 278):
   - Change stripLength from 70 to 140 (double the length for real Vegas spacing)
   - Add highwayExtension: 80 (road continuing past Vegas into distance)

2. Modify mkVegasHighway() to extend past Vegas:
   After existing highway code, add extension segment:
   - Create continuation road from Strip end to Strip end + highwayExtension
   - Same width (VEGAS_CFG.highwayWidth), same materials
   - Dashed center line and edge lines continuing
   - Desert strips on both sides extending with it
   - Road can fade: either keep solid or add fog-like gradient at far end (simpler: just let scene fog handle it)

3. Extend desert ground in mkVegasZoneGround():
   - Increase vegasGroundWidth calculation to include highwayExtension
   - This ensures desert terrain covers the extended highway area

4. Hotel positions automatically adjust (they use stripLength fractions):
   - Luxor at 0.15 * 140 = 21 units from start
   - Caesars at 0.3 * 140 = 42 units from start
   - Excalibur at 0.4 * 140 = 56 units from start
   - Paris at 0.5 * 140 = 70 units from start
   - Bellagio at 0.65 * 140 = 91 units from start

   This spreads them out nicely along the longer Strip with ~14-21 unit gaps between them.

5. Adjust Welcome sign position if needed (currently at stripStartX - 12, should still work)

6. Adjust temperature billboard position if needed (currently at stripStartX + 5)
  </action>
  <verify>Open in browser, verify: 1) Highway continues past Vegas into distance, 2) Hotels are visibly more spread out along Strip, 3) Desert terrain extends to cover new road</verify>
  <done>Highway extends 80 units past Vegas, Strip is 140 units long with hotels spread ~15-20 units apart</done>
</task>

</tasks>

<verification>
- [ ] Highway has cars traveling in both directions
- [ ] Cars wrap around at highway ends (continuous traffic)
- [ ] Highway continues past Vegas Strip into the desert distance
- [ ] Hotels are spread apart with visible gaps between them
- [ ] Desert terrain covers all road areas
- [ ] No console errors
</verification>

<success_criteria>
1. Highway traffic: 6-8 cars traveling bidirectionally on highway
2. Extended highway: Road continues 80+ units past Vegas into distance
3. Hotel spacing: Strip doubled to 140 units, hotels have 15-20 unit gaps
4. All existing Vegas features (landmarks, welcome sign, billboard) still functional
</success_criteria>

<output>
After completion, create `.planning/quick/003-vegas-traffic-highway-extension-hotel-sp/003-SUMMARY.md`
</output>
