# FTL Impossibility Visualizer — Progress

## Live URL
https://sampsonb.github.io/ftl-impossibility/

## Sections (current order)

### 01 — The Speed Limit of the Universe (Explained Simply)
- Five-tab interactive section — NO equations, purely visual storytelling
- **Tab 1: Speedometer of Spacetime**
  - Quarter-circle arc visualization: dot moves along arc as speed increases
  - X-axis = speed through space (cyan), Y-axis = speed through time (amber)
  - Projection lines show how one trades off for the other
  - Descriptive labels change at different speed ranges
  - Slider: 0.00c – 1.00c
- **Tab 2: Astronaut Aging**
  - Three-column comparison: Sitting Still, Fast Rocket (adjustable), Photon
  - Animated clock faces ticking at different rates
  - Astronaut figures with helmets and spacesuits
  - Star streaks show motion, frozen blur for photon
  - Age counters diverge in real time
  - Play/Pause, Reset controls; speed slider
- **Tab 3: Photon's View**
  - Split screen: "Your View" vs "Photon's View"
  - Top: photon travels Sun to Earth (8 minutes, 150M km)
  - Bottom: universe squishes flat — Sun and Earth merge together
  - Length contraction animated in real time
  - "To the photon, the whole universe is squished flat!"
  - Play/Pause, Reset controls
- **Tab 4: The Wall (Energy Hill)**
  - Hill curve steepens with speed (green → yellow → red)
  - Stick figure pushing boulder up increasingly steep slope
  - Sweat drops appear at high speeds
  - Vertical wall at c with "IMPOSSIBLE" label
  - Photon floats effortlessly over the wall (massless)
  - Speed slider: 0.00c – 1.00c
- **Tab 5: Birthday Candles**
  - Twin comparison: Earth Twin vs Traveler Twin
  - Birthday cakes with candles lighting up at different rates
  - Clock faces above each twin
  - Candle count diverges over a 20-year trip
  - Play/Pause, Reset, Speed (1×/2×/5×/10×) controls; speed slider

### 02 — The Twin Paradox
- Animated rocket trip: Earth to destination star and back
- Rocket points correctly (toward star outbound, toward Earth on return)
- Traveler twin rides above the rocket with live aging counter during flight
- Earth twin stays grounded with their own aging counter
- Hair grays realistically with age
- Controls (Launch/Pause, Reset, Speed) placed above the canvas
- Full-width spacetime (Minkowski) diagram below the trip scene
  - Earth twin worldline (vertical/stationary)
  - Traveler worldline (kinked V-shape)
  - Animated tracking dots on both worldlines
  - Turnaround kink highlighted
  - Light cone reference lines
  - Outbound/return leg labels
  - Proper time annotations with background pills on reunion
  - Departure and reunion event markers
- Sliders: velocity (0.10c–0.99c), destination distance (0.5–25 ly)
- Controls: Launch/Pause, Reset, Speed (1x/2x/5x/10x)
- 6 readouts: both ages, both elapsed times, age difference, trip phase

### 03 — Length Contraction
- Detailed starship (hull, cockpit, wings, engines) drawn on canvas
- Top panel: ship at rest with ruler and grid
- Bottom panel: contracted ship against same fixed grid
- Ghost outline of rest-length ship for comparison
- Red dashed contraction arrows
- Fly-by mode: 4 ships at 0.10c/0.50c/0.80c/0.95c with motion blur
- Formula overlay: L = L₀/γ
- Readouts: rest length, observed length, contraction %, γ

### 04 — Causality Violation — Why FTL Breaks Reality
- Two-tab layout: Simultaneity & Light Cones / The Paradox
- **Tab 1: Simultaneity & Light Cones**
  - Interactive spacetime diagram with light cones and spacelike "FTL Zone"
  - Earth and Alpha Centauri worldlines (4.37 ly apart)
  - FTL message line drawn in spacelike region (outside light cone)
  - Moving observer's simultaneity line tilts with velocity slider
  - Shows how "now" disagrees between reference frames
  - Lorentz-transformed arrival time: t' = γ(t - vx/c²)
  - When t' goes negative → red "CAUSALITY VIOLATION" flash
  - Animated photons on light cone for reference
  - Two sliders: observer velocity (0–0.95c) and FTL speed (2–50c)
  - 6 readouts: velocity, FTL speed, Earth arrival, moving frame arrival, time reversal, causality status
