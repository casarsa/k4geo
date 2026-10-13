## Textual description of the geometry
A simplified overview to easily recreate the main elements of the geometry in FLUKA for radiation studies.
Regenerated from the XML compact files on 2026-09-10 (MuSIC_v3.1: nine ForwardTracker disks in 2 cm nozzle gaps).

All silicon "support" thicknesses below are the Silicon material assigned to passive
module/ladder elements in the XML (used as a stand-in for the carbon-fibre support
mass in some MuColl-derived models).


### Beampipe
Three coaxial volumes around the interaction point:

|Volume         | z range [cm]      | Rmin [cm]  | Rmax [cm]  | Material  |
|---------------|-------------------|------------|------------|-----------|
|Inner bore     | −595 to +595      | 0          | 0.3 → 1.78 (tapered) | beam      |
|Cavity         | −12.81 to +12.81  | 1.0 → 2.2 (on the nozzle cone) | 2.2 | beam |
|Be wall        | −13.37 to +13.37  | 2.2 → 2.3  | 2.3        | Beryllium |

The inner-bore taper is built from the same constants as the nozzle bore (see
Nozzle_10deg_v3.xml): rmax = 1 cm at the IP, narrows to 0.3 cm at |z| = 100 cm,
then widens back to 1.78 cm at |z| = 595 cm. The cavity and the 1 mm Be wall are
closed by the 10° nozzle cone, which reaches the wall's inner radius at
|z| = 12.81 cm and its outer radius at |z| = 13.37 cm; beyond that there is no
separate Be tube — the tungsten nozzle bore acts as the beampipe wall.


### Nozzle (10° MAP-style)
Symmetric on both sides of the IP. Inner tungsten cone + borated-polyethylene
middle + tungsten cladding. Each of the three radial components is interrupted
by nine 2 cm wide air gaps that house the Forward Tracker silicon disks; the
radii at each gap boundary are computed by exact linear interpolation along the
nozzle cone. A 5 mm thick Steel235 tube seated at the bore radius spans each gap
to keep the beam vacuum closed.

| Gap | z range [cm]  | Disk       |
|-----|---------------|------------|
| 0   | 540.0 – 542.0 | 0 (541)    |
| 1   | 544.0 – 546.0 | 1 (545)    |
| 2   | 549.0 – 551.0 | 2 (550)    |
| 3   | 554.0 – 556.0 | 3 (555)    |
| 4   | 564.0 – 566.0 | 4 (565)    |
| 5   | 574.0 – 576.0 | 5 (575)    |
| 6   | 579.0 – 581.0 | 6 (580)    |
| 7   | 584.0 – 586.0 | 7 (585)    |
| 8   | 588.0 – 590.0 | 8 (589)    |

Nozzle material left between consecutive gaps, in z: 2, 3, 3, 8, 8, 3, 3, 2 cm.
The nozzle then runs on for a further 5 cm to its end at |z| = 595 cm.

| Component       | z range [cm]                          | Material       |
|-----------------|---------------------------------------|----------------|
| Tungsten core   | ±6 to ±595 (10 segments per side)     | Tungsten_light |
| BCH2 layer      | ±100 to ±595 (10 segments per side)   | BCH2           |
| Tungsten clad   | ±100 to ±595 (10 segments per side)   | Tungsten_light |
| Steel inserts   | one per gap (9 per side)              | Steel235       |

Tungsten core inner radius starts at 1 cm (z = ±6 cm) and tapers down to 0.3 cm
at |z| = 100 cm, then opens to 1.78 cm at |z| = 595 cm (matching the beampipe
inner-bore profile).


### Forward Tracker (silicon disks in nozzle gaps)
Nine double-layer silicon disk stations per side, one in each nozzle gap.
Each station consists of two staggered rings (A and B) registered as separate
detector layers so that every layer contains exactly one ring
(VertexEndcap_o1_v07 constraint). Each ring carries 8 trapezoidal modules; the
two rings together tile the full azimuth with 16 modules covering 22.5° each, in
a brick-wall arrangement (ring A covers even slots, ring B covers odd slots, offset
by 2 mm in z). A station spans ~2.3 mm in z (ring A at the gap centre, ring B
2 mm further out, 330 µm each), leaving ~8 mm of clearance to the nozzle
material on either side of its 2 cm gap.

Module stack per module: 280 µm Si (passive support) + 50 µm Si (sensitive).
Total silicon thickness per layer: 330 µm.

