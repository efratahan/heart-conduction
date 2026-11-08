# Heart conduction model: attribution and provenance

## Anatomy
- **Source:** BodyParts3D, © The Database Center for Life Science (DBCLS), Japan.
  https://dbarchive.biosciencedbc.jp/en/bodyparts3d/
- **Licence:** Creative Commons Attribution-ShareAlike 2.1 Japan (CC BY-SA 2.1 JP).
  https://creativecommons.org/licenses/by-sa/2.1/jp/deed.en
- **Files used:** `partof_BP3D_4.0_obj_99.zip`. Only the heart and great-vessel element files
  (FJxxxx.obj) were fetched, by HTTP range requests against the zip's own index. The parts
  are the four cavities, both atrial walls, the valves, the papillary muscles, the aorta,
  pulmonary trunk, SVC, IVC, pulmonary veins (the parts next to the left atrium), the left
  main, LAD, LCx, RCA trees and the cardiac veins.
- **Changes:** converted to centimetres in a body frame (x patient's left, y superior,
  z anterior), centred, decimated and recoloured. BodyParts3D has no ventricular wall, so the
  ventricular myocardium is **reconstructed** around the real cavities:
  - left ventricle about 1.1 cm, right ventricle about 0.45 cm, and the septum is what lies
    between the two cavities;
  - trimmed above the AV-valve level, except the right ventricular outflow tract.

  The real coronary arteries lie on or within about 2–4 mm of that reconstructed surface.
  `build_anatomy.py` prints this check.
- **Derived model licence:** the model derived from BodyParts3D here (decimated meshes, reconstructed
  ventricular wall, recolouring, and the modelled conduction tissue placed on it) is likewise licensed
  CC BY-SA 2.1 Japan.
- **Share-alike:** `heart.glb`, `heart_mesh.json` and the anatomy-derived parts of `heart_data.json` are
  derivatives and are under CC BY-SA 2.1 JP.

## Conduction system
No open dataset has the conduction system as meshes (BodyParts3D part lists and the Z-Anatomy
cardiovascular model were checked, 2026-11-03). The SA node, AV node, His bundle, bundle branches,
fascicles, Purkinje fibres, the three internodal pathways and Bachmann's bundle are modelled as 3D
tissue at their anatomical landmarks on the BodyParts3D heart.

## Simulation
`sim.js`, `index.src.html` and `build_anatomy.py` were written for this project. The ECG is
computed from the simulated tissue (activation → transmembrane potential → heart dipole →
lead projection). No waveform is drawn by hand.

## Size
- `heart.glb`: about 1.2 MB
- `heart_mesh.json`: about 1.7 MB (the same GLB, base64; the artifact host does not serve `.glb`/`.bin`)
- `heart_data.json`: about 0.2 MB
- `index.html`: about 70 KB

All of these are small enough to commit. The raw BodyParts3D OBJs (8.7 MB) stay in
`data/bp3d/` (gitignored); `build_anatomy.py` rebuilds everything from them.
