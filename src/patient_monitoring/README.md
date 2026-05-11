# Source Code

Add implementation files for the patient monitoring pipeline in this package.

Suggested modules:

- `detection/` for YOLOv8 model loading and inference
- `tracking/` for ByteTrack integration
- `modules/occupancy.py` for entry and exit counting
- `modules/fall_detection.py` for fall-event logic
- `modules/spatial_mapping.py` for homography and distance estimation
- `modules/re_identification.py` for histogram-based matching
- `visualization/` for overlays and alert rendering

Keep raw videos, model weights, and generated runs outside the repository.