| Disk | |z| centre [mm] | Rmin [mm] | Rmax [mm] | Layer IDs (A/B) | Origin |
|------|-----------------|-----------|-----------|-----------------|--------|
| 0    | 5410            | 25        | 509.172   | 0 / 1           | v3.1   |
| 1    | 5450            | 25        | 512.197   | 2 / 3           | v3     |
| 2    | 5500            | 25        | 515.977   | 4 / 5           | v3.1   |
| 3    | 5550            | 25        | 519.757   | 6 / 7           | v3.1   |
| 4    | 5650            | 25        | 527.318   | 8 / 9           | v3     |
| 5    | 5750            | 25        | 534.879   | 10 / 11         | v3.1   |
| 6    | 5800            | 25        | 538.659   | 12 / 13         | v3.1   |
| 7    | 5850            | 25        | 542.439   | 14 / 15         | v3     |
| 8    | 5890            | 25        | 545.464   | 16 / 17         | v3.1   |

Each disk has 8 modules in ring A (phi0 = π/16) and 8 modules in ring B
(phi0 = 3π/16, zstart + 2 mm). The detector is reflected to cover both ±z sides
(`reflect="true"`), giving 18 layers × 2 sides = 36 active layers in total.
Readout: `ForwardTrackerCollection` (same bit-field as GlobalTrackerReadoutID).


### Vertex Barrel layers (5 single layers)
Silicon thickness: 190e-3 mm (50e-3 sensor + 140e-3 support)

Each layer is built from ladders running the full length in z. A ladder carries a
single 260 mm long passive silicon support and, on its outer face, 10 sensitive
silicon sensors of 26 mm each tiling that length. Sensor width equals the ladder
width and grows with radius.

|ID | R [mm]    | Zmax [mm] | Ladders | Sensors/ladder | Sensor w x l x t [mm] |
|---|-----------|-----------|---------|----------------|-----------------------|
|0  | 29        | 130       | 16      | 10             | 13 x 26 x 0.050       |
|1  | 40        | 130       | 15      | 10             | 18 x 26 x 0.050       |
|2  | 50        | 130       | 15      | 10             | 23 x 26 x 0.050       |
|3  | 73        | 130       | 21      | 10             | 24 x 26 x 0.050       |
|4  | 101       | 130       | 29      | 10             | 24 x 26 x 0.050       |

Total: 960 sensors. Sensor centres run from z = -117 mm to +117 mm in 26 mm
steps. The sensor index is written to the `sensor` field of the readout ID, the
ladder index to `module`.


### Vertex Endcap disks (4 single disks per side)
Silicon thickness: 330e-3 mm (50e-3 sensor + 280e-3 support)

|ID | Z [mm]    | Rmin [mm] | Rmax [mm] |
|---|-----------|-----------|-----------|
|0  | 180       | 34.7      | 112       |
|1  | 230       | 43.5      | 112       |
|2  | 298       | 55.5      | 112       |
|3  | 366       | 67.5      | 112       |


### Inner Tracker Barrel layers
Silicon thickness: 200e-3 mm (100e-3 sensor + 100e-3 r/o ASIC)
Aluminium thickness: 250e-3 mm (200e-3 power-bus conductor + 50e-3 FPC metal)

|ID | R [mm]    | Zmax [mm] |
|---|-----------|-----------|
|0  | 164       | 481.6     |
|1  | 354       | 481.6     |
|2  | 554       | 692.3     |


### Inner Tracker Endcap disks (7 per side)
Silicon thickness: 200e-3 mm
Aluminium thickness: 250e-3 mm

|ID | Z [mm]    | Rmin [mm] | Rmax [mm] |
|---|-----------|-----------|-----------|
|0  | 604       | 116       | 405       |
|1  | 888       | 166       | 555       |
|2  | 1173      | 201       | 555       |
|3  | 1457      | 225       | 555       |
|4  | 1741      | 249       | 555       |
|5  | 1946      | 266       | 555       |
|6  | 2190      | 287       | 555       |


### Outer Tracker Barrel layers
Silicon thickness: 200e-3 mm
Aluminium thickness: 250e-3 mm

|ID | R [mm]    | Zmax [mm] |
|---|-----------|-----------|
|0  | 819       | 1264.2    |
|1  | 1153      | 1264.2    |
|2  | 1486      | 1264.2    |


### Outer Tracker Endcap disks (4 per side)
Silicon thickness: 200e-3 mm
Aluminium thickness: 250e-3 mm

|ID | Z [mm]    | Rmin [mm] | Rmax [mm] |
|---|-----------|-----------|-----------|
|0  | 1410      | 617.5     | 1430.2    |
|1  | 1667      | 617.5     | 1430.2    |
|2  | 1933      | 617.5     | 1430.2    |
|3  | 2190      | 617.5     | 1430.2    |


### Calorimeter Barrel
Polyhedron: 12 sides (Rmin is the inscribed-circle radius).

