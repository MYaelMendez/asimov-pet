# asimov-cad — a Hermes pet rendered from the real robot

Not an illustration of a humanoid. **1,007,041 triangles of Menlo Research's
Asimov-1 CAD**, rasterised on an RTX 3050 at 192×208, nine animation states,
six frames each. Same input, same bytes.

```
atlas   1536 × 1872 RGBA  ·  8 cols × 9 rows of 192×208
frames  6 per state (columns 6–7 unused, per the petdex contract)
loop    1100 ms
size    ~139 KB lossless WebP
```

## Install

Copy the `asimov-cad/` folder into your Hermes pets directory, then select it:

```bash
# Windows
copy /E asimov-cad %LOCALAPPDATA%\hermes\pets\asimov-cad
# macOS / Linux
cp -r asimov-cad ~/.hermes/pets/asimov-cad

hermes pets select asimov-cad
hermes pets doctor          # → ✓ ready
```

Or unzip `asimov-cad.zip` directly into `pets/`.

## The nine states

| row | state | what it does |
|---|---|---|
| 0 | idle | gentle sway, breathing |
| 1 | running-right | policy gait, facing right |
| 2 | running-left | policy gait, facing left |
| 3 | waving | shoulder pitch + roll raised, oscillating |
| 4 | jumping | vertical arc |
| 5 | failed | a slump that settles |
| 6 | waiting | slower sway |
| 7 | running | policy gait in place |
| 8 | review | lean forward |

The walk rows use a **real locomotion policy trace** — Menlo's
`asimov1-locomotion-0818` ONNX running against MuJoCo contact. The robot walks
the way it walks in our films, not the way an animator guessed it should.

## Regenerate it yourself

The atlas is deterministic. `asimov_pet.py` rebuilds it byte-for-byte from the
same CAD and the same trace:

```bash
pip install tinycuda[cuda] numpy pillow
python asimov_pet.py --model-dir <asimov-urdf-dir> --out ./asimov-cad \
    --trace walk.json --head 255,214,0
```

Requires an NVIDIA GPU with CuPy. **No OpenGL ICD needed** — that is the point:
on an Optimus laptop the GL path lands on the integrated GPU, and CUDA does not.

A frame with fewer than 500 opaque pixels aborts the build. An off-camera pose
must never ship as a blank pet.

## Licence — read this before redistributing

**The atlas is a rendered derivative of Menlo Research's Asimov-1 CAD, which is
licensed CERN-OHL-S-2.0 (strongly reciprocal).** The atlas therefore carries
CERN-OHL-S-2.0, not the Apache-2.0 of our own code. See `LICENSE` and
`THIRD_PARTY_NOTICES.md`.

- **The generator** (`asimov_pet.py`) is Apache-2.0. Our tool, our terms.
- **The atlas** (`spritesheet.webp`) is CERN-OHL-S-2.0, following upstream.
- **No CAD is redistributed here.** The meshes are fetched from Menlo's public
  repository at generation time, exactly as `tinygpu fetch` does.

No endorsement by Menlo Research, Nous Research, NVIDIA or CERN is claimed or
implied.

## Provenance

```
renderer   tinycuda / rtx_raster — packed uint64 depth+id atomicMin, race-free
geometry   menloresearch/asimov-1 · sim-model/asimov_1_25dof · 26 links, 25 joints
motion     Menlo/asimov1-locomotion-0818 (ONNX) + MuJoCo 4.0.1
device     NVIDIA GeForce RTX 3050 6GB Laptop · cc 8.6 · CUDA
verified   all 9 rows 6/6 distinct frames · min 4,328 opaque px
```

Every number above was measured, not estimated.

`>_æ://` · HUMAN://ROOT · #opensourceware
