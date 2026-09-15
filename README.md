# TIMBERHALL — Digital Studio (single-file portfolio)

A responsive, single-file portfolio for a fictional digital studio. It opens with a
real-time **Three.js** 3D timber lobby, then continues into an editorial studio index.

> One deployable file: **`index.html`**. No framework, build step, server function,
> secret, or environment variable required. Works from a GitHub Pages repo subpath
> because all asset references are relative or embedded.

---

## Run it

Serve over HTTP (ES modules + import maps do **not** work from `file://`):

```bash
# any of these from the repo root
python3 -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000/`.

---

## The experience

- **Full-viewport 3D lobby** built from procedural geometry, canvas-painted wood
  textures, shadow-casting lights, exponential fog, and a custom post-processing pass.
- **Four interaction targets**, each with a distinct camera state, one focused
  interaction, and a reliable return path (`Esc`, the floating **RETURN TO ROOM**
  button, or each panel's own close control):
  - **Portfolio CRTs** — cycle case studies on a canvas-rendered CRT.
  - **Arcade cabinet** — a tiny playable *DODGE* mini-game.
  - **Basketball hoop** — physics-based shot with adjustable power.
  - **Sliding door** — slides open and travels the camera into the studio index.
- **Menu** is presented as a tilted physical plate in an accessible modal dialog while
  keeping normal keyboard/pointer access to its anchor links.
- **Editorial page**: manifesto, masonry work grid (canvas thumbnails), capability
  list, people + demonstrational contact form, and footer.

## Motion & visual system

- Monochrome palette with one warm signal color (`--signal: #ff5a1f`).
- Compact monospaced labels (**Space Mono**) + confident grotesk headlines
  (**Space Grotesk**).
- **Custom analog-video shader** (`AnalogShader`): grain, scanlines, chromatic drift,
  and an occasional head-switching tear band.
- Camera uses spring-based interpolation with damped secondary motion.
- Scroll-triggered reveals via `IntersectionObserver`.
- Honors `prefers-reduced-motion` (softens the video effect, disables reveals/smooth
  scroll) and keeps all text in the DOM.

## Performance & accessibility

- Device pixel ratio capped at **1.75**; an adaptive check lowers DPR if the average
  frame time stays high. Rendering pauses when the lobby scrolls out of view.
- Semantic landmarks (`header`, `main`, `section`, `footer`), labelled controls,
  visible `:focus-visible` states, a skip link, and explicit close/return controls.
- Layout verified for desktop and a narrow **390 × 844** mobile viewport.

---

## External dependencies (documented)

Loaded at runtime via CDN — no install step:

| Dependency | Source |
| --- | --- |
| three @0.161.0 (module) | `https://cdn.jsdelivr.net/npm/three@0.161.0/build/three.module.js` |
| three addons (`EffectComposer`, `RenderPass`, `ShaderPass`) | `https://cdn.jsdelivr.net/npm/three@0.161.0/examples/jsm/` |
| Space Grotesk + Space Mono | Google Fonts (`fonts.googleapis.com`) |

All are declared in the `<head>` import map / `@import`. If you need a fully
offline build, vendor these files next to `index.html` and update the paths.

---

## Verification checklist

Served over local HTTP and checked:

- [x] Initial render (loader → lobby) with **no console errors**.
- [x] Every primary lobby state (CRTs, arcade, hoop, door) and its return path.
- [x] Menu open/close (button, overlay click, `Esc`) and focus handling.
- [x] Anchor navigation to `#manifesto`, `#work`, `#capabilities`, `#studio`, `#contact`.
- [x] Responsive layout at desktop and 390 × 844.
- [x] `prefers-reduced-motion` behavior.

### Screenshot for this README

Capture a real screenshot from the running server, e.g.:

```bash
npx playwright screenshot --viewport-size=1280,800 http://localhost:8000/ screenshot.png
```

Then reference it here:

```md
![Timberhall lobby](./screenshot.png)
```
