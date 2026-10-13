**MUon System for Interesting Collision** (MuSIC) v2.1: MuSIC_v2 with the nozzles removed
- Identical to MuSIC_v2 except for the beamline:
  - the tungsten/BCH2 nozzles (`Nozzle_10deg_v1.xml`) and the `NozzleRegion` are removed
  - the beampipe (`Beampipe_Be_r22_v01.xml`) is a straight beryllium tube, 0.5 mm thick, inner radius 22 mm, over |z| < 6 m, filled with vacuum
- `Nozzle_zmax` (beampipe length) and `Nozzle_kink_z` (Inner Tracker support cone) remain as shape constants
- Compact file: [./MuSIC_v2.1.xml](./MuSIC_v2.1.xml)
