# FTL Impossibility Visualizer — Progress

## Live URL
https://sampsonb.github.io/ftl-impossibility/

## Sections (current order)

### 01 — The Twin Paradox
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

### 02 — Length Contraction
- Detailed starship (hull, cockpit, wings, engines) drawn on canvas
- Top panel: ship at rest with ruler and grid
- Bottom panel: contracted ship against same fixed grid
- Ghost outline of rest-length ship for comparison
- Red dashed contraction arrows
- Fly-by mode: 4 ships at 0.10c/0.50c/0.80c/0.95c with motion blur
- Formula overlay: L = L₀/γ
- Readouts: rest length, observed length, contraction %, γ

### 03 — Causality Violation — Why FTL Breaks Reality
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

### 04 — Spacetime Curvature in 3D
- Interactive 3D visualization using Three.js + OrbitControls
- **2D Sheet view**: 60×60 vertex grid deforms downward (classic rubber-sheet analogy)
- **3D Spherical view**: 3 concentric icosahedron shells (r=8, 14, 20) compress inward toward masses
  - Demonstrates gravity curves space equally in ALL directions, not just "downward"
  - 3 orthogonal cross-section rings (XZ amber, XY cyan, YZ purple) show curvature in each plane
- Grid/shell vertex colors show gravitational time dilation (red = slow, blue = flat)
- Schwarzschild-like potential: displacement ∝ -M/r
- Click to place masses (up to 5), raycasting onto XZ plane
- Particle simulation with full 3D Verlet integration following geodesics
  - Drop mode: particles fall from rest into gravity wells
  - Orbit mode: tangential launch for orbital mechanics
  - **Rain mode**: 6 particles from ±X, ±Y, ±Z all fall inward — proves omnidirectional curvature
  - Trail rendering (300-point ring buffer)
- Presets: Earth (gentle), Sun (moderate), Black Hole (extreme + accretion ring), Binary Stars
- Toggle between 2D Sheet and 3D Spherical views
- Show/hide cross-section rings, grid, geodesic straightness
- Geodesic straightness: red dashed (flat line) vs green (curved geodesic)
- Mouse controls: rotate, zoom, pan via OrbitControls
- Tooltip showing gravitational potential and time dilation at cursor
- 5 readouts: masses placed, active particles, velocity, time dilation, orbital period

### 05 — Photon Clock & Time Dilation
- Side-by-side animated photon clocks (stationary vs moving)
- Smooth easing with proper requestAnimationFrame timestamps
- Photon trails, mirror flash effects, layered glow
- Pythagorean triangle overlay on moving clock (c·t₀, v·t, c·t)
- Velocity slider (0–0.99c)
- Readouts: velocity, Lorentz factor, time dilation, traveler time

### 05b — Minkowski Spacetime Diagram
- Interactive spacetime diagram with color-coded regions
  - Future/past light cones (yellow)
  - Spacelike regions (blue, labeled "FTL needed")
- Animated photons traveling along the light cone
- Object worldline tilts toward light cone with velocity
- Simultaneity line showing how "now" tilts for moving observers
- Proper time tick marks along the worldline
- Smooth slider interpolation
- Readouts: worldline angle, light cone angle, proper time ratio, simultaneity tilt

### 06 — The Lorentz Factor
- Interactive γ vs velocity graph (asymptotic blowup at c)
- Crosshair tracking dot on the curve
- Step-by-step derivation from the photon clock geometry (7 steps)
- Readouts: v/c, γ, length contraction %, relativistic mass

### 07 — The Infinite Energy Barrier
- 3 tabbed graphs: Kinetic Energy, Total Energy, Momentum
- Each shows relativistic vs classical (Newtonian) curves
- Velocity slider with tracking dot
- Readouts: rest energy, KE, total energy, momentum (all in mc² units)

### 08 — Real-World Evidence
- 4 example cards: GPS satellites, muon decay, particle accelerators, stellar aberration
- Interactive muon decay simulation
  - Classical vs relativistic survival rates descending from 15 km
  - Animated particle groups fading as muons decay
  - Play/Pause/Reset controls

### 09 — E=mc² and Mass-Energy Equivalence
- Log-scale bar chart: rest energy vs Hiroshima vs US daily energy vs relativistic energy
- Mass slider (1–100 kg)
- Readouts: rest energy, TNT equivalent, city-powering duration

### 10 — Putting It All Together
- Combined graph overlaying γ, time dilation, length contraction, energy
- High-precision slider (0.0000c–0.9999c)
- All curves diverge simultaneously at c
- Readouts: γ, time dilation, length %, energy

## Technical Details
- Single self-contained HTML file (~5400 lines)
- Vanilla JS + HTML5 Canvas for sections 01–03, 05–10; Three.js (CDN) for section 04
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
