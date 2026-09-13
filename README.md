# Ghost Rival Studio

A local motorsport video research application. React/TypeScript, FastAPI, SQLite, OpenCV and PyTorch. The dashboard uses the supplied F1 Ghost Rival Analysis visual reference: photographic source footage, green detections, cyan schematic simulation and amber line candidates.

Open **http://127.0.0.1:8765** while the local server is running. `start-studio.ps1` starts it again. `setup.ps1` installs dependencies and builds the interface on a new machine. The current development environment reuses ML libraries from `D:\ANTIGRAVITY\ParcelMapper\.venv` through a `.pth` file; a clean installation requires the dependencies in requirements.txt instead.

## Delivered implementation

- Video upload, actual source playback, frame stepping, overlay toggle, background final/preview processing, cancellation and consistent restart from source.
- Car detection/tracking, camera-motion compensation, cut detection, apparent image-plane movement and experimental visible-wheel segmentation. These are estimates, not measured vehicle dynamics.
- Analyst track/contact polygons, line-inclusive single-frame excursion logic, frame evidence and CSV/JSON/video/still/manifests. No missing geometry is silently treated as inside.
- Dataset inventory and evaluation dashboard, FastF1 explicit session loader/timing annotations, deterministic simplified rival playback and separate CARLA adapter.
- Ground-plane registration/projection and recorded-telemetry replay API endpoints. Spatial registration requires analyst evidence; it is not automatic or validated for moving cockpit views.

## Actual training and evidence

Three trained checkpoints are in `data/models`: `car-detector.pt`, `wheel-segmenter.pt`, `steering-wheel.pt`. Training scripts, split manifests and reports are retained. Steering-wheel regression is a research checkpoint, not a tire-angle prediction, and is not used to decide track limits.

The original 17,115-frame test video has a completed analysis in `data/analyses/548a34c2d69348c4b2ba576db83f5464`. All frames are present. All lack enough four-wheel/legal-boundary geometry; zero flags does **not** establish a clean lap. The original analysis is preserved; later jobs additionally use the experimental wheel model. A browser-compatible H.264 derivative is included.

The additional uploaded 1280×720, 50 fps clip also completed all 5,293 frames in `data/analyses/c342c55f714c410aa8699f9950c21bfe`. Its H.264 export and annotated still are verified. All frames remain geometrically unresolved; only one experimental wheel instance was detected. This is not adequate F1 wheel performance.

## Remaining research requirements

This is a working research application, not the fully validated system described in the brief. Reviewed F1 wheel-contact/keypoint and legal-track-mask training data are still missing. There is no trained legal-boundary model, no validated hidden-wheel reconstruction, no reliable tire-angle estimate, no universal camera/speed guarantee, and no calibrated event probabilities. Curbs, runoff and painted-line candidates cannot substitute for legal-area annotation.

Cross-recording/camera evaluation, event ground truth, identity-switch metrics, ghost occlusion/registration validation, and CARLA hardware execution remain pending. The 3D asset is procedural and illustrative; no to3D-generated physics asset is claimed. No publication or cloud upload was performed.

See `RESEARCH_AND_DESIGN.md`, `data/source_catalog.json`, and `data/reports/*.json` for evidence and scope. Run `python -m unittest discover -s tests -p "test_*.py"`, `npx tsc --noEmit`, and `npm run build` for local checks.
