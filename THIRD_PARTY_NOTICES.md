# Third-party notices

This pet is a small route to other people's large work. That is stated rather
than implied. **No endorsement is claimed from Menlo Research, Nous Research,
NVIDIA, or CERN.**

---

## Menlo Research — the robot

The Asimov-1 humanoid CAD is authored and published by **Menlo Research** under
**CERN-OHL-S-2.0** (CERN Open Hardware Licence Version 2, Strongly Reciprocal).

- https://github.com/menloresearch/asimov-1
- `sim-model/asimov_1_25dof/` — `urdf.json`, `asimov_1_25dof.urdf`, `meshes/*.STL`
- `HARDWARE-LICENSE.txt` upstream — the licence reproduced in `asimov-cad/LICENSE`
- https://docs.menlo.ai/asimov/1/overview

**The spritesheet is a rendered derivative of that CAD.** CERN-OHL-S is strongly
reciprocal: a derivative must carry the same licence and make the Source
available. This package therefore:

1. licenses `asimov-cad/spritesheet.webp` under **CERN-OHL-S-2.0**, not Apache-2.0;
2. reproduces the upstream licence text verbatim in `asimov-cad/LICENSE`;
3. points to the Source — the public Menlo repository above — rather than
   redistributing the meshes;
4. ships the generator so anyone can regenerate the atlas from the Source.

**No CAD meshes are redistributed in this package.** They are fetched at
generation time from Menlo's public repository, exactly as `tinygpu fetch` does.

If you intend to redistribute this atlas commercially or as part of a larger
work, read CERN-OHL-S-2.0 in full and take your own advice. The strongly
reciprocal term has consequences for combined works, and this notice is not
legal advice.

---

## Menlo Research — the locomotion policy

The walk rows are driven by a trace from **`Menlo/asimov1-locomotion-0818`**,
trained and published by Menlo Research.

- https://huggingface.co/Menlo/asimov1-locomotion-0818
- sha256 `47f70691ecd5afda2933b2e6430d2375004c943552284172a2d7b28b84188a0c`
- https://github.com/menloresearch/humanoid-policy-viewer — the inference contract

The policy is **not redistributed here**. `tinypython` runs your own copy.

---

## NVIDIA — the compute

Rendered with **CuPy** on an NVIDIA GeForce RTX 3050. CUDA and the NVIDIA driver
are NVIDIA Corporation's, under their own terms. Nothing of theirs is bundled.

---

## Hermes Agent — the pet contract

The atlas geometry (192×208 frames, 8×9 grid, 6 frames per state, 1100 ms loop)
and the row taxonomy follow **Hermes Agent**'s `agent/pet/constants.py`, by
**Nous Research**.

- https://github.com/NousResearch/hermes-agent
- https://github.com/crafter-station/petdex — the gallery whose format this follows

Hermes Agent and petdex are under their own licences. This package implements
their published format; it bundles none of their code.

---

## Our own code

`asimov_pet.py` — the generator — is **Apache-2.0**, copyright Yæl Méndez.
The tool is open. The assets it renders carry their upstream terms.
