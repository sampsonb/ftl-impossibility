# Changelog — FTL Impossibility Visualizer

All changes from the February 2026 build session.

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
| `index.html` | Single-file app, grew from ~5400 to ~7100 lines |
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
