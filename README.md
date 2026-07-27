# Murmuration — a living sky

An interactive 3D flocking simulation: a murmuration of starlings wheels over a
calm alpine lake beneath a procedural mountain range, through a full day and
night. Real-time WebGL2, no dependencies, one HTML file.

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

A real 3D scene rendered in WebGL2 with hand-written GLSL — five shader programs,
no libraries, one self-contained `index.html`. A perspective camera stands at the
shore of an alpine lake and drifts slowly, so the whole world holds together with
true parallax rather than stacked 2D layers.

- **Emergent flocking in 3D** — classic boids (separation, alignment, cohesion)
  over a 3D spatial-hash grid on the CPU, streamed to the GPU as instanced
  geometry. The birds occupy real volume: they fly toward and away from the
  camera, scale with distance, and fade into aerial perspective. No scripted paths.
- **3D birds** — each starling is a faceted low-poly mesh that flaps, pitches, and
  banks into its turns along its actual flight basis, lit per-fragment
  (Blinn–Phong with an iridescent specular) by whichever of the sun or moon is up.
- **Procedural mountain vista** — layered ridgelines raised from ridged fractal
  noise, shaded by their own slope so faces alternate lit and shadowed, with a
  second fbm pass driving true crinkled relief, a ragged noise-broken snowline,
  alpenglow rim light on the crests, and per-layer atmospheric haze.
- **The lake** — a genuine ground plane at y=0, not a screen-space strip.
  Reflections come from mirroring the eye ray about the wave normal and sampling
  the same world function the sky uses, so the mountains, sun, moon and stars all
  reflect correctly; the flock is rendered into a mirrored buffer sampled through
  the wave field. Schlick Fresnel blends reflection against deep-water color.
- **Wave physics** — a wave-equation simulation in a ping-pong floating-point
  framebuffer, mapped onto the lake in world space. Wakes, splashes and ambient
  drops propagate, reflect and interfere across a deliberately calm surface.
- **Sun and moon glitter** — a physical specular lobe off the real wave normals,
  plus a broken sparkle path along the light's azimuth, so the reflection sits
  exactly beneath the sun and stretches back toward the viewer.
- **A full day** — the sky interpolates through six palette keyframes
  (night → dawn → day → golden hour → dusk → twilight) every ~84 seconds, with the
  sun and a crescent moon arcing opposite each other and procedural stars at dark.
- **Shape formation** — target shapes are rasterized to an offscreen canvas and
  sampled into per-bird targets on a plane facing the camera; a formation force
  blends against the flocking forces, with damping applied only once a bird nears
  its target so the shape resolves crisply instead of orbiting.

Runs at 60fps at full retina resolution. Needs a WebGL2-capable browser (any
current one). Open `index.html`, or serve the folder with any static file server.

---

Built with [Claude Code](https://claude.com/claude-code).
