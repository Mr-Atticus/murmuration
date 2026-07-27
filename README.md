# Murmuration — a living sky

An interactive flocking simulation: thousands of starlings wheel over a mirror lake
through a full day/night cycle, rendered on a single HTML canvas with no dependencies.

**[Live demo →](https://a-living-sky.netlify.app)**

## Interactions

| Input | Effect |
| --- | --- |
| Move the cursor | The flock reads you as a falcon and carves away |
| Click | Scatter burst |
| `1` / `2` / `3` / `4` | Gather into a heart, star, spiral, or the word **AMAZE** |
| `Space` | Release the flock back to free flight |
| ♪ toggle (top right) | Optional generative ambient soundscape |

## How it works

- **Emergent flocking** — classic boids (separation, alignment, cohesion) over a
  spatial-hash grid, so 900–2,400 birds stay at 60 fps. No scripted paths.
- **A full day** — the sky interpolates through six palette keyframes
  (night → dawn → day → golden hour → dusk → twilight) every ~84 seconds, with a
  sun and crescent moon arcing opposite each other and stars that emerge at dark.
- **Adaptive contrast** — each bird samples the sky luminance behind it and shades
  from pale silver (against dark sky) to dark silhouette (against the bright horizon).
- **Shape formation** — target shapes are rasterized to an offscreen canvas and
  sampled into per-bird targets; a formation force blends against the flocking
  forces with velocity damping so the birds settle crisply.
- **The lake** — the bottom fifth mirrors the flock with ripple distortion and a
  glitter column under the sun/moon.

Everything is one self-contained `index.html`. Open it, or serve the folder with
any static file server.

---

Built with [Claude Code](https://claude.com/claude-code).
