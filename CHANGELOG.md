# Changelog — FTL Impossibility Visualizer

All changes from the February 2026 build session.

---

## 26. Tractor-Beam Force Visualization
**Prompt:** "Add gravitational force visualization to the 3D Spacetime view — tractor beam visual design with color gradients, force magnitude visualization, per-mass colored beams, educational features."

**Changes:**
- Rewrote `updateForceVectors()` from simple red ArrowHelper arrows to rich tractor-beam visualization
- Added reusable `beamGeo` (CylinderGeometry) and `coneGeo` (ConeGeometry) shared across all beams
- Per-mass beam coloring via `massBeamColor(m)`: purple for black holes, gold for stars/sun, blue for planets
- Force-strength color gradient via `forceColor(baseCol, strength)`: blends source color → orange/red at high force
- Beam thickness proportional to force: 0.03 (weak) → 0.25 (strong)
- Beam opacity proportional to force: 0.15 (dim) → 0.7 (bright)
- Gentle pulsing animation via `forcePulsePhase` (sinusoidal, per-particle/per-mass offset)
- Glow halo: wider, more transparent cylinder layered behind each beam
- Arrowhead cone at 82% along beam, pointing toward the attracting mass
- Net force: white ArrowHelper showing combined force when multiple masses present
- Force info row in top-right overlay: "Force ∝ 1/r²" label + peak force magnitude (red)
- Context-sensitive: force info row shown/hidden based on Show Forces toggle state
- **Commit:** (pending)

---

## 25. Camera Default Mode — Fix Accidental Mass Placement
**Prompt:** "Fix the accidental mass placement issue — separate camera controls from object placement. Default behavior should NEVER place objects."

**Changes:**
- Default mode changed from `place` to `camera` — clicking only controls the camera (OrbitControls)
- Added Camera button to mode group (active by default, green highlight)
- Place Mass, Drop Particle, Launch Orbit are now explicit opt-in toggles
- Clicking an already-active mode button toggles back to Camera (radio behavior)
- Mode indicator overlay (bottom-right of 3D container): color-coded by mode
  - Green "Camera Controls" (default)
  - Yellow "Click to Place Mass"
  - Blue "Click to Drop Particle"
  - Purple "Click to Launch Orbit"
- Container border glow (inset box-shadow) when in any action mode
- Keyboard shortcuts: M = toggle Place Mass, P = toggle Drop Particle, O = toggle Launch Orbit, Esc = Camera
  - Only active when curvature section is in viewport
  - Ignored when typing in input fields
- Rain mode fires immediately then auto-returns to Camera
- Presets, scenarios, Reset All, and Clear All all return to Camera mode
- Default cursor changed from `crosshair` to `grab`
- Mode button tooltips show keyboard shortcuts
- **Commit:** `5e0ee88`

---

## 24. Curvature UI Reorganization: Bottom Control Panel
**Prompt:** "Reorganize the 3D Spacetime Curvature interface for better usability: Move ALL controls to the bottom, consolidate into organized sections (Quick Start, Simulation, Advanced), add collapsible sections, context-sensitive controls, compact info display, enhanced fullscreen, responsive design."

**Changes:**
- Moved 3D container to top of section (70-80% of space), controls to bottom panel
- 3-column control panel layout: Quick Start | Simulation | Advanced
  - **Quick Start** (always visible): mass presets (Earth/Sun/Black Hole/Binary) + scenario buttons (ISS/Moon/Earth-Sun/Binary/Figure-8)
  - **Simulation** (always visible): Pause/Step+1/Reset, sim speed slider, 2-column checkbox grid (Grid, Trails, Cross-Sections, Forces, Geodesics)
  - **Advanced** (collapsible ▼/▶): view toggle, camera buttons, mode buttons, mass/launch/inclination sliders, orbital presets, Clear All, Fullscreen
- Collapsible **Help** section with camera, shell legend, and mode explanations
- Compact **info overlay** (top-right of 3D view): scenario name, elapsed time, time dilation, energy drift
- **Context-sensitive controls** (5Hz setInterval):
  - Launch speed slider: visible only in orbit/orbits mode
  - Follow camera button: visible only when movable bodies exist
  - Step+1: grayed out when simulation is playing
  - Mass strength slider: hidden during preset scenarios
