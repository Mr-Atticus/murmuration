# Murmuration — a living sky

An interactive flocking simulation: thousands of starlings wheel over a mirror lake
through a full day/night cycle, rendered on a single HTML canvas with no dependencies.

**[Live demo →](https://a-living-sky.netlify.app)**

## Interactions

| Input | Effect |
| --- | --- |
| Move the cursor | The flock reads you as a falcon and carves away |
| Drag across the water | Leave a wake — real ripples that propagate and interfere |
| Click the sky | Scatter burst |
| Click the water | Splash |
| `1` / `2` / `3` / `4` | Gather into a heart, star, spiral, or the word **AMAZE** |
| `Space` | Release the flock back to free flight |
| ♪ toggle (top right) | Optional generative ambient soundscape |

## How it works

Rendered entirely in WebGL2 with hand-written GLSL — five shader programs, no
libraries, one self-contained `index.html`.

- **Emergent flocking** — classic boids (separation, alignment, cohesion) over a
  spatial-hash grid on the CPU, streamed to the GPU as instanced geometry.
  No scripted paths.
- **3D birds** — each starling is a faceted low-poly mesh with flapping wings and
  banked turns, lit per-fragment (Blinn–Phong with an iridescent specular) by the
  sun or moon. Far birds fade into atmospheric haze.
- **Wave physics** — the lake runs a real wave-equation simulation in a ping-pong
  floating-point framebuffer. Wakes, splashes, and ambient drops propagate,
  reflect, and interfere; wave normals distort the reflections and catch the light.
- **Reflections & shadows** — the flock is rendered mirrored into an offscreen
  buffer that the water samples through its wave field; low birds cast soft
  shadows on the surface. Fresnel blends reflection against deep-water color, and
  a specular glitter path tracks the sun/moon.
- **A full day** — the sky interpolates through six palette keyframes
  (night → dawn → day → golden hour → dusk → twilight) every ~84 seconds, with a
  sun and crescent moon arcing opposite each other and procedural stars at dark.
- **Adaptive contrast** — each bird samples the sky gradient behind it and shades
  from pale silver (against dark sky) to dark silhouette (against the bright horizon).
- **Shape formation** — target shapes are rasterized to an offscreen canvas and
  sampled into per-bird targets; a formation force blends against the flocking
  forces with velocity damping so the birds settle crisply.

Needs a WebGL2-capable browser (any current one). Open `index.html`, or serve the
folder with any static file server.

---

Built with [Claude Code](https://claude.com/claude-code).
