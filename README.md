# 🌲 Forest Dash — Fox & Cuy Runner

A browser-based endless runner game inspired by the Chrome Dino game. Play as a Fox or a Cuy (guinea pig) and sprint through a procedurally generated forest, leaping over logs and rivers while collecting chocolate and strawberries.

No build tools. No frameworks. One `index.html` file.

---

## Gameplay

You run automatically. Press **Space**, **↑**, or **tap** the screen to jump. Use your second jump mid-air to clear wider gaps. Avoid logs and rivers — touching either ends the run. Collect chocolate bars and strawberries for bonus points. Speed increases gradually over time.

### Controls

| Action      | Keyboard        | Mobile          |
|-------------|-----------------|-----------------|
| Jump        | Space / Arrow ↑ | Tap screen      |
| Double jump | Space / Arrow ↑ | Tap again in air|

---

## Characters

| Character  | Jump height | Double jump |
|------------|-------------|-------------|
| 🦊 Fox     | Normal      | Yes         |
| 🐹 Cuy     | Higher      | Yes         |

Both characters have a fully animated run cycle (4–5 frames at 10 FPS) and a dedicated jump pose, rendered procedurally onto off-screen canvases at startup.

---

## Collectibles

| Item          | Bonus  | Spawn location    |
|---------------|--------|-------------------|
| 🍫 Chocolate  | +20 pts | Ground or mid-air |
| 🍓 Strawberry | +15 pts | Ground or mid-air |

Collectibles bob gently and burst into sparkles when picked up.

---

## Obstacles

- **Logs** — single or double stacked; jump over them
- **Rivers** — wide animated water gaps; must be cleared by jumping over them; landing in one is an instant game over

---

## Features

- Procedural pixel-art sprites — no external image assets
- Parallax forest background with two tree layers and a glowing sun
- Particle system: foot dust, death explosion, collect bursts
- Fully responsive canvas — adapts to desktop and mobile viewport sizes
- Web Audio API beeps for jump, collect, milestone, and death — no audio files required
- Session high score

---

## Running the Game

Open `index.html` directly in any modern browser — no server required.

```
double-click index.html
```

Or serve locally if your browser restricts local file access:

```bash
npx serve .
# open http://localhost:3000
```

---

## Project Structure

```
cuyJump/
├── index.html      # Entire game — HTML, CSS, and JS in a single file
├── README.md
├── CHANGELOG.md
└── ROADMAP.md
```

### Code Architecture (inside `index.html`)

| Class / Function     | Responsibility                                           |
|----------------------|----------------------------------------------------------|
| `Game`               | State machine, main `requestAnimationFrame` loop, HUD   |
| `Player`             | Physics, double jump logic, hitbox, animation timing     |
| `SpriteRenderer`     | Pre-bakes procedural frames onto off-screen canvases     |
| `drawFoxFrame()`     | Procedural pixel-art draw function for the Fox           |
| `drawGuineaFrame()`  | Procedural pixel-art draw function for the Cuy           |
| `ObstacleManager`    | Spawns and scrolls logs and rivers; collision dispatch   |
| `LogObstacle`        | Renders a single or double log with wood grain detail    |
| `River`              | Animated water gap; kills player on ground contact       |
| `CollectibleManager` | Spawns, scrolls, and collision-checks collectibles       |
| `Collectible`        | Bobbing animation, sparkle burst, kind-specific drawing  |
| `Background`         | Two-layer parallax trees, sun, ground strip, pebbles     |
| `ParticleSystem`     | Generic particle emitter for dust and explosions         |
| `AudioEngine`        | Web Audio oscillator beeps — entirely self-contained     |
| `InputHandler`       | Keyboard and pointer events unified into a single action |

---

## Browser Support

Requires a browser with support for:

- Canvas 2D API
- Web Audio API
- `requestAnimationFrame`
- ES6 classes

Works in Chrome, Firefox, Safari, and Edge. No polyfills or transpilation needed.

---

## License

Free to use and modify for personal or educational purposes.