- **Enhanced fullscreen**: H key toggles control panel visibility (CSS fixed overlay at bottom), ESC exits + cleans up
- Fullscreen instructions updated to mention H key
- Scenario descriptions moved to button `title` tooltips
- Tooltip repositioned to top-center (avoids overlapping info overlay)
- Replaced ~180 lines of inline-styled control rows with comprehensive CSS layout
- Responsive: columns stack on ≤900px, compact sizing on ≤600px
- All 58 element IDs preserved — zero JS modifications to existing event handlers
- **Commit:** (pending)

---

## 23. Physics Rewrite: Velocity-Verlet Integrator
**Prompt:** "The orbital physics simulation is fundamentally broken - all orbits are wrong. Complete rewrite needed: Fix core gravitational physics, use proper physics integrator (velocity-Verlet or RK4), verify circular orbit calculations, add energy conservation check, step-by-step debugging mode."

**Changes:**
- Replaced position-Verlet integrator with velocity-Verlet (symplectic, energy-conserving)
- **Root cause**: old integrator encoded velocity implicitly as `(x - prevX)/dt`; variable sub-step sizes between frames corrupted velocity, causing energy drift and spiral orbits
- Fixed sub-step size `PHYSICS_DT = 0.004` — consistent integration regardless of frame rate
- New `gravAccel(px, py, pz)` helper computes gravitational acceleration at any point (with soft minimum radius 0.15 to prevent singularity)
- New `computeTotalEnergy()` tracks kinetic + potential energy for conservation monitoring
- Explicit velocity storage on particles (`vx`, `vy`, `vz`) — removed all `prevX`/`prevY`/`prevZ` fields
- Rewrote `stepParticles(dt)`: half-step velocity → full-step position → recompute acceleration → half-step velocity
- Rewrote `stepDynamicMasses(dt)` with same velocity-Verlet pattern and new `massAccel(m)` helper
- Added energy drift readout with color coding (green <0.01%, yellow <0.1%, red >0.1%)
- Added Step Forward button for single-frame debugging while paused
- Removed orphaned `VERLET_DT` constant
- **Commit:** `fc4585f`

---

## 22. 3D Curvature Polish: Labels, Legend, Axes, Camera Help
**Prompt:** "Fix multiple issues with the 3D Spacetime Curvature visualization: Label ALL objects, explain the spherical wireframes, fix Moon orbit preset, improve axis labels, add camera controls explanation, fix all preset scenarios, add visual clarity."

**Changes:**
- Added labels to all default presets (Earth, Sun, Black Hole, Star A/B) via `label` property in PRESETS object
- Added wireframe shell legend overlay explaining inner/outer shells and color coding
- Improved axis labels: bigger text (16px), arrowhead cones at positive ends
- Added camera help overlay ("Drag: Rotate | Right-drag: Pan | Scroll: Zoom")
- Added time elapsed readout (seconds/minutes/hours format), reset on scenario change
- Increased trail opacity from 0.35 to 0.55
- Reduced Moon preset sim speed from 2.0 to 1.0
- **Commit:** `bd43d59` (combined with landing page)

---

## 21. Netflix-Style Landing Page
**Prompt:** "Transform the website into a modern educational platform with: full-viewport Netflix-style landing page, interactive module cards, progress tracking, sticky navigation."

**Changes:**
- Full-viewport hero with progress bar ("X / 12 modules") and bouncing scroll hint chevron
- 12 module cards in responsive CSS grid (3-column desktop, 1-column mobile)
  - Each card: emoji icon thumbnail, section number, difficulty badge, title, description, visited status dot
  - Hover: lift -6px with blue glow, opacity transition
- Progress tracking via IntersectionObserver: sections marked "visited" after 2-second dwell at 25% visibility
- localStorage persistence (`ftl-visited-sections` key) — visited state restored across sessions
- Sticky navigation bar: appears when scrolling past module grid, backdrop-blur glass effect
  - 12 section buttons with horizontal scroll, mini progress bar with percentage
  - Highlights current section via IntersectionObserver
