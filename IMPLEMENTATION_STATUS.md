# Implementation status — 2026-09-13

The application is usable locally at http://127.0.0.1:8765 when its server is running. Existing source files, trained checkpoints and analysis artifacts were preserved. This directory is not a Git repository; no commits or branches were changed.

## Finished

- React/TypeScript dashboard and local FastAPI/SQLite processing, source playback, exact-frame review, saved-run selection, annotation input and evidence exports.
- Actual car-detector, road-car wheel-segmentation and steering-wheel-regression training. Checkpoint identities and the original training snapshots are retained.
- Completed full analyses of 17,115, 5,293 and 5,309 frames: **27,717 recorded frames** in total. H.264 annotated clips, annotated stills, event JSON/CSV and manifests are available. The 60-frame sampled preview is separately labeled.
- All **6,632** CSV-referenced steering images are present and pass image-integrity verification. Earlier transient file-lock errors are retained in the acquisition history and reconciled in `data/reports/acquisition-final.json`.
- Extended duplicate screening compared every recorded frame of the original test video against all **2,545** images in the actual detector, steering and wheel training/validation snapshots. No candidates appeared at the documented difference-hash threshold. Cropped/transformed duplicates may still evade this check; the report does not claim a proof of independence.
- Source catalog, dataset integrity checks, acquired-file hashes, diagnostic model comparisons, research/design documentation and twelve passing automated tests. TypeScript and production build checks passed; the bundle-size warning is documented.
- FastF1 session adapter, manual timing anchors, planar-registration API, recorded-reference replay API, local schematic simulation and separate CARLA adapter.

## Evidence prevents a full-accuracy completion claim

All three completed full analyses report insufficient geometry for every frame. **Zero flags is not evidence of zero track-limit violations.** The wheel model found 0 instances in the cockpit preview, 1 in the second full clip, and 304 in the São Paulo clip; these are prediction counts, not measured recall. Visual review also found broad or misplaced car boxes. Current models do not satisfy the requested universal, accurate F1 perception.

Reviewed F1 legal-track masks, four-wheel contact/keypoint annotations, independent camera/condition test labels, and calibration evidence are still required. No dedicated track-segmentation or wheel-contact-keypoint checkpoint has been trained. Tire direction and hidden rear-wheel positions are not reliably recovered. Accurate registered/occluded video ghosts and CARLA execution remain unvalidated. The procedural 3D car is illustrative; no to3D physics asset is claimed.

The 572,351-frame long-video run was found **cancelled** after 125 frames and remains cancelled. Its source and partial output are preserved. Completed analyses were not rerun during final reconciliation.
