---
phase: quick
plan: 002
type: execute
wave: 1
depends_on: []
files_modified: [metropolis-3d-city-7.html]
autonomous: true

must_haves:
  truths:
    - "Vegas hotels are visibly larger than current (2-3x scale increase)"
    - "Hotels have many illuminated windows like Metropolis buildings"
    - "Welcome to Fabulous Las Vegas sign visible at Vegas entrance"
    - "Sign has animated chase lights around perimeter"
  artifacts:
    - path: "metropolis-3d-city-7.html"
      provides: "Scaled up Vegas landmarks, enhanced windows, Welcome sign"
      contains: "mkWelcomeSign"
  key_links:
    - from: "mkWelcomeSign()"
      to: "scene"
      via: "scene.add"
      pattern: "scene\\.add.*welcomeSign"
---

<objective>
Scale up Vegas hotels significantly (2-3x), add many more windows matching Metropolis style, and create the iconic "Welcome to Fabulous Las Vegas" sign at the Vegas entrance.

Purpose: Make Vegas feel like Vegas - massive hotels with endless lit windows, and the famous diamond-shaped welcome sign greeting arrivals.
Output: Larger landmarks, dense window grids on all hotel buildings, animated welcome sign.
</objective>

<execution_context>
@/Users/peter/.claude/get-shit-done/workflows/execute-plan.md
@/Users/peter/.claude/get-shit-done/templates/summary.md
</execution_context>

<context>
@.planning/STATE.md
@metropolis-3d-city-7.html (lines 1017-1830 for landmark functions)
</context>

<tasks>

<task type="auto">
  <name>Task 1: Scale up Vegas hotels significantly</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Increase the size of all Vegas landmarks by approximately 2-3x to create real Vegas hotel scale:

1. **mkLuxorPyramid()** (~line 1017):
   - pyramidHeight: 30 -> 75 (2.5x)
   - pyramidBaseWidth: 25 -> 60 (2.4x)
   - base: 27 -> 65 (BoxGeometry)
   - sphinx: scale proportionally (body 6x3x4, head 2x2.4x2)
   - sphinx position: adjust to 38 units in front
   - Position offset: increase Z offset from 18 to 45 for parking lot

2. **mkParisEiffelTower()** (~line 1097):
   - foundation: 15 -> 35 (BoxGeometry)
   - legHeight: 12 -> 30, legSpread: 5 -> 12, legTopSpread: 2 -> 5
   - deck1 radius: 4 -> 10
   - middleHeight: 12 -> 30, middleSection radii: 1.2->3, 2.2->5.5
   - deck2 radius: 3 -> 7.5
   - spireHeight: 10 -> 25, spire radii: 0.2->0.5, 0.6->1.5
   - antenna: scale 1.5x (0.075/0.15 radii, 4.5 height)
   - Position offset: increase Z offset from 12 to 30

3. **mkBellagio()** (~line 1232):
   - centerSection: 12x25x15 -> 30x65x35
   - wings: 10x25x15 -> 25x65x35, positions scale accordingly
   - accentBand: 32x1.5x16 -> 80x3x40
   - tower: 8x35x10 -> 20x90x25, position -10 -> -25
   - towerAccent: 9x1x11 -> 22x2x27
   - lakeWidth/Depth: 35x20 -> 90x50
   - Update addHotelWindows calls with new dimensions
   - Position offset: increase Z offset from 25 to 55

4. **mkCaesarsPalace()** (~line 1406):
   - main: 40x20x30 -> 100x50x75
   - columns: scale positions and dimensions (radius 1.25, height 25)
   - columnSpacing: 5 -> 12
   - capital/base: scale proportionally
   - pediment: scale to match new entrance (20 width, 5 height)
   - dome: radius 4 -> 10, position adjust
   - staircase: scale accordingly (30 width, 15 depth)
   - Position offset: increase Z offset from 25 to 55

5. **mkExcaliburCastle()** (~line 1586):
   - foundation: 40x2x22 -> 100x4x55
   - moat strips: scale proportionally
   - mainBody: 35x15x18 -> 90x40x45
   - battlements: adjust positions and scale
   - gate: 6x8 -> 15x20
   - turrets: radius 2.5->6, height 12->30, cone 3.5->8 radius, 5->12 height
   - centralTower: radius 3->7.5, height 20->50
   - spire: radius 4->10, height 6->15
   - Position offset: increase Z offset from 22 to 55

6. **Update parking lot width** in VEGAS_CFG (around line 278):
   - Current lotWidth in mkTheStrip is 30, increase to 70 for larger hotels
   - Or expand desert zone to accommodate larger footprints
  </action>
  <verify>
