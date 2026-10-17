# Verification report
Verified here (offline sandbox, no browser, no network):
- FBX parsed by a custom reader: 133 meshes, 30 materials, +Z front bumper, ~4.6 units long, 4 separate wheel meshes (FL, FR, BR, BL), calipers, spoiler/bumper/skirt meshes; all referenced textures exist in `assets/`.
- HDR/EXR→RGBE and asphalt conversions ran; sun direction measured from the brightest HDRI pixel.
- `index.html` module passes `node --check` (syntax only).
- Timeline maths run in Node: no NaN in camera path, camera never enters the car's clearance box (closest ≈2.5 m), speed/path/corner tables correct (82° left-hander at ≈73.7–77 s, max accel ≈1.5 g).

NOT verified (could not run WebGL/audio/recorder here): FBX actually loading in a browser, materials/clearcoat look, wheel pivots visually correct, label placement, clipping cutaway look, framing in every shot, audio loops sounding seamless, MediaRecorder output, mobile performance. Expect to need small tweaks after a first real run — open Debug (⚙ → Debug) and the console (`window.__jesko.diag`) to see what loaded and what was found.
