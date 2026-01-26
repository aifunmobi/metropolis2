---
phase: quick-001
plan: 01
type: execute
wave: 1
depends_on: []
files_modified: [metropolis-3d-city-7.html]
autonomous: true

must_haves:
  truths:
    - "Road from Metropolis continues straight as Vegas Strip (not T-intersection)"
    - "Vegas hotel buildings have visible windows with flickering lights"
    - "HUD temperature display is stable (not flickering every frame)"
  artifacts:
    - path: "metropolis-3d-city-7.html"
      provides: "Fixed Strip layout, hotel windows, stable HUD"
      contains: "vegasTemperature"
  key_links:
    - from: "mkExcaliburCastle"
      to: "window meshes"
      via: "window grid creation"
      pattern: "windowMat|emissive"
---

<objective>
Fix three Vegas zone issues: 1) Reorient Strip to continue straight from highway, 2) Add flickering windows to hotel landmarks, 3) Fix HUD temperature flicker bug.

Purpose: Vegas zone currently has layout, visual, and UI bugs that break immersion
Output: Working Vegas zone with correct road layout, lit hotels, and stable HUD
</objective>

<context>
@.planning/STATE.md
@metropolis-3d-city-7.html
</context>

<tasks>

<task type="auto">
  <name>Task 1: Fix HUD Temperature Flicker</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
The updateWeatherUI() function (line ~8493) has a bug: it calls `Math.random()` every frame when in Vegas, causing temperature to flicker crazily.

Fix by:
1. Add a global variable near vegasWeatherState (around line 192-199):
   ```javascript
   let vegasTemperature = 95 + Math.floor(Math.random() * 20); // Initial random temp
   let vegasTemperatureTimer = 0;
   ```

2. In updateWeatherUI() (line ~8493), replace the Vegas display logic:
   ```javascript
   if (inVegas) {
       // Vegas always shows sunny and hot - use stable temperature
       weatherEl.textContent = '\u2600\ufe0f Sunny ' + vegasTemperature + '\u00b0F';
   }
   ```

3. Add temperature update logic in updWeather() (after line ~8270) to change temperature slowly:
   ```javascript
   // Update Vegas temperature slowly (every 30 seconds)
   vegasTemperatureTimer += 0.016;
   if (vegasTemperatureTimer > 30) {
       vegasTemperature = Math.max(90, Math.min(115, vegasTemperature + Math.floor(Math.random() * 5) - 2));
       vegasTemperatureTimer = 0;
   }
   ```

This caches the temperature and only updates it every 30 seconds instead of every frame.
  </action>
  <verify>
Load page, fly to Vegas zone. Observe HUD - temperature should be stable (e.g., "Sunny 102F") and only change occasionally, not flickering every frame.
  </verify>
  <done>HUD temperature is stable in Vegas zone, changes only every 30 seconds</done>
</task>

<task type="auto">
  <name>Task 2: Add Windows to Vegas Hotels</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Vegas landmarks are solid blocks without windows. Add illuminated windows with flickering capability.

Create a helper function after the landmark functions (around line 1782):
```javascript
function addHotelWindows(building, width, height, depth, color = 0xffffcc) {
    // Add windows to a building face
    const windowMat = new THREE.MeshStandardMaterial({
        color: color,
        emissive: color,
        emissiveIntensity: 0.3
    });

    const windowSize = 0.8;
    const windowSpacing = 2;

    // Front and back faces
    for (const zSide of [1, -1]) {
        const cols = Math.floor(width / windowSpacing) - 1;
        const rows = Math.floor(height / windowSpacing) - 1;

        for (let c = 0; c < cols; c++) {
            for (let r = 0; r < rows; r++) {
                if (Math.random() > 0.3) { // 70% windows lit
                    const win = new THREE.Mesh(
                        new THREE.PlaneGeometry(windowSize, windowSize),
                        windowMat.clone()
                    );
                    win.position.set(
                        -width/2 + windowSpacing + c * windowSpacing,
                        windowSpacing + r * windowSpacing,
                        zSide * depth/2 + zSide * 0.05
                    );
                    if (zSide < 0) win.rotation.y = Math.PI;
                    win.userData.isVegasWindow = true;
                    building.add(win);
                }
            }
        }
    }
}
```

Modify landmark functions to add windows:

1. **mkExcaliburCastle()**: After creating mainBody (line ~1657), add:
   ```javascript
   // Add windows to main castle body
   addHotelWindows(castle, 30, 12, 16, 0xffffaa);
   ```

2. **mkBellagio()**: After creating the main building sections, add windows to the tower.

3. **mkCaesarsPalace()**: After creating the main building, add windows.

4. Add vegasWindows tracking array near vegasLandmarks:
   ```javascript
   let vegasWindows = [];
   ```

5. Modify addHotelWindows to track windows:
   ```javascript
   vegasWindows.push(win);
   ```

6. Add updVegasWindows() function to animate window flickering:
   ```javascript
   function updVegasWindows() {
       vegasWindows.forEach(win => {
           if (Math.random() < 0.001) { // Occasional flicker
               const mat = win.material;
               const lit = Math.random() > 0.3;
               mat.emissiveIntensity = lit ? 0.3 + Math.random() * 0.2 : 0;
           }
       });
   }
   ```

7. Call updVegasWindows() in the animate loop after updWindowLights().