- **Tab 2: The Paradox**
  - Animated 7-phase scenario: ready → send → arrive → reframe → reply → paradox → loop
  - Top panel: scene with Earth and Alpha Centauri, animated FTL pulses
  - Bottom panel: spacetime diagram showing worldlines and causal loop
  - Concrete numbers: send at T=0, arrive T=+2yr, moving frame T'=-0.21yr (-78 days)
  - "HELLO" sent, "DON'T SEND" reply arrives before original message
  - Causal loop triangle highlighted with pulsing animation
  - Play/Pause, Reset, Speed (1×/2×/5×/10×) controls
  - 6 readouts: Earth clock, AC clock, moving frame clock, phase, message content, paradox status

### 05 — Spacetime Curvature in 3D
- Interactive 3D visualization using Three.js + OrbitControls
- **2D Sheet view**: 60×60 vertex grid deforms downward (classic rubber-sheet analogy)
- **3D Spherical view**: 3 concentric icosahedron shells (r=8, 14, 20) compress inward toward masses at center
  - Masses sit at the CENTER of the shells — demonstrates gravity curves space equally in ALL directions
  - Enhanced deformation (3.5× pull factor) for more visible curvature
  - 3 orthogonal cross-section rings (XZ amber, XY cyan, YZ purple) show curvature in each plane
- Grid/shell vertex colors show gravitational time dilation (red = slow, blue = flat)
- Schwarzschild-like potential: displacement ∝ -M/r (1.5× depth scale for dramatic wells)
- Click to place masses (up to 5), raycasting onto XZ plane
- Particle simulation with full 3D Verlet integration following geodesics
  - Drop mode: particles fall from rest into gravity wells
  - Orbit mode: tangential launch for orbital mechanics (inclination-aware)
  - **Launch speed calibrated** to circular orbit velocity (slider: 0x–2x v_circ)
  - **Rain mode**: 6 particles from ±X, ±Y, ±Z all fall inward — proves omnidirectional curvature
  - **Orbital Planes mode**: multi-plane orbital demonstrations
  - Trail rendering (300-point ring buffer), togglable on/off
- **Physics engine**: velocity-Verlet integrator with fixed sub-step size (0.004s)
  - Explicit velocity storage (no more implicit prevX/prevZ)
  - Symplectic integrator conserves energy to <0.01% drift
  - `gravAccel()` helper computes gravitational acceleration at any point
  - `computeTotalEnergy()` tracks kinetic + potential energy for conservation checks
  - Energy drift readout shows conservation quality (green <0.01%, yellow <0.1%, red >0.1%)
  - Step Forward button for single-frame debugging while paused
- **Dynamic masses**: masses can have velocities and move under mutual N-body gravity
  - Enables Binary Star and Figure-8 scenarios
  - Grid deformation updates dynamically as masses move
  - Dynamic masses leave their own orbit trails
- **Scenario presets** (educational, with calibrated physics):
  - **ISS Orbiting Earth**: blue Earth, ISS at distance 6, stable circular orbit
  - **Moon Orbiting Earth**: blue Earth, gray Moon at distance 12
  - **Earth Orbiting Sun**: gold Sun, blue Earth at distance 10
  - **Binary Star System**: two equal dynamic masses orbiting common center of mass
  - **Figure-8 Three-Body**: Chenciner-Montgomery solution — 3 equal masses on figure-8 path
- **Simulation controls**: Pause/Play, Reset All, speed slider (0.1x–5.0x)
- **3D centering fix**: masses positioned at CENTER of spherical grid (Y=0), not on deformed surface
- **3D axis labels**: X (red), Y (green), Z (blue) dashed axis lines with projected labels — shows no preferred "down"
- **Omnidirectional hint**: educational note appears in 3D mode explaining gravity curves space in ALL directions
- **Camera controls**: Top View, Side View, Front View, Free Rotation presets; Follow Body mode
- **Full orbit freedom**: removed polar angle constraint — camera can view from any direction including below
- **Fullscreen mode**: expands visualization to fill viewport, H key shows/hides controls, ESC to exit
- **Visual improvements**: body sizes scaled by mass, custom colors per body (Earth blue, Moon gray, Sun gold, etc.), HTML label overlays projected from 3D positions
- **Force vectors**: optional red ArrowHelper showing gravitational force on each particle
- **Educational readouts**: altitude (distance to nearest mass), escape velocity at current position
- Orbital inclination slider (0°–180°) for orbit and orbital planes modes
- **Orbital plane presets** (auto-switch to 3D view):
  - **3-Plane Demo**: equatorial (0°), polar (90°), tilted (45°) — all equally stable
  - **Solar System**: Mercury (7°), Earth (0°), Mars (1.9°), Pluto (17°), comet (62°)
  - **Globular Cluster**: 8 stars with uniformly distributed inclinations — truly spherical
