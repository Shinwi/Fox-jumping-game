# Changelog

All notable changes to Forest Dash are documented here.

---

## [v3.3] — 2026-03-29

### Added

- **Portrait-mode rotation warning** — on touch devices held in portrait orientation, a full-screen overlay (`#portrait-warning`) fades in with an animated rotating phone icon and a "Rotate your phone to play in landscape!" message. It disappears automatically when the device is rotated. Implemented purely in CSS using `@media (pointer: coarse) and (orientation: portrait)` — zero JavaScript required.
- **Landscape mobile canvas sizing** — `getCanvasDims()` now reads `window.innerHeight` and caps the canvas height to `vh - 72px`. This ensures the canvas never overflows the viewport in landscape on phones (e.g. a 375px-tall iPhone landscape viewport gets a ~303px canvas instead of the default 380px).

### Reverted

- **Keyboard button navigation** — the arrow-key panel navigation, char-card `tabindex`, auto-focus on panel open, pixel focus rings, and `InputHandler` Space-key changes introduced in this session were reverted at user request. `InputHandler` is back to its original behaviour (Space or ArrowUp = act).

---

## [v3.2] — 2026-03-29

### Added

- **Grape collectible** — a bunch of grapes drawn as a pyramid of six purple circles (3–2–1 layout) with per-bead shine highlights, a green stem, and a small leaf. Worth +25 points on pickup — the highest value collectible.
- **Grape HUD counter** — a 🍇 counter in purple (`#c080e8`) added to the collectible row, flashes independently on pickup.
- **Grape in game over summary** — the end-of-run stats line now shows all three icons: `🍫 N  🍓 N  🍇 N`.

### Changed

- **Spawn distribution** — collectible spawn now picks evenly across three kinds (≈33% each) instead of 50/50 chocolate/strawberry.
- `COLLECT_SCORE` extended: `{ chocolate: 20, strawberry: 15, grape: 25 }`.
- `collectWith()` return shape updated from `{ total, choco, straw }` to `{ choco, straw, grape }` — score is now computed per kind in the Game loop so each counter stays independent.

---

## [v3.1] — 2026-03-29

### Added

- **Clouds** — five procedurally generated clouds drift slowly across the sky. Each cloud is rendered as a cluster of overlapping white ellipses with a soft blue-tinted underside shadow. Every cloud has its own randomised scale (0.65–1.35×) and drift multiplier (0.5–1.3×) so they move at slightly different speeds, giving a natural layered feel.
- **Pink ribbon for Cuycita** — the Cuy character now has a cute pink bow rendered on top of her head. Drawn as two rotated ellipse wings, a dark-pink center knot, and highlight shine — baked into every run and jump frame.

### Changed

- **Split collectible HUD counters** — the single 🍓 collect counter has been replaced with two independent counters: 🍫 for chocolates and 🍓 for strawberries. Each flashes its own element when the corresponding item is collected. The game over screen now shows both counts separately.
- **Cuy renamed to Cuycita** — character card, ready panel title (`🐹 CUYCITA DASH`), and internal name string updated throughout.

### Fixed

- **Score double-count on collection** — rewired the collectible pickup path so chocolate and strawberry scores are added in separate branches, avoiding any risk of double-adding `total` alongside per-kind values.

---

## [v3.0] — 2026-03-29

### Added

- **River obstacles** — wide animated water gaps (80–150 px) that scroll with the game. The player must jump over them. Landing on a river at ground level causes an instant game over. Rivers render animated wave lines, sunlight sparkle highlights, and dark muddy banks. A cooldown of 220 frames prevents rivers from spawning back-to-back.
- **Chocolate collectible** — a brown segmented chocolate bar with a groove pattern and a shine highlight. Worth +20 points on pickup.
- **Strawberry collectible** — a red teardrop-shaped berry with seeds, green leaves, and a shine highlight. Worth +15 points on pickup.
- **Collectible sparkle burst** — both collectible types emit a ring of colour-matched particles on collection, plus an expanding ring fade-out animation.
- **Double jump for Cuy** — the Cuy (guinea pig) character can now double jump, matching the Fox. `MAX_JUMPS` is `2` for both characters.

### Changed

- **Canvas height increased** — desktop canvas raised from `280 px` to `380 px`; mobile from `220 px` to `300 px`. All derived values (ground Y, spawn heights, hitboxes) recalculate proportionally so nothing breaks.
- **Background simplified** — far tree count reduced from 18 to 6; mid tree count reduced from 10 to 4; the bush layer was removed entirely. The result is a cleaner, less cluttered forest.
- **HUD updated** — the coin counter (🪙) replaced with a collectibles counter (🍓) that increments for any item picked up regardless of type.
- **Game Over screen** — "Coins" stat replaced with "Collected" count.
- **Character selection** — Cuy description updated from "High jump" to "Double jump".
- **Character name** — "GUINEA PIG" renamed to "CUY" in the selection screen and ready panel title.

### Removed

- **Coins** — the `Coin` class and `CoinManager` class removed entirely.
- **Day/Night cycle** — the oscillating `skyT` value, night sky gradient, star field, moon rendering, and the `DAY_FRAMES` constant have all been removed. The sky is permanently a bright daytime blue gradient with a glowing sun.
- **Mode display** (`☀️ DAY` / `🌙 NIGHT`) — the HUD mode label removed alongside the day/night cycle.

### Fixed

- **Panel button cutoff** — overlay panels (character select, ready, game over) now have `overflow-y: auto` and `padding: 20px 12px`. The confirm/start/retry buttons have `flex-shrink: 0` applied, preventing them from being clipped on small or narrow screens. This fixes the "Play button partially cut off" issue on mobile.

---

## [v2.0] — prior

- Initial ES6 rewrite with class-based architecture
- Fox and Cuy (Guinea Pig) character selection with procedural sprite animation
- Parallax forest background with far trees, mid trees, and bushes
- Log obstacles (single and double)
- Coin collectibles with sparkle animation
- Day/Night sky cycle (1800-frame period)
- Web Audio beep engine (no audio files)
- Particle system for dust and death explosions
- Responsive canvas sizing for desktop and mobile
- Session high score tracking