Open browser, fly to Vegas. Hotels should appear 2-3x larger than before. Pyramid should dominate the skyline. Eiffel Tower should be clearly taller. All hotels should still be positioned properly along the Strip without overlapping.
  </verify>
  <done>All 5 Vegas landmarks scaled up approximately 2.5x, properly positioned on enlarged parking lots.</done>
</task>

<task type="auto">
  <name>Task 2: Add dense window grids to all Vegas hotels</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Add window grids to all hotel buildings using the existing addHotelWindows() function pattern, and add windows to buildings that currently lack them (Caesars, Paris base):

1. **Enhance addHotelWindows()** (~line 1793):
   - Reduce windowSpacing from 2 to 1.5 for denser grid
   - Add side faces (left/right) in addition to front/back
   - Ensure windows are added to all 4 faces of rectangular buildings

2. **Add windows to all hotel sections**:
   - Bellagio: leftWing, rightWing (already has center and tower)
   - Caesars main building: add call to addHotelWindows()
   - Paris base building (if created): add windows
   - Luxor: Skip (pyramid shape doesn't suit windows)

3. **Update existing addHotelWindows calls** with scaled dimensions:
   - mkExcaliburCastle: mainBody windows (scaled dimensions)
   - mkBellagio: centerSection, tower, leftWing, rightWing windows
   - mkCaesarsPalace: main building windows

4. **Window colors**: Use warm 0xffffcc or 0xffeeaa (matching Metropolis windows)
  </action>
  <verify>
Fly around Vegas at night (press T to cycle time). All hotel buildings should have dense grids of lit windows on all visible faces. Windows should flicker occasionally (existing updVegasWindows handles this).
  </verify>
  <done>All rectangular Vegas hotel buildings have dense window grids on all 4 faces.</done>
</task>

<task type="auto">
  <name>Task 3: Create Welcome to Fabulous Las Vegas sign</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Create the iconic "Welcome to Fabulous Las Vegas Nevada" sign at the Vegas entrance:

1. **Create mkWelcomeSign() function** (add after mkTemperatureBillboard, ~line 980):

```javascript
function mkWelcomeSign() {
    const sign = new THREE.Group();

    // Diamond-shaped main sign (rotated square)
    // Real sign is ~25ft tall, scale to ~15 units for visibility
    const diamondSize = 10;
    const diamondMat = new THREE.MeshStandardMaterial({
        color: 0xcc0000,  // Red
        roughness: 0.5
    });

    // Main diamond shape using rotated box
    const diamond = new THREE.Mesh(
        new THREE.BoxGeometry(diamondSize, diamondSize, 0.5),
        diamondMat
    );
    diamond.rotation.z = Math.PI / 4; // Rotate 45 degrees
    diamond.position.y = 12;
    sign.add(diamond);

    // Inner diamond (slightly smaller, different color)
    const innerDiamond = new THREE.Mesh(
        new THREE.BoxGeometry(diamondSize * 0.8, diamondSize * 0.8, 0.6),
        new THREE.MeshStandardMaterial({ color: 0xffffff })
    );
    innerDiamond.rotation.z = Math.PI / 4;
    innerDiamond.position.y = 12;
    sign.add(innerDiamond);

    // Blue accent at bottom of diamond
    const blueAccent = new THREE.Mesh(
        new THREE.BoxGeometry(diamondSize * 0.6, diamondSize * 0.3, 0.7),
        new THREE.MeshStandardMaterial({ color: 0x0033aa })
    );
    blueAccent.position.y = 8;
    sign.add(blueAccent);

    // Canvas texture for text
    const canvas = document.createElement('canvas');
    canvas.width = 512;
    canvas.height = 512;
    const ctx = canvas.getContext('2d');

    // Draw sign text
    ctx.fillStyle = '#cc0000';
    ctx.fillRect(0, 0, 512, 512);
    ctx.fillStyle = '#ffffff';
    ctx.font = 'bold 40px serif';
    ctx.textAlign = 'center';
    ctx.fillText('WELCOME', 256, 120);
    ctx.font = 'italic 50px serif';
    ctx.fillText('to Fabulous', 256, 200);
    ctx.font = 'bold 80px serif';
    ctx.fillText('LAS VEGAS', 256, 310);
    ctx.font = 'bold 35px serif';
    ctx.fillText('NEVADA', 256, 380);

    const texture = new THREE.CanvasTexture(canvas);
    const textPlane = new THREE.Mesh(
        new THREE.PlaneGeometry(8, 8),
        new THREE.MeshBasicMaterial({ map: texture, transparent: true })
    );
    textPlane.position.set(0, 12, 0.4);
    sign.add(textPlane);

    // Back side
    const textPlaneBack = textPlane.clone();
    textPlaneBack.rotation.y = Math.PI;
    textPlaneBack.position.z = -0.4;
    sign.add(textPlaneBack);

    // Support poles
    const poleMat = new THREE.MeshStandardMaterial({ color: 0x888888 });
    for (const xOff of [-2, 2]) {
        const pole = new THREE.Mesh(
            new THREE.CylinderGeometry(0.2, 0.2, 8, 8),
            poleMat
        );
        pole.position.set(xOff, 4, 0);
        sign.add(pole);
    }

    // Circle medallion at top
    const circleMat = new THREE.MeshStandardMaterial({
        color: 0xffd700,
        metalness: 0.7
    });
    const circle = new THREE.Mesh(
        new THREE.CircleGeometry(1.5, 16),
        circleMat
    );
    circle.position.set(0, 19, 0.3);
    sign.add(circle);

    // Star in circle
    // (simplified - just a yellow sphere for now)

    // Chase lights around perimeter (12-16 bulbs)
    const lights = [];
    const bulbGeo = new THREE.SphereGeometry(0.2, 8, 8);
    const bulbMatOn = new THREE.MeshBasicMaterial({ color: 0xffff00 });
    const bulbMatOff = new THREE.MeshBasicMaterial({ color: 0x444400 });

    // Position bulbs around diamond perimeter
    const numBulbs = 16;
    for (let i = 0; i < numBulbs; i++) {
        const angle = (i / numBulbs) * Math.PI * 2 - Math.PI/4;
        const radius = diamondSize * 0.6;
        const bulb = new THREE.Mesh(bulbGeo, bulbMatOn.clone());
        bulb.position.set(
            Math.cos(angle) * radius,
            12 + Math.sin(angle) * radius,
            0.5
        );
        bulb.userData.lightIndex = i;
        lights.push(bulb);
        sign.add(bulb);
    }

    sign.userData.lights = lights;
    sign.userData.chasePhase = 0;

    // Position at Vegas entrance (where highway meets Strip)
    const stripStartX = theStrip.userData.startX;
    sign.position.set(
        stripStartX - 10, // Just before Strip starts
        0,
        12 // South side of road, visible when approaching
    );

    scene.add(sign);
    return sign;
}
```

2. **Add global variable** for welcome sign (near line 195):
```javascript
let welcomeSign = null;
```

3. **Call mkWelcomeSign() in init()** (after mkTemperatureBillboard, ~line 324):
```javascript
welcomeSign = mkWelcomeSign();
```

4. **Add updWelcomeSign() for chase light animation**:
```javascript
function updWelcomeSign() {
    if (!welcomeSign) return;
    const lights = welcomeSign.userData.lights;
    welcomeSign.userData.chasePhase += 0.1;

    lights.forEach((bulb, i) => {
        const phase = (welcomeSign.userData.chasePhase + i * 0.5) % (Math.PI * 2);
        const brightness = Math.sin(phase) > 0.3 ? 1 : 0.2;
        bulb.material.color.setHex(brightness > 0.5 ? 0xffff00 : 0x444400);
    });
}
```

5. **Call updWelcomeSign() in animate()** (in main loop, ~line 4050):
```javascript
updWelcomeSign();
```
  </action>
  <verify>
Fly from Metropolis toward Vegas on Route 66. The Welcome sign should be visible at the Vegas entrance. Chase lights should animate around the diamond perimeter. Sign text should be readable when close.
  </verify>
  <done>Welcome to Fabulous Las Vegas sign positioned at Vegas entrance with animated chase lights.</done>
</task>

</tasks>

<verification>
1. Fly from Metropolis through Vegas - all hotels visibly larger
2. At night (T key), see dense window grids on all hotel faces
3. Welcome sign visible at Vegas entrance with working chase lights
4. No overlapping landmarks, proper spacing maintained
5. Console: `vegasWindows.length` should be significantly larger than before
</verification>

<success_criteria>
- All 5 Vegas hotels scaled up 2-3x
- Dense window grids on Bellagio, Caesars, Excalibur (all faces)
- Welcome to Fabulous Las Vegas sign at Vegas entrance
- Chase lights animate on welcome sign
- No visual overlaps or positioning issues
</success_criteria>

<output>
After completion, create `.planning/quick/002-vegas-hotels-larger-many-windows-welcome/002-SUMMARY.md`
</output>