Note: Focus on Excalibur and Bellagio (the hotel-shaped buildings) as they have clear window-compatible facades. Luxor (pyramid), Paris (tower), and Caesars (columns) are architectural shapes where windows don't make as much sense.
  </action>
  <verify>
Load page, fly to Vegas at night (press T to speed up time). Excalibur castle and Bellagio hotel should show lit windows with occasional subtle flickering.
  </verify>
  <done>Vegas hotels have visible windows with subtle flickering animation</done>
</task>

<task type="auto">
  <name>Task 3: Reorient Strip to Continue Straight from Highway</name>
  <files>metropolis-3d-city-7.html</files>
  <action>
Currently the Strip runs north-south (perpendicular to highway) creating a T-intersection. User wants highway to continue straight into Vegas as the main Strip road, with hotels on the sides.

Modify mkTheStrip() function (line ~744):

1. Change Strip orientation from north-south (Z-axis) to east-west (X-axis):
   - Strip should continue along X-axis from highway end
   - stripStartX becomes the start of Strip, not the center
   - Road runs along X instead of along Z

2. Update road geometry:
   ```javascript
   // Strip continues straight from highway (along X axis)
   const stripStartX = VEGAS_CFG.zoneStartX + VEGAS_CFG.highwayLength;
   const stripCenterZ = 0;

   // Main road - now runs along X axis (east-west)
   const stripRoad = new THREE.Mesh(
       new THREE.PlaneGeometry(VEGAS_CFG.stripLength, VEGAS_CFG.stripWidth),
       roadMat
   );
   stripRoad.rotation.x = -Math.PI / 2;
   stripRoad.position.set(stripStartX + VEGAS_CFG.stripLength/2, 0.02, stripCenterZ);
   ```

3. Update lane markings to run along X:
   ```javascript
   // Center lines now run along X
   const centerLine = new THREE.Mesh(
       new THREE.PlaneGeometry(VEGAS_CFG.stripLength - 4, 0.15),
       yellowMat
   );
   centerLine.position.set(stripStartX + VEGAS_CFG.stripLength/2, 0.025, offset);
   ```

4. Update sidewalks to be on north and south sides (along Z):
   ```javascript
   // Sidewalks on north and south sides of Strip
   const sidewalk = new THREE.Mesh(
       new THREE.PlaneGeometry(VEGAS_CFG.stripLength, sidewalkWidth),
       sidewalkMat
   );
   sidewalk.position.set(
       stripStartX + VEGAS_CFG.stripLength/2,
       0.015,
       side * (VEGAS_CFG.stripWidth / 2 + sidewalkWidth / 2)
   );
   ```

5. Update parking lots to be on north and south sides:
   ```javascript
   const lot = new THREE.Mesh(
       new THREE.PlaneGeometry(VEGAS_CFG.stripLength + 20, lotWidth),
       lotMat
   );
   lot.position.set(
       stripStartX + VEGAS_CFG.stripLength/2,
       0.005,
       side * (VEGAS_CFG.stripWidth / 2 + sidewalkWidth + lotWidth / 2)
   );
   ```

6. Remove T-intersection (no longer needed - it's now a straight continuation).

7. Update userData to reflect new orientation:
   ```javascript
   strip.userData = {
       centerZ: stripCenterZ,
       startX: stripStartX,
       endX: stripStartX + VEGAS_CFG.stripLength,
       width: VEGAS_CFG.stripWidth,
       sidewalkWidth: sidewalkWidth
   };
   ```

8. Update landmark positioning functions (mkLuxorPyramid, mkParisEiffelTower, mkBellagio, mkCaesarsPalace, mkExcaliburCastle) to place hotels on NORTH and SOUTH sides of the Strip (along Z axis) instead of WEST and EAST:
   - Hotels that were west of Strip -> now north of Strip (negative Z)
   - Hotels that were east of Strip -> now south of Strip (positive Z)
   - Position along Strip length (X axis) at various points

For each landmark, change from:
```javascript
stripCenterX - stripWidth / 2 - sidewalkWidth - offset  // West side
```
to:
```javascript
stripStartX + stripLength * fraction  // Position along X
stripCenterZ - stripWidth / 2 - sidewalkWidth - offset  // North side
```
  </action>
  <verify>
1. Load page, fly from Metropolis along highway toward Vegas
2. Highway should continue straight as the Vegas Strip road
3. Hotels should be visible on BOTH SIDES (north and south) of the Strip
4. No T-intersection - road continues straight
5. Can drive/fly straight from Metropolis into and through Vegas
  </verify>
  <done>Strip continues straight from highway with hotels on both sides, no T-intersection</done>
</task>

</tasks>

<verification>
1. HUD stable: Fly to Vegas, watch temperature - should be steady, changing only occasionally
2. Windows visible: Fly around Vegas hotels at night - Excalibur and Bellagio show lit windows
3. Strip layout: Fly from Metropolis to Vegas - road continues straight, hotels on sides
4. No console errors
</verification>

<success_criteria>
- HUD temperature stable in Vegas (no per-frame flickering)
- Vegas hotels have visible windows with occasional flicker animation
- Strip road continues straight from highway (not perpendicular T-intersection)
- Hotels positioned on north/south sides of the east-west Strip
</success_criteria>

<output>
After completion, update .planning/STATE.md with fixes applied
</output>
