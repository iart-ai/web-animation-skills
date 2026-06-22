---
name: ascii-animation
description: This skill should be used when the user asks to "make an ASCII animation", "build a terminal/CLI intro or loader", "convert an image or video to ASCII art", "add an ASCII shader/post-effect to a canvas or Three.js scene", "create retro/hacker text-character motion", or "animate text characters with a brightness ramp". Covers generative ASCII fields, image/video/3D-to-ASCII, and animated character art for both web and terminal.
version: 0.1.0
---

# ASCII Animation

Render motion entirely with text characters. ASCII output is extremely lightweight, distinctive, and works in browsers (`<pre>`/canvas), terminals (ANSI), and over any 3D scene (Three.js `AsciiEffect`).

## When to use

- Build terminal/CLI intros, loaders, banners, or a retro/hacker aesthetic.
- Convert an image, video frame, or 3D scene into animated ASCII.
- Add an ASCII post-effect over an existing canvas/WebGL render.
- Create generative text fields (plasma, sine waves, noise, tunnels).

## Core concept: the brightness ramp

Map luminance (0..1) to a character whose ink density matches. Order characters dark-to-light. Pick the index with `Math.round(lum * (ramp.length - 1))`.

Common ramps (dark to light):
- Short (10): ` .:-=+*#%@`
- Medium (16): ` .'\`^",:;Il!i><~+_-?][}{1)(|/tfjrxnuvczXYUJCLQ0OZmwqpdbkhao*#MW&8%B@$`  truncated — see table below.
- Standard 70-level (Paul Bourke), best for photos:
  `` $@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\|()1{}[]?-_+~<>i!lI;:,"^`'.  `` (reverse for dark-on-light).

Compute relative luminance from sRGB (perceptual):
```js
const lum = (0.2126 * r + 0.7152 * g + 0.0722 * b) / 255; // 0..1
```

Invert when drawing dark text on a light background: `lum = 1 - lum`.

## Character cell aspect correction (the #1 gotcha)

Monospace character cells are taller than wide — roughly **0.5 width:height**. Sampling a square pixel grid produces a vertically stretched image. Correct by sampling **fewer rows than columns**: for a target of `cols` characters wide, use `rows = Math.round(cols * (imgH / imgW) * fontAspect)` where `fontAspect ≈ 0.5`. Equivalently, when drawing to an offscreen canvas, set its height to `cols * aspect * 0.5`.

## Web rendering: `<pre>` vs canvas

- **`<pre>` + textContent**: simplest. One string with `\n` per row. Fine up to ~120×60 chars at 30fps. Set `white-space: pre; font-family: monospace; line-height: 1;`.
- **Canvas `fillText`**: needed for per-character color, larger grids, or 60fps. Draw each char at `x * cellW, y * cellH`. Faster than thousands of DOM nodes.

Generative `<pre>` field (plasma):
```js
const pre = document.querySelector('pre');
const COLS = 100, ROWS = 50, ramp = ' .:-=+*#%@';
function frame(t) {
  let out = '';
  for (let y = 0; y < ROWS; y++) {
    for (let x = 0; x < COLS; x++) {
      const v = Math.sin(x * 0.2 + t * 0.001)
              + Math.sin(y * 0.3 + t * 0.0013)
              + Math.sin((x + y) * 0.15 + t * 0.0007);
      const lum = (v + 3) / 6;                    // normalize -3..3 to 0..1
      out += ramp[Math.round(lum * (ramp.length - 1))];
    }
    out += '\n';
  }
  pre.textContent = out;
  requestAnimationFrame(frame);
}
requestAnimationFrame(frame);
```

## Image / video to ASCII

Draw the source to a small offscreen canvas at `cols × rows`, read pixels with `getImageContext().getImageData`, then map each pixel to a character. For video, repeat per frame from a `<video>` element.

```js
function videoToAscii(video, cols = 120) {
  const aspect = video.videoHeight / video.videoWidth;
  const rows = Math.round(cols * aspect * 0.5);   // cell aspect correction
  const cv = document.createElement('canvas');
  cv.width = cols; cv.height = rows;
  const ctx = cv.getContext('2d', { willReadFrequently: true });
  const ramp = ' .:-=+*#%@', pre = document.querySelector('pre');
  (function tick() {
    ctx.drawImage(video, 0, 0, cols, rows);
    const { data } = ctx.getImageData(0, 0, cols, rows);
    let out = '';
    for (let i = 0; i < data.length; i += 4) {
      const lum = (0.2126*data[i] + 0.7152*data[i+1] + 0.0722*data[i+2]) / 255;
      out += ramp[Math.round(lum * (ramp.length - 1))];
      if (((i / 4) + 1) % cols === 0) out += '\n';
    }
    pre.textContent = out;
    requestAnimationFrame(tick);
  })();
}
```

For Node image→ASCII, see `scripts/img-to-ascii.mjs`.

## 3D-to-ASCII with Three.js

`AsciiEffect` wraps a renderer and renders any scene as ASCII into a DOM element. Render through the effect, not the renderer.

```js
import { AsciiEffect } from 'three/addons/effects/AsciiEffect.js';
const effect = new AsciiEffect(renderer, ' .:-=+*#%@', { invert: true });
effect.setSize(innerWidth, innerHeight);
effect.domElement.style.color = '#0f0';
effect.domElement.style.backgroundColor = 'black';
document.body.appendChild(effect.domElement);
// in loop: effect.render(scene, camera);  // NOT renderer.render
```

## Terminal / CLI animation

Loop with ANSI escape codes: hide the cursor, move to home, print the frame, throttle to 12–24 fps. Show the cursor again on exit.

```js
const ESC = '\x1b[';
process.stdout.write(ESC + '?25l');               // hide cursor
function frame(t) {
  process.stdout.write(ESC + 'H');                // cursor to top-left
  // build and write rows...
}
const id = setInterval(() => frame(Date.now()), 1000 / 20);
process.on('SIGINT', () => {
  clearInterval(id);
  process.stdout.write(ESC + '?25h' + ESC + '2J'); // show cursor, clear
  process.exit();
});
```
Use `ESC + '2J'` to clear the whole screen, `ESC + 'H'` for home (cheaper per frame than clearing). Color with `\x1b[38;2;R;G;Bm` (truecolor) and reset with `\x1b[0m`.

## Quick reference

| Need | Approach |
|------|----------|
| Simple generative field | `<pre>` + `textContent`, sine/noise → ramp |
| Photo fidelity | 70-level Bourke ramp, luminance from sRGB weights |
| Per-char color / 60fps | Canvas `fillText` per cell |
| Video | `<video>` → offscreen canvas → `getImageData` per frame |
| 3D scene | Three.js `AsciiEffect.render(scene, camera)` |
| Terminal | ANSI `\x1b[H` home + throttle 12–24fps, hide cursor |
| Aspect fix | `rows = cols * imgAspect * 0.5` |

## Reference files

- `references/rendering.md` — Full brightness ramp tables (10/70/extended), pixel sampling math and cell aspect correction, `<pre>` vs canvas tradeoffs with code, ANSI terminal frame loop with truecolor, and complete `AsciiEffect` wiring.
- `scripts/img-to-ascii.mjs` — Runnable Node script that converts a PNG/JPG file to ASCII text, with `--cols`, `--invert`, and `--ramp` flags.