- Smooth scroll: card/nav clicks scroll to section with `scroll-margin-top: 60px` offset
- Keyboard accessible: cards focusable with Enter/Space activation
- **Commit:** `bd43d59`

---

## 20. 3D Centering Fix: Masses at Center of Spherical Grid
**Prompt:** (continuation from prior session — fix 3D visualization)

**Changes:**
- Modified `updateMassPositions()`: masses use Y=0 in 3D mode (center of spherical shells) instead of sitting on deformed surface
- Added 3D axis labels: X (red), Y (green), Z (blue) dashed lines with projected HTML labels
- Arrowheads on axis positive ends
- Added Front camera preset button (camera at (50, 0, 0))
- Removed polar angle constraint (`maxPolarAngle = Math.PI`) — full orbit freedom
- Added omnidirectional gravity hint div in 3D mode
- Better 3D camera default: (15, 18, 35) instead of (0, 20, 45)
- Fixed dynamic mass trail Y in 3D mode: `view3D ? 0 : gridYAt(m.x, m.z)`
- **Commit:** `75f4312`

---

## 19. Major 3D Curvature Overhaul
**Prompt:** (continuation from prior session — dynamic masses, scenarios, controls)

**Changes:**
- Dynamic masses: masses can have velocities and move under mutual N-body gravity
- Scenario presets: ISS Orbiting Earth, Moon Orbiting Earth, Earth Orbiting Sun, Binary Star System, Figure-8 Three-Body
- Simulation controls: Pause/Play, Reset All, speed slider (0.1x–5.0x)
- Camera controls: Top/Side/Front View, Free Rotation, Follow Body mode
- Fullscreen mode with ESC to exit
- Body sizes scaled by mass, custom colors per body
- HTML label overlays projected from 3D positions
- Force vectors: optional red ArrowHelper showing gravitational force
- Educational readouts: altitude, escape velocity
- **Commit:** (prior session)

---

## 18. Adaptive Difficulty Level System
**Prompt:** "Make the website work for both younger students (7th-12th grade) and college level: 1. Add difficulty level toggle at the top... 2. Adaptive content for each section... 3. Visual indicators... 4. Educational scaffolding... 5. Interactive elements scale with difficulty... 6. Teacher/classroom features... Make it feel like ONE cohesive tool that grows with the student, not three separate websites!"

**Changes:**
- Added 3-button difficulty toggle in hero section: Beginner (Grades 7–9), Intermediate (Grades 10–12), Advanced (College+)
- Body-class CSS system (`level-beginner`, `level-intermediate`, `level-advanced`) with content visibility rules
- Wrote ~40 alternate explain paragraphs (beginner + advanced variants) across all 12 sections
  - Beginner: simple analogies, no equations ("Imagine two identical twins...")
  - Intermediate: original text, unchanged
  - Advanced: full math — four-vectors, Minkowski metric, Schwarzschild solution, rapidity, stress-energy tensor
- Added color-coded section difficulty badges (green/yellow/red) to all 12 section headings
- Added ~15 technical term tooltips (time dilation, geodesic, worldline, light cone, etc.) with hover definitions — hidden in advanced mode
- Added "Recommended path" banner in beginner mode (sections 01 → 02 → 03 → 06 → 09)
- Added beginner-friendly E=mc² subtitle in hero
- Derivation block (Lorentz Factor section) hidden in beginner mode via `.eq-only` class
- localStorage persistence — level saved and restored across visits
- Classroom mode: `?level=beginner` URL parameter locks level and hides toggle for teacher-shared links
- Per-section override CSS classes for future "Show Simple / Show Full" buttons
- **Commit:** `2c5d767`

---

## 17. "The Speed Limit of the Universe" — New Section 01
**Prompt:** "Add a new interactive section called 'The Speed Limit of the Universe (Explained Simply)' with: [5 detailed sub-visualizations] NO equations, NO formulas - just visual storytelling and animations that make it intuitive!"

**Follow-up prompt (position):** "Before section 01 (first section)"

