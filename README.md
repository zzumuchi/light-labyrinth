# Light Labyrinth

Light Labyrinth is a browser-based 3D puzzle game about guiding a laser through a closed room. Players place and rotate optical objects to reflect or split the beam, avoid obstacles, and deliver the required light to the sensor.

## Gameplay

Each stage introduces a different light-manipulation challenge. Select a stage, arrange the available objects, then click the laser source to test the path. A successful beam activates the sensor and advances to the next stage; an unsuccessful attempt costs one life.

The six stages progress through:

- straight-line beam routing
- reflection with triangular and trapezoidal mirrors
- splitting and recombining light with a dispersion cube
- multi-reflection paths around fixed obstacles
- puzzles that combine movable and fixed optical elements

## Features

- Real-time laser ray casting with up to 20 reflections
- Reflection, obstruction, and red/blue beam dispersion
- Grid-snapped placement and axis-based 90° rotation
- Six selectable stages with per-stage object limits
- Perspective, top, front, side, and first-person camera modes
- Bloom post-processing, textured materials, shadows, and stage-clear effects
- Responsive full-screen interface with lives and laser status

## Controls

| Input | Action |
| --- | --- |
| Mouse drag | Move a selected optical object or orbit the camera |
| Mouse wheel on a rotation axis | Rotate the selected object by 90° |
| Click the laser source | Turn the laser on or off and test the solution |
| `1` / `2` / `3` / `4` | Perspective / top / front / side view |
| `V` | Toggle first-person view |
| `W` `A` `S` `D` | Move in first-person view |
| `R` | Reset movable objects in the current stage |
| `Esc` | Exit first-person view |

## Tech Stack

- JavaScript ES modules
- [Three.js 0.160.0](https://threejs.org/)
- Three.js OrbitControls and PointerLockControls
- EffectComposer with UnrealBloomPass
- HTML5 and CSS3

The project has no build step or package installation.

## Run Locally

Because the game loads JavaScript modules and texture assets, serve the repository through a local web server rather than opening `index.html` directly.

```bash
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in a modern desktop browser.

## Project Structure

```text
.
├── index.html              # Game UI and Three.js import map
├── style.css               # Layout, HUD, and stage-selection styles
└── src
    ├── main.js             # Scene setup, game state, controls, and stage flow
    ├── laser.js            # Ray casting, reflection, and dispersion logic
    ├── objects.js          # Room, player, sensor, mirror, and prism geometry
    ├── stages.js           # Stage definitions and object limits
    └── assets/textures     # Surface and material textures
```

## How It Works

The laser system casts a ray from the source toward the nearest interactive object. Reflective surfaces calculate a new direction from the surface normal, while the dispersion cube branches a white beam into red and blue rays. The sensor completes a stage when it receives either a white beam or both component colors. Reusable beam meshes keep the visualization efficient as the player edits the path in real time.
