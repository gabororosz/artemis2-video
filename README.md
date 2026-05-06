# Artemis II: Return to the Moon

A cinematic 60-second 1920×1080 explainer video about NASA's **Artemis II** crewed lunar flyby mission (April 1–11, 2026), built with [HyperFrames](https://hyperframes.heygen.com/) — an HTML-to-video composition framework powered by GSAP.

## What's this project all about

A "Mission Control Cinematic" visual piece that walks through the mission timeline in seven scenes:

1. **Title card** — Artemis II launch identity
2. **Launch** — SLS liftoff telemetry
3. **TLI burn** — trans-lunar injection trajectory
4. **Outbound coast** — 4-day cruise to the Moon
5. **Lunar flyby** — closest approach (hero shot)
6. **Free-return** — figure-8 trajectory home via lunar gravity assist
7. **Splashdown** — Pacific Ocean recovery, mission complete

**Stack**

- **HyperFrames** + GSAP 3.14 timelines for scene animation
- **Kokoro-82M** TTS (`bf_emma` voice) for narration
- **whisper.cpp** for word-level caption transcription
- Sub-compositions per scene (`compositions/scene-*.html`) mounted from `index.html`

**Visual identity**

- Palette: `#05070D` void black · `#0B1426` deep navy · `#E8EEF7` bone white · `#FF6B35` ignition orange · `#4FC3F7` telemetry cyan · `#FFD166` lunar gold
- Type: Space Grotesk (titles) + JetBrains Mono (telemetry)

## Project structure

```
.
├── index.html              # root composition (timeline + chrome + audio)
├── compositions/
│   ├── scene-1.html ... scene-7.html
│   └── captions.html       # per-word caption overlay
├── narration.txt           # narration script
├── narration.wav           # generated TTS audio
├── transcript.json         # whisper word-level timestamps
├── meta.json               # project metadata
├── hyperframes.json        # HyperFrames config
├── DESIGN.md               # visual design spec
└── AGENTS.md / CLAUDE.md   # agent instructions
```

## Install dependencies

You need **Node.js 18+** and **Python 3.12+** (for the TTS pipeline).

```bash
# 1. HyperFrames CLI runs via npx — no global install required.
#    Pull it once to warm the cache:
npx hyperframes --version

# 2. ffmpeg (required for transcription / rendering)
brew install ffmpeg          # macOS
# sudo apt install ffmpeg    # Debian/Ubuntu

# 3. Python venv for Kokoro TTS (only needed if regenerating narration.wav)
python3.12 -m venv .ttsenv
source .ttsenv/bin/activate
pip install kokoro-onnx soundfile
deactivate
```

## How to run

All commands run from the project root.

```bash
# Live preview in the browser (Studio editor with scrub timeline)
npx hyperframes preview

# Render the final MP4 (writes to ./out/)
npx hyperframes render

# Validate compositions (run after every edit)
npx hyperframes lint
npx hyperframes validate
```

### Regenerating narration & captions

```bash
# Regenerate TTS from narration.txt (uses .ttsenv)
PATH="$PWD/.ttsenv/bin:$PATH" npx hyperframes tts --voice bf_emma

# Re-transcribe to word-level JSON for captions
npx hyperframes transcribe narration.wav --model small.en
```

## License

Private project — for educational / portfolio use.
