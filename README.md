# Koenigsegg Jesko Attack — "How Does a Hypercar Get Pushed Toward the Road?"
Three.js 9:16 explainer, 80 s, 11 scenes, one master timeline. No build step.

## Run
```bash
cd <this folder>
python3 -m http.server 8000
# open http://localhost:8000   (HTTP is required: browsers block local-file access to the FBX/textures)
```
Phone on the same Wi-Fi: open `http://<computer-LAN-IP>:8000`. **Internet is needed once** — three.js 0.180.0 loads from jsDelivr (import map in `index.html`). Tap ▶ once: browsers need a tap before sound starts.

## Controls (⚙ opens the panel)
Play/Pause · Restart · scrubber (scrub forward/back any time) · scene buttons 1–11 · Airflow · Pressure · Force vectors · Labels · Underbody cutaway · Simple mode · Inspect/orbit (timeline keeps running; car stays followed) · Reset camera · Debug · Sound/volume · Voice preview · speed 0.5/1/2× · quality Low/Med/High · Record. Keys: Space, ←/→ (±2 s).

## Recording
"Record video" restarts at 0:00, captures the WebGL canvas (`captureStream(30)`) plus the Web Audio mix, and downloads on completion. It runs in real time (80 s) — keep the tab visible. Format = best the browser supports (tries MP4/H.264+AAC, then WebM VP9/VP8+Opus); the status line states the actual format. 1080×1920 or 720×1280. Highlight tags, curve and bars are drawn inside WebGL so they are in the file; DOM controls and debug are not.

## Assets (`assets/`)
| File | Role |
|---|---|
| `FINAL_MODEL_AT.fbx` + `T_*.png`, `common_carbon05_*.png` | Your Jesko Attack and its textures (loaded with `FBXLoader`). `*_RME.png` are repacked at load for roughness/metalness |
| `sky.hdr` | Your `kloppenheim_03_puresky_2k.exr`, converted to RGBE (values clamped at 3000) — lighting, reflections, sky |
| `asphalt_diff.jpg`, `asphalt_nor.jpg`, `asphalt_rough.jpg` | Your asphalt maps converted from the 2k EXR/JPG (diffuse resized 2048). Displacement webp and .blend are not used |
| `engine_loop_low.mp3`, `engine_loop_high.mp3` | Two seamless sustained loops cut from your MP3 (≈14–25 s and ≈26–33 s). Pitch follows speed, blended by speed |

Total ≈ 27 MB (FBX 16 MB, HDRI 5 MB).

## What is real vs. illustrative
Real: the car (all four wheels are separate meshes, wrapped in steer/roll pivots; they roll by distance/radius and the front pair steers in the corner), wing, splitter and bumpers used as anchors, HDRI, asphalt, your engine recording.
Illustrative (procedural, not CFD, not factory data): streamlines/beads (shaped from the car's measured silhouette), pressure glows, force arrows, balance line, F∝v² curve, 250/290 km/h bars. Bar heights are proportional to 700 and 1,000. The wing's upward air deflection is drawn as an explanation, not a simulation. The model's wing is treated as fixed; no flap/wing articulation is animated. The cutaway is a clipping plane through the real model (interior is the model's own).
Published figures used: 700 kg @ 250 km/h, 1,000 kg @ 290 km/h (from your narration; matches the Koenigsegg spec page figures I was given — not re-checked online here). The 1,400 kg maximum from the original brief is **not** used because your script doesn't include it. "Kg" is a force-equivalent, not added mass.

## Known limitations
Not run in a browser in my environment (see VERIFICATION). Engine sound comes from a YouTube screen recording, so it may contain other audio/compression and isn't a clean isolated Jesko sample. Fog colour is a hand-picked match to the HDRI horizon. Asphalt is one 5 m tile repeated.