**Changes:**
- Added 5-tab interactive section — purely visual, no equations
- **Tab 1: Speedometer of Spacetime** — Quarter-circle arc visualization; dot moves along arc as speed increases; X-axis = speed through space (cyan), Y-axis = speed through time (amber); projection lines show tradeoff; descriptive labels change at different speed ranges
- **Tab 2: Astronaut Aging** — Three-column comparison (Sitting Still, Fast Rocket, Photon); animated clock faces ticking at different rates; astronaut figures with helmets/spacesuits; star streaks show motion; age counters diverge in real time
- **Tab 3: Photon's View** — Split screen "Your View" vs "Photon's View"; photon travels Sun→Earth (8 min, 150M km); universe squishes flat via length contraction animation
- **Tab 4: The Wall (Energy Hill)** — Hill curve steepens with speed (green→yellow→red); stick figure pushing boulder up slope; sweat drops at high speeds; vertical wall at c with "IMPOSSIBLE"; photon floats over wall (massless)
- **Tab 5: Birthday Candles** — Twin comparison with birthday cakes; candles light at different rates; clock faces above each twin; candle count diverges over 20-year trip
- Each tab has its own 800×500 canvas with Play/Pause, Reset, and speed controls
- ~700 lines of JS in a single IIFE with tab switching and animation loop dispatcher
- Inserted as new section 01; all existing sections renumbered +1
- **Commit:** `28a8ca0`

---

## 16. Multi-Plane Orbital Demonstrations
**Prompt:** "Add to the gravity visualization: 1. Show multiple orbital planes simultaneously around the same central mass 2. Add preset examples: horizontal orbit, vertical orbit, 45° tilted orbit 3. Let users click to add particles with different orbital inclinations 4. Show that all orbital planes are equally valid - no preferred direction 5. Include real examples: our solar system's ecliptic plane vs Pluto's tilted orbit vs globular cluster's spherical distribution. This proves that gravity is truly spherically symmetric - orbits work in any orientation."

**Changes:**
- Added "Orbital Planes" mode button to curvature section
- Added orbital inclination slider (0°–180°) for orbit and orbital planes modes
- Inclination-aware orbit launching: velocity = speed × (cos(incl) × horiz_tangent + sin(incl) × vertical)
- 3 orbital plane presets (auto-switch to 3D view):
  - **3-Plane Demo**: equatorial (0°), polar (90°), tilted (45°) — all equally stable
  - **Solar System**: Mercury (7°), Earth (0°), Mars (1.9°), Pluto (17°), comet (62°)
  - **Globular Cluster**: 8 stars with uniformly distributed inclinations via `acos(2t-1)` — truly spherical
- Added `hslToHex()` helper, `orbitalPresets` config object, `launchOrbitalPreset()`, `generateGlobularOrbits()`
- Increased MAX_PARTICLES from 10 to 12
- **Commit:** `8899d15`

---

## 15. Move Spacetime Curvature to Section 04
**Prompt:** "Can you move 10 Spacetime Curvature in 3D to position 04?"

**Changes:**
- Cut section 10 HTML and inserted after section 03 (Causality Violation)
- Renumbered all affected sections: old 04→05, 04b→05b, 05→06, 06→07, 07→08, 08→09, 09→10
- Updated all HTML comments and `<span class="num">` tags
- **Commit:** `b3f1d36`

---

## Summary of file changes

| File | Description |
|------|-------------|
| `index.html` | Single-file app, grew from ~5400 to ~8200+ lines |
| `progress.md` | Documentation updated after every change |
| `CHANGELOG.md` | This file |

## Section order (final)

| # | Section | Badge |
|---|---------|-------|
| 01 | The Speed Limit of the Universe | Start Here (green) |
| 02 | The Twin Paradox | Beginner (green) |
| 03 | Length Contraction | Beginner (green) |
| 04 | Causality Violation — Why FTL Breaks Reality | Intermediate (yellow) |
| 05 | Spacetime Curvature in 3D | Intermediate (yellow) |
| 06 | Photon Clock & Time Dilation | Beginner (green) |
| 06b | Minkowski Spacetime Diagram | Intermediate (yellow) |
| 07 | The Lorentz Factor | Intermediate (yellow) |
| 08 | The Infinite Energy Barrier | Advanced (red) |
| 09 | Real-World Evidence | Beginner (green) |
| 10 | E=mc² and Mass-Energy Equivalence | Intermediate (yellow) |
| 11 | Putting It All Together | Intermediate (yellow) |