- Mass presets: Earth (gentle), Sun (moderate), Black Hole (extreme + accretion ring), Binary Stars
- Toggle between 2D Sheet and 3D Spherical views
- Show/hide cross-section rings, grid, geodesic straightness, trails, force vectors
- **Reorganized bottom-panel UI**:
  - 3D container fills top 70-80% of section; controls consolidated at bottom
  - 3-column control panel: Quick Start (presets + scenarios) | Simulation (play/pause, speed, checkboxes) | Advanced (view, camera, mode, sliders)
  - Collapsible "Advanced" section with ▼/▶ toggle
  - Collapsible "Help" section with camera, shell, and mode explanations
  - Compact top-right info overlay: scenario name, elapsed time, time dilation, energy drift
  - Context-sensitive controls: launch speed shown only in orbit mode, Follow button only when bodies exist, Step+1 grayed when playing, mass slider hidden in scenarios
  - Enhanced fullscreen: H key toggles control panel visibility, ESC exits
  - Scenario descriptions available via button tooltips (title attributes)
  - Responsive: columns stack on ≤900px, compact sizing on ≤600px
- 9 readouts: masses, particles, velocity, time dilation, orbital period, altitude, escape velocity, time elapsed, energy drift

### 06 — Photon Clock & Time Dilation
- Side-by-side animated photon clocks (stationary vs moving)
- Smooth easing with proper requestAnimationFrame timestamps
- Photon trails, mirror flash effects, layered glow
- Pythagorean triangle overlay on moving clock (c·t₀, v·t, c·t)
- Velocity slider (0–0.99c)
- Readouts: velocity, Lorentz factor, time dilation, traveler time

### 06b — Minkowski Spacetime Diagram
- Interactive spacetime diagram with color-coded regions
  - Future/past light cones (yellow)
  - Spacelike regions (blue, labeled "FTL needed")
- Animated photons traveling along the light cone
- Object worldline tilts toward light cone with velocity
- Simultaneity line showing how "now" tilts for moving observers
- Proper time tick marks along the worldline
- Smooth slider interpolation
- Readouts: worldline angle, light cone angle, proper time ratio, simultaneity tilt

### 07 — The Lorentz Factor
- Interactive γ vs velocity graph (asymptotic blowup at c)
- Crosshair tracking dot on the curve
- Step-by-step derivation from the photon clock geometry (7 steps)
- Readouts: v/c, γ, length contraction %, relativistic mass

### 08 — The Infinite Energy Barrier
- 3 tabbed graphs: Kinetic Energy, Total Energy, Momentum
- Each shows relativistic vs classical (Newtonian) curves
- Velocity slider with tracking dot
- Readouts: rest energy, KE, total energy, momentum (all in mc² units)

### 09 — Real-World Evidence
- 4 example cards: GPS satellites, muon decay, particle accelerators, stellar aberration
- Interactive muon decay simulation
  - Classical vs relativistic survival rates descending from 15 km
  - Animated particle groups fading as muons decay
  - Play/Pause/Reset controls

### 10 — E=mc² and Mass-Energy Equivalence
- Log-scale bar chart: rest energy vs Hiroshima vs US daily energy vs relativistic energy
- Mass slider (1–100 kg)
- Readouts: rest energy, TNT equivalent, city-powering duration

### 11 — Putting It All Together
- Combined graph overlaying γ, time dilation, length contraction, energy
- High-precision slider (0.0000c–0.9999c)
- All curves diverge simultaneously at c
- Readouts: γ, time dilation, length %, energy

