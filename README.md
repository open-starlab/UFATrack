## UFATrack Dataset

UFATrack is a professional Ultimate Frisbee dataset released with synchronized **video, tracking, and event annotations** to support reproducible research and practitioner use. :contentReference

### Source / Scope

- Match: **Oakland Spiders vs Salt Lake Shred** (score: OAK 4–9 SLC)
- Date: **June 27, 2025**
- Segment: **2nd quarter** :contentReference
- Effective play included: **~9.5 minutes** (excluding pulls and offense–defense transitions) :contentReference
- Possessions: **20 possession sequences** :contentReference

### Sampling & Coordinates

- Coordinate system: metric (x, y) on a standard pitch of **109.73 m × 48.77 m** :contentReference
- Per frame: positions of **all 14 on-field players + the disc** :contentReference
- Video: **30 fps**, tracking: **10 fps** :contentReference

### Disc position definition

- Disc position is obtained by annotating the **disc holder**
- When no player is in possession, disc location is **linearly interpolated** between consecutive possession events :contentReference

---

## Raw UFATrack Format (this repository)

The raw UFATrack file is in a **long (tidy) format**: each row corresponds to one object (a player or the disc) at a given frame.

Example columns:
- `frame`, `id`
- `x`, `y`
- `vx`, `vy`, `ax`, `ay`
- `v_mag`, `a_mag`
- `v_angle`, `a_angle` (angle unit follows the dataset generation definition)
- `diff_v_a_angle`, `diff_v_angle`, `diff_a_angle` (derived features)
- `class`: `offense` / `defense` / `disc`
- `holder`: `True` only for the disc holder row
- `closest`, `selected`, `prev_holder`, `def_selected` (helper/analysis flags)

---

## Generate Event/Tracking Data via OpenSTARLab PreProcessing

You can convert the raw UFATrack file into standardized **Event data** and **Tracking data** using the OpenSTARLab preprocessing pipeline. The preprocessing module merges and aligns raw inputs, normalizes coordinates, attaches context (team/period labels), and produces an analysis-ready **space-data** representation that can be used directly by downstream evaluation modules (e.g., SpaceEval). :contentReference

### Repository

OpenSTARLab PreProcessing (GitHub):
```text
https://github.com/open-starlab/PreProcessing