# September 13 upgrade verification

The upgraded interface runs locally at http://127.0.0.1:8766. The original port 8765 worker remains running its existing long analysis. The upgraded launcher preserves active database records; cancellation of another worker's job must use its original interface. New analyses are accepted and serialized within the upgraded worker, independently of the legacy CPU worker. Matching active submissions return the existing job. Waiting jobs can be cancelled. This removes the former global 'A processing job is already active' rejection. Submission regression coverage brings the Python test count to 18.

Implemented car-mask contours (pretrained YOLO segmentation fallback), independently smoothed display contours, thick glowing white track candidates, dashed short-lived inferred continuation, reviewed polygon fallback, exact-frame prefetch, RTX 5050 CUDA/FP16 batch inference, and an OpenF1 session/driver circuit companion.

CUDA benchmark: 24 frames, 640-pixel model input, CPU 9.68 FPS versus GPU batch-eight 37.18 FPS. This excludes decoding and export overhead and is not an accuracy measurement. See data/reports/gpu-benchmark.json.

Verification: 15 Python unittest checks, four Sites packaging tests, production build, and a held-out 77-frame GPU integration run including a partial final batch. OpenF1 Interlagos 2023 qualifying was verified through the visible interface with a circuit trace and driver/lap details. See data/reports/gpu-pipeline-verification.json and openf1-verification.json.

Limitations: new contours are not a newly trained F1 segmentation model. Track candidates are not validated legal boundaries. Missing lines can use recent evidence or reviewed camera geometry; automatic circuit-to-camera reconstruction is not implemented. OpenF1 provides a separate reference trace, not synchronized legal boundaries. Scores remain uncalibrated. Old analysis artifacts are preserved and require reprocessing to obtain new contours. No universal accuracy or instantaneous processing claim is supported.
