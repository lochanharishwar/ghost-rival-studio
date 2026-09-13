# Research, design and evidence status

The approved implementation plan controls scope. The PDF and companion text supply the research/design requirements; their original research-only framing was superseded by the user's explicit implementation/training instruction. The reference PNG controls visual language, never measured geometry. The supplied cockpit video remains held out.

## Dataset discovery and provenance

The source catalog records accessible and blocked sources across GitHub, Hugging Face, Kaggle, Roboflow and academic projects. Discovery is documented but not an exhaustive proof that all online datasets have been found. A 50,000,000,000-byte collection budget includes archives and derivatives. Publisher licenses do not independently establish rights to underlying broadcast footage.

| Source | Finding and use |
|---|---|
| [FormulaTracker](https://github.com/theosorus/FormulaTracker) / [Formula1-Box](https://www.kaggle.com/datasets/gazeux330000/formula1-box) | Acquired F1 images; source polygon labels converted to car boxes. Single broadcast source limits independence. |
| [F1 steering dataset](https://huggingface.co/datasets/daniel-saed/F1-steering-angle-dataset) | CSV has 6,632 rows; snapshot acquisition counts in catalog. Original-angle column contains invalid values; rejected labels retained. Some filenames indicate game footage. |
| [Formula One Cars](https://www.kaggle.com/datasets/vesuvius13/formula-one-cars) | Appearance collection acquired; no precise wheel/boundary supervision established. |
| [Track limits](https://universe.roboflow.com/nikshithas-workspace/f1-race-track-limits) | Listing inspected; export version unavailable. Object classes do not establish accurate legal masks. |
| [VROOM](https://varun-bharadwaj.github.io/vroom/) | Registration/reconstruction reference; linked repository unavailable during inspection. |
| [RACECAR](https://registry.opendata.aws/racecar-dataset/) | Indy sensor corpus, noncommercial terms; not acquired as F1 supervision. |
| [Carparts-Seg](https://docs.ultralytics.com/datasets/segment/carparts-seg/) | Road-car wheel masks, class 22. Acquired for experimental wheel segmentation; F1 transfer unvalidated. |
| [TUM racetrack database](https://github.com/TUMFTM/racetrack-database) | Centerlines and approximate widths are simulation references, not video-exact legal boundaries. |

Exact SHA and difference-hash candidate checks are recorded in `data/reports/data-quality.json`. All 17,115 test frames were fingerprinted against the detector sample set. No candidates were found under the stated threshold; perceptual hashing does not prove absence of all matching footage. Recording-derived samples stay grouped where provenance permits; mixed/source-unknown material needs further review before claims of independent performance.

## Model evidence

| Component | Actual experiment | Practical limit |
|---|---|---|
| Car detector | YOLO11n fine tuning, 209 train / 168 validation images, 3 epochs; diagnostic mAP50 0.7593 | Chronological split within one broadcast; no independent multi-camera benchmark |
| Detector comparison | At confidence .25, IoU .5: pretrained precision .3436 / recall .3394; trained .6417 / .7273 | Same diagnostic slice; not universal performance |
| Visible-wheel segmentation | 320 road-car train / 34 validation, 3 epochs; mask precision .6078 / recall .3510 | Low recall, road-car domain; masks do not establish contact points |
| Steering-wheel regression | 1,195 train / 619 validation; 38.61° MAE vs 48.16° constant baseline | Validation selected checkpoint; no independent test; not tire steering or heading |
| Track / contact keypoints | Training entry point exists but requires reviewed labels | No checkpoint or accuracy claim |

Raw reports, configurations and checkpoint hashes take precedence over rounded figures here. Dataset downloads may exceed the snapshot used for a training experiment; downloading more files does not retroactively train the model.

Integration preview on the reserved cockpit video sampled 60 frames at 1 fps. The wheel model returned **zero wheel instances** at its .25 threshold. This establishes a failure on this sampled footage, not a successful cockpit-wheel detector. The preview retained all 60 frames as insufficient geometry.

## Product and interfaces

Analysis preserves the source camera. Preview is explicitly reduced-frame; final processes every decoded frame. The interface separates intake/analysis, source inventory, models/evaluation, session alignment, scenarios and exports. Errors, cancellation and restart are visible. SQLite stores versioned records; frame JSONL and manifests retain units, confidence kind and provenance. Scores are uncalibrated and absent when unsupported.

Track-limit logic requires all four contact polygons to be disjoint from a valid permitted-area polygon. Boundary contact is inside. Isolated flags are retained; smoothing never removes them. Missing contacts yield unknown. Geometry is interval-specific and cannot be assumed stationary across camera cuts or a moving cockpit.

FastF1 channels require explicit session identity and synchronization. No telemetry was fabricated for the unmatched supplied clip. Image velocity describes apparent compensated movement, not physical speed or a measured acceleration. Steering-wheel angle, tire angle and image-plane motion heading remain distinct.

Recorded-reference replay uses external telemetry. Parameterized and responsive scenarios are separately labeled simulation. The local fallback is a one-dimensional kinematic experiment, not validated racing physics. Recorded ego video never responds to it. The CARLA adapter remains pending local server/hardware validation. Procedural cyan 3D meshes are illustrative; they do not establish accurate car geometry or physics.

## Verification boundaries

Automated checks cover line contact, one-frame excursions, hidden contacts, missing confidence, deterministic simulation and known/degenerate planar registration. The completed supplied-video audit establishes frame coverage, not event accuracy. Detection precision/recall are diagnostic model measurements; false flags/minute, legal-boundary error, tire-contact error, identity switches, calibrated confidence and cross-condition event precision/recall require reviewed independent ground truth and remain unavailable.
