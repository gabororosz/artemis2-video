Build a HyperFrames composition titled "Artemis II: Return to the Moon" — a cinematic 60-second explainer video (16:9, 1920x1080) visualizing NASA's Artemis II crewed lunar flyby mission (April 1–11, 2026). VISUAL IDENTITY Style: "Mission Control Cinematic" — dark deep-space canvas with precision data overlays, inspired by NASA flight dynamics consoles and cinematic space documentaries.

Palette: #05070D (void black), #0B1426 (deep navy), #E8EEF7 (bone white), #FF6B35 (ignition orange), #4FC3F7 (telemetry cyan), #FFD166 (lunar gold)

Typography: "Space Grotesk" for titles/headings, "JetBrains Mono" for telemetry, coordinates, timestamps, distances

Motion: precise, weighted easing (power3.out, expo.out). No bouncy motion. Data counters use tabular-nums. Subtle starfield parallax on all scenes. SCENE BREAKDOWN (7 scenes, ~8–9s each, shader crossfade transitions) 

Scene 1 — TITLE CARD (0–8s) Hero title "ARTEMIS II" at 180px, subtitle "First Crewed Lunar Flyby in Over 50 Years" at 36px. Mission patch silhouette fades in behind. Mono datetime stamp bottom-left: "APR 01 2026 · 22:35 UTC · KSC LC-39B". 

Scene 2 — LAUNCH & HIGH EARTH ORBIT (8–16s) SLS rocket SVG silhouette with animated exhaust plume. Heading "PHASE 01 · LAUNCH + HIGH EARTH ORBIT". Ticker with live telemetry: altitude counting up, velocity in km/s, T+ mission elapsed time. Annotation: "~24h elliptical orbit for system checkouts". 

Scene 3 — TRANS-LUNAR INJECTION (16–24s) Animated orbital diagram: Earth (left), Moon (right), curved free-return trajectory drawn with SVG stroke-dashoffset animation in cyan. Label "TRANS-LUNAR INJECTION BURN · 6 MIN" with flame icon at burn point. Stat card: "Δv: +3.05 km/s". 

Scene 4 — OUTBOUND COAST (24–32s) Orion capsule wireframe drifting across frame. Progress bar "EARTH → MOON" filling left-to-right over 4 days. Distance counter animating from 384,000 km down to closest-approach value. Subtle earthrise reference. 

Scene 5 — LUNAR FLYBY (32–42s) — HERO MOMENT Full-frame Moon with crater texture. Trajectory arc sweeps behind the far side. Pulsing marker labeled "CLOSEST APPROACH · APR 06 2026 · 6,545 km". Secondary stat: "DISTANCE FROM EARTH · 406,771 KM — FARTHEST HUMANS HAVE EVER TRAVELED". Crew name plate fades in: Wiseman · Glover · Koch · Hansen. 

Scene 6 — RETURN COAST (42–50s) Mirror of Scene 4 in reverse — trajectory arc completing the figure-8. Heading "FREE-RETURN · GRAVITY BRINGS THEM HOME". Re-entry velocity counter climbing toward 11 km/s. 

Scene 7 — SPLASHDOWN (50–60s) Pacific Ocean horizon at dawn, Orion under three parachutes. Final stat block: "10 DAYS · 1 FLYBY · 4 ASTRONAUTS · ∞ AMBITION". Closing title "APR 11 2026 · PACIFIC OCEAN · MISSION COMPLETE". Fade to black on "NEXT: ARTEMIS III — BOOTS ON THE MOON". TECHNICAL

Generate a DESIGN.md before writing any HTML with the palette, typography, and "What NOT to Do" list (no generic blues, no Roboto, no bouncy easing, no full-screen linear gradients on dark backgrounds).

Use sub-compositions for each scene (scene-1.html through scene-7.html).

Shader crossfade transitions between scenes (~0.6s each).

All data counters deterministic (seeded PRNG if needed, no Date.now).

Run npx hyperframes lint and npx hyperframes validate before finalizing.

Add a TTS narration track using the hyperframes-cli skill with voice "bf_emma" or equivalent authoritative documentary voice. Captions synced per-word, bottom-center, bone-white on void black with subtle drop shadow.