## Adaptive Difficulty Level System
- 3-level toggle in hero: Beginner (Grades 7–9), Intermediate (Grades 10–12), Advanced (College+)
- Body-class CSS system: `level-beginner`, `level-intermediate`, `level-advanced` on `<body>`
- Content tagged with `.level-beg`, `.level-int`, `.level-adv` — CSS shows/hides based on active level
- Default level: Intermediate (matches original content)
- localStorage persistence: level saved and restored across visits
- URL parameter `?level=beginner|intermediate|advanced` for classroom use (hides toggle)
- **Adaptive content per section**: beginner (simple analogies, no math), intermediate (current text), advanced (full equations, metric derivations, four-vectors)
- **Section difficulty badges**: color-coded labels on each section heading (green=beginner, yellow=intermediate, red=advanced)
- **Technical term tooltips**: ~15 key terms with hover definitions (hidden in advanced mode)
- **Recommended path banner**: shown in beginner mode — suggests order 01 → 02 → 03 → 06 → 09
- **Hero equation subtitle**: beginner-friendly explanation of E=mc² shown in beginner mode
- **Equation/derivation hiding**: `.eq-only` blocks hidden in beginner mode, `.deriv-only` shown only in advanced
- **Per-section override**: cards support local level override classes for "Show Simple / Show Full" toggling

## Netflix-Style Landing Page
- Full-viewport hero with progress bar and scroll hint animation
- Module card grid: 12 interactive cards with emoji icons, difficulty badges, hover effects
- Card layout: thumbnail area with gradient background → body with title, description, status
- Progress tracking: IntersectionObserver marks sections as "visited" after 2-second dwell
- localStorage persistence: visited sections saved across sessions
- Overall progress bar in hero and sticky nav (gradient fill, percentage)
- Module cards show visited/not-visited status with green dot
- Sticky navigation bar: appears when scrolling past module grid, highlights current section
- Backdrop-blur glass effect, horizontal scroll for section buttons
- Mini progress bar in nav with percentage
- Smooth scroll: clicking cards or nav items scrolls to section with `scroll-margin-top` offset
- Keyboard accessible: cards are focusable with Enter/Space activation
- Responsive: 3-column grid on desktop, single column on mobile

## Technical Details
- Single self-contained HTML file (~8200 lines)
- Vanilla JS + HTML5 Canvas for sections 01–04, 06–11; Three.js (CDN) for section 05
- Animated starfield background
- Responsive design with dark theme
- Tightened hero/section spacing for minimal dead space
- All animations use requestAnimationFrame with proper delta timing
- DPR-aware canvas rendering for crisp display on Retina screens
- Hosted on GitHub Pages (auto-deploys on push to main)

## Commits
1. Initial build — all core sections
2. Smoother photon clocks + Minkowski spacetime diagram
3. Deployed to GitHub Pages via `gh`
4. Twin paradox section with animated rocket trip
5. Length contraction visualization with fly-by mode
6. Twin paradox moved to section 01, stacked vertical layout
7. Rocket direction fix, controls moved above canvas
8. Traveler twin rides with rocket during flight
9. Reduced hero/section padding to eliminate large gap
10. Length contraction moved to section 02, all sections renumbered
11. Causality violation section with simultaneity diagram and paradox animation
12. Causality violation moved to section 03, all sections renumbered
13. 3D spacetime curvature section (10) with Three.js visualization
14. Added 3D Spherical view with concentric shells, cross-section rings, rain particles
15. Spacetime curvature moved to section 04, all sections renumbered
16. Multi-plane orbital demonstrations: inclination slider, 3-Plane/Solar System/Globular Cluster presets
17. "Speed Limit of the Universe" section with 5 visual tabs, moved to section 01
18. Adaptive difficulty level system: 3-level toggle, adaptive content, badges, tooltips, classroom mode
19. Major 3D curvature overhaul: physics fixes, dynamic masses, scenarios (ISS/Moon/Binary/Figure-8), pause/speed/camera/fullscreen controls, labels, force vectors
20. 3D centering fix: masses at center of spherical grid, axis labels, Front view, enhanced curvature visibility
21. Netflix-style landing page: module card grid, progress tracking, sticky nav, smooth scroll
22. 3D curvature polish: labeled presets, wireframe legend, axis arrowheads, camera help, time elapsed, trail visibility
23. Physics rewrite: velocity-Verlet integrator, fixed sub-steps, energy conservation tracking, Step Forward debug button
24. Curvature UI reorganization: bottom control panel, 3-column layout, collapsible sections, context-sensitive controls, info overlay, enhanced fullscreen
25. Camera default mode: explicit mode toggle for mass/particle placement, keyboard shortcuts (M/P/O/Esc), mode indicator overlay
