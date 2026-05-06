# DESIGN — Artemis II: Return to the Moon

Mission Control Cinematic — a 60-second 1920×1080 explainer for NASA's Artemis II crewed lunar flyby (April 1–11, 2026).

## Palette (frozen — use literal values only; no `var()` in rendered DOM)

| Token         | Hex       | Role                                                         |
| ------------- | --------- | ------------------------------------------------------------ |
| Void black    | `#05070D` | Primary background, negative space                           |
| Deep navy     | `#0B1426` | Panel surfaces, trajectory canvas                            |
| Bone white    | `#E8EEF7` | Primary text, title, captions                                |
| Ignition      | `#FF6B35` | Burn events, warnings, hero accents (use sparingly)          |
| Telemetry     | `#4FC3F7` | Data, gauges, trajectory strokes, coordinates                |
| Lunar gold    | `#FFD166` | Moon surface, closest-approach marker, sun-lit highlights    |

- **No generic blues.** Telemetry cyan only; no Material blue, no #4285F4.
- **No full-screen linear gradients on dark backgrounds** — use radial vignettes, noise, or solids.
- Typography and strokes on thin lines: solid color only (no gradients < 4px tall).
- Alpha floors: gradient stops never below 0.15 alpha.

## Typography

- **Titles / headings** — "Space Grotesk", 500–700 weight, tight letter-spacing (−0.01em).
- **Telemetry / coordinates / timestamps / distances** — "JetBrains Mono", 400–700, `font-variant-numeric: tabular-nums`, letter-spacing 0.08em for ALL CAPS labels.
- **Captions** — "Space Grotesk" 700, 52px, bone white, on a subtle void-black drop shadow (no pill, no box).

HyperFrames embeds registered fonts automatically — declare `font-family` inline or in `<style>`; no `<link>`/`@import` tags in scene bodies.

## Motion principles

| Move              | Easing              | Duration  |
| ----------------- | ------------------- | --------- |
| Title / hero      | `expo.out`          | 1.0–1.4s  |
| Data reveal       | `power3.out`        | 0.5–0.8s  |
| Counter count-up  | `power2.out`        | 1.5–3.0s  |
| Trajectory stroke | `power2.inOut`      | 2.0–4.0s  |
| Scene crossfade   | `power2.inOut`      | 0.6s      |
| Boundary flash    | `power4.in → out`   | 0.20s     |

- All counters are deterministic. No `Date.now()`, no `Math.random()` — use seeded PRNG or timeline-driven tweens.
- Counters render in tabular-nums mono so digits don't jitter.
- Captions: fade + 6px rise over 0.14s in, hard `tl.set(opacity:0)` kill at word end.
- Starfield parallax: three depth layers at 0.12× / 0.28× / 0.45× scene-local drift.

## Scene crossfades

- Each scene sub-composition **fades IN** over its first 0.6s (opacity 0 → 1, `power2.out`).
- At the root, adjacent scenes are placed with 0.6s overlap — the incoming scene's fade-in happens while the outgoing scene still holds full opacity (the transition IS the exit).
- A full-screen white flash (`#E8EEF7` at 0.18 peak alpha, 0.20s, `power4.in → out`) pulses at each boundary midpoint — cinematic flash-through-white shader feel without the WebGL texture-capture fragility.

## Audio

- Narration: Kokoro `bf_emma` voice, 1.0× speed, single track at `data-track-index="2"`.
- No music bed (keeps the Mission Control dryness).
- Captions composition reads `transcript.json` (word-level, produced by `hyperframes transcribe`).

## What NOT to do

- **No generic blues.** Only telemetry cyan `#4FC3F7`.
- **No Roboto / no Material Sans / no Inter.** Space Grotesk + JetBrains Mono only.
- **No bouncy motion.** No `back.out`, `elastic.out`, `bounce.out` anywhere. Weighted `power*` / `expo` only.
- **No full-screen linear gradients on dark backgrounds.** Use solids, radial vignettes, or noise.
- **No `Date.now()` / `Math.random()`.** All randomness seeded.
- **No emoji in text.** ASCII + middle-dot `·` separators only.
- **No `transparent` keyword in gradients.** Use `rgba(… 0)` with the target color baked in.
- **No CSS `var(--…)`** on captured elements — literal hex values only.
- **No `class="clip"` on scene root divs inside standalone scene compositions** (they only get their own `data-composition-id`). Clips are for timed elements inside the scene.
- **No exit animations inside scenes** (except Scene 7). The crossfade at the root is the exit.
- **Video never animated** via `width`/`height`/`top`/`left` — none of our scenes use video, so N/A.
- **Pixel sizes** on thin lines: minimum 1.5px in shader-visible areas.
- **No copyrighted NASA imagery.** All visuals are SVG/CSS/Canvas primitives — silhouettes, strokes, procedural textures.
