# FTL Impossibility Visualizer — Progress

## Live URL
https://sampsonb.github.io/ftl-impossibility/

## Sections (current order)

### 01 — The Twin Paradox
- Animated rocket trip: Earth to destination star and back
- Traveler twin rides above the rocket with live aging counter
- Earth twin stays grounded with their own aging counter
- Hair grays realistically with age
- Full-width spacetime (Minkowski) diagram below the trip scene
  - Earth twin worldline (vertical/stationary)
  - Traveler worldline (kinked V-shape)
  - Animated tracking dots on both worldlines
  - Turnaround kink highlighted
  - Light cone reference lines
  - Proper time annotations on reunion
- Sliders: velocity (0.10c–0.99c), destination distance (0.5–25 ly)
- Controls: Launch/Pause, Reset, Speed (1x/2x/5x/10x)
- 6 readouts: both ages, both elapsed times, age difference, trip phase

### 02 — Photon Clock & Time Dilation
- Side-by-side animated photon clocks (stationary vs moving)
- Smooth easing with proper requestAnimationFrame timestamps
- Photon trails, mirror flash effects, layered glow
- Pythagorean triangle overlay on moving clock (c·t₀, v·t, c·t)
- Velocity slider (0–0.99c)
- Readouts: velocity, Lorentz factor, time dilation, traveler time

### 02b — Minkowski Spacetime Diagram
- Interactive spacetime diagram with color-coded regions
  - Future/past light cones (yellow)
  - Spacelike regions (blue, labeled "FTL needed")
- Animated photons traveling along the light cone
- Object worldline tilts toward light cone with velocity
- Simultaneity line showing how "now" tilts for moving observers
- Proper time tick marks along the worldline
- Smooth slider interpolation
- Readouts: worldline angle, light cone angle, proper time ratio, simultaneity tilt

### 03 — The Lorentz Factor
- Interactive γ vs velocity graph (asymptotic blowup at c)
- Crosshair tracking dot on the curve
- Step-by-step derivation from the photon clock geometry (7 steps)
- Readouts: v/c, γ, length contraction %, relativistic mass

### 03b — Length Contraction
- Detailed starship (hull, cockpit, wings, engines) drawn on canvas
- Top panel: ship at rest with ruler and grid
- Bottom panel: contracted ship against same fixed grid
- Ghost outline of rest-length ship for comparison
- Red dashed contraction arrows
- Fly-by mode: 4 ships at 0.10c/0.50c/0.80c/0.95c with motion blur
- Formula overlay: L = L₀/γ
- Readouts: rest length, observed length, contraction %, γ

### 04 — The Infinite Energy Barrier
- 3 tabbed graphs: Kinetic Energy, Total Energy, Momentum
- Each shows relativistic vs classical (Newtonian) curves
- Velocity slider with tracking dot
- Readouts: rest energy, KE, total energy, momentum (all in mc² units)

### 05 — Real-World Evidence
- 4 example cards: GPS satellites, muon decay, particle accelerators, stellar aberration
- Interactive muon decay simulation
  - Classical vs relativistic survival rates descending from 15 km
  - Animated particle groups fading as muons decay
  - Play/Pause/Reset controls

### 06 — E=mc² and Mass-Energy Equivalence
- Log-scale bar chart: rest energy vs Hiroshima vs US daily energy vs relativistic energy
- Mass slider (1–100 kg)
- Readouts: rest energy, TNT equivalent, city-powering duration

### 07 — Putting It All Together
- Combined graph overlaying γ, time dilation, length contraction, energy
- High-precision slider (0.0000c–0.9999c)
- All curves diverge simultaneously at c
- Readouts: γ, time dilation, length %, energy

## Technical Details
- Single self-contained HTML file (~3000 lines)
- Vanilla JS + HTML5 Canvas (no dependencies)
- Animated starfield background
- Responsive design with dark theme
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