|ID    | Rmin [mm] | Rmax [mm] | Zmax [mm] | Layers | Sensor (per layer)             | Other material (per layer)               |
|------|-----------|-----------|-----------|--------|--------------------------------|------------------------------------------|
|ECAL  | 1690      | 1960      | 2210      | 6      | 40 mm PbF2 (LeadDifluoride)      | 1 mm Si + 3 mm siPCBMix + 1 mm Air       |
|HCAL  | 2902      | 4756      | 2509      | 70     | 3 mm Polystyrene               | 20 mm Steel235 + 0.1 mm Cu + 0.7 mm PCB + 0.5 mm Steel235 + 2.7 mm Air |

ECAL is a homogeneous PbF2 (CRILIN) calorimeter: the 40 mm crystal is the
sensitive medium and there is no tungsten radiator. Total ECAL radial depth
= 6 × 45 mm = 270 mm.
Total HCAL radial depth = 70 × 26.5 mm = 1855 mm.

The HCAL iron absorbers (20 mm Steel235 per layer + 0.5 mm trim slices) also
provide the magnetic-field return: ~1400 mm of iron per barrel stave.


### Calorimeter Endcap
Polyhedron: 12 sides.

|ID    | Rmin [mm]           | Rmax [mm] | Zmin [mm] | Zmax [mm] | Layers | Sensor (per layer)          | Other material (per layer)               |
|------|---------------------|-----------|-----------|-----------|--------|-----------------------------|------------------------------------------|
|ECAL  | 310                 | 1960      | 2307      | 2577      | 6      | 40 mm PbF2 (LeadDifluoride)   | 1 mm Si + 3 mm siPCBMix + 1 mm Air       |
|HCAL  | 320 → 499 (5 steps) | 4756      | 2579      | 4434      | 70     | 3 mm Polystyrene            | 20 mm Steel235 + 0.1 mm Cu + 0.7 mm PCB + 0.5 mm Steel235 + 2.7 mm Air |

HCAL endcap has a conical inner cutout to clear the nozzle: the inner radius
steps from 320 mm at the front face (z = 2579 mm) to 499 mm at the back face
(z = 4434 mm) in 5 equal radial steps (≈35.8 mm each). 14 layers occupy each
step.


### Solenoid
Vacuum tank with steel walls and a single aluminium coil:

|ID                  | Rmin [mm] | Rmax [mm] | Zmax [mm] | Material               |
|--------------------|-----------|-----------|-----------|------------------------|
|Tank inner wall     | 2055      | 2135      | 2509      | 80 mm Steel235         |
|Coil                | 2247.5    | 2670.5    | 2280      | 423 mm Aluminium       |
|Tank outer wall     | 2782      | 2862      | 2509      | 80 mm Steel235         |

The volume between coil and tank walls is filled with Vacuum.

**Magnetic field** (modelled as an axial DD4hep `solenoid` field with two
cylindrical regions, no field outside):

| Region                                                          | B    |
|-----------------------------------------------------------------|------|
| r < 2902 mm and \|z\| < 2509 mm (tracker, ECAL, solenoid bore)  | +5 T |
| 2902 < r < 4756 mm and \|z\| < 2509 mm (HCAL barrel iron)       | −2 T |
| Elsewhere (HCAL endcap, yoke volume, beyond tracker z)          | 0    |

Because the iron has been removed from the yoke, the magnetic-flux return
is approximated by the HCAL barrel iron, which is treated as the return-yoke
material. The HCAL endcap and the muon-yoke volumes carry no field in this
simplified model.


### Muon System (formerly Return Yoke)
Polyhedron: 12 sides. **No iron absorber** in this version — the iron mass has
been removed from the simulation; the RPC chambers are kept in their original
geometric positions by replacing each former iron slab with an equal-thickness
air slice.

|ID     | Rmin [mm]    | Rmax [mm] | Zmin [mm] | Zmax [mm] | Layers | Per-layer structure                        |
|-------|--------------|-----------|-----------|-----------|--------|--------------------------------------------|
|Barrel | 4806         | 6800      | —         | 4444      | 7      | 2 × RPC chamber + air gap + 244 mm of air  |
|Endcap | 493 → 622    | 6800      | 4444      | 5903      | 6      | 197 mm of air + 2 × RPC chamber            |

The endcap layers have a stepped inner radius following the nozzle
(rmin increases by ≈20 mm per layer from 493 to 613 mm).

Each RPC chamber is built as:
PyrexGlass 2 mm + RPCGas 2 mm + PyrexGlass 2 mm, sandwiched between 1 mm Al
covers with 3.5 mm air gaps (≈15 mm per chamber, two stacked back-to-back).
Only the first RPC chamber of each pair carries the `sensitive="yes"` flag;
the second chamber is geometrically present but does not write hits to the
readout collection. This matches the convention used in all MuColl/MAIA-derived
geometries (consult the muon-system contact before changing it).
