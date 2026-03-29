# Roadmap — Upcoming Changes

Planned improvements and feature ideas for Forest Dash, roughly ordered by priority.

---

## High Priority

### Persistent High Score
Store the best score in `localStorage` so it survives page refreshes and browser restarts. Show a "New best!" flash on the game over screen when the player beats their record.

### Real Sprite Sheets
Replace the current procedural canvas drawing with actual sprite sheet images loaded via `<img>` tags and sliced with `drawImage(img, sx, sy, sw, sh, dx, dy, dw, dh)`.

Candidate free assets (CC0 / CC-BY):
- Fox run cycle — [OpenGameArt: "Fox" by bevouliin](https://opengameart.org/content/fox-platformer-game-sprite)
- Guinea pig / Cuy — [OpenGameArt: small animal sprites](https://opengameart.org)
- Fallback: [itch.io free asset packs](https://itch.io/game-assets/free)

This would also enable smoother animations at higher frame counts without the per-frame canvas re-draw cost.

### Sound Effects File
Add proper `.ogg`/`.mp3` sound effects (jump thud, water splash for river death, collect chime) using the Web Audio API's `decodeAudioData`. Keep the oscillator beeps as a silent-context fallback.

---

## Gameplay

### Slide / Duck Mechanic
Hold **↓** (keyboard) or **swipe down** (mobile) to make the character crouch. Add low-flying log obstacles (e.g. a branch) that require ducking rather than jumping. Introduces a second input axis and more variety.

### Coin Combo Multiplier
Collecting multiple items in quick succession (within ~1 second of each other) triggers a combo multiplier (×2, ×3 …) with a brief on-screen label. Resets on any gap.

### Power-Up: Speed Boost
Rare golden acorn collectible that temporarily increases speed and makes the player invincible for 3 seconds, with a screen-edge glow effect.

### Power-Up: Shield
Rare collectible that absorbs one obstacle hit before breaking, giving the player a second chance.

### Difficulty Tiers
Split the speed curve into named tiers — Meadow → Forest → Deep Forest → Night Run — each with a distinct background tint, slightly different music tempo, and increased spawn rates. Trigger tier changes at score milestones (500 / 1500 / 3000).

---

## Visuals

### Parallax Clouds
Add a slow-moving cloud layer between the sky and the tree layers. Three or four simple ellipse-cluster clouds at 5–8% of game speed give a much greater sense of depth without performance cost.

### Ground Detail Layer
Add animated grass tufts at the ground line that bend in the direction of movement — a cheap effect using a few short Bezier curves per tuft.

### River Entry Splash
When the player collides with a river (game over), emit a large upward water-blue particle burst from the impact point before the standard death explosion.

### Death Screen Polish
Freeze the last frame of the canvas as a blurred screenshot behind the game over overlay instead of continuing to draw the background. Creates a more cinematic pause.

---

## Mobile & Accessibility

### Swipe-Down to Duck
Detect a downward swipe gesture (touchmove delta) as a crouch input once the duck mechanic is added.

### Haptic Feedback
Call `navigator.vibrate(30)` on jump, `navigator.vibrate([40, 20, 80])` on death for supported mobile browsers.

### Reduced Motion Mode
Detect `prefers-reduced-motion: reduce` and disable the parallax scroll, particle effects, and bobbing animations, keeping only the core gameplay visible.

---

## Technical

### Sprite Caching Validation
Add a dev-mode flag (`?debug=1`) that draws all hitboxes in red and logs frame timing to the console, making it easier to tune collision feel without touching production code.

### Pause on Tab Blur
Pause the game loop when `document.visibilitychange` fires (user switches tab). Currently the `dt` clamp of `3` frames prevents large jumps on return, but a proper pause avoids any drift.

### Level Seed Sharing
Generate a short alphanumeric seed from the RNG state at game start and display it on the game over screen. Let the player copy the seed to share a run with the same obstacle layout.
