# Architecture

## Pipeline

```text
Input Video Stream
      |
      v
Frame Preprocessing
      |
      v
YOLOv8 Person Detection
      |
      v
ByteTrack Tracking
      |
      +-----------------------------+
      |                             |
      v                             v
Application Modules          Visualization / Alerts
```

## Detection Layer

YOLOv8 is used as the primary object detector for identifying people in each frame. The selected detector balances inference speed and detection quality for near real-time processing.

## Tracking Layer

ByteTrack assigns track IDs to detected people and maintains identity continuity across frames. This enables downstream modules to reason over movement history instead of analyzing every frame independently.

## Application Modules

### Occupancy Counting

- Maintains centroid history for each tracked person
- Compares movement against a configured doorway line
- Uses crossing direction to update entry and exit counts
- Applies multi-frame confirmation to reduce jitter-based errors

### Fall Detection

- Uses fall detection corroboration with overlap checks
- Applies posture analysis from bounding-box geometry
- Uses bed-region overlap filtering to reduce false alarms
- Produces fall alerts only when multiple conditions align

### Spatial Mapping

- Uses calibrated floor reference points
- Applies perspective transformation from image space to floor space
- Estimates room-level person position from the bounding-box foot point
- Supports distance measurement between mapped points

### Re-Identification

- Extracts HSV histogram descriptors from tracked people
- Stores descriptors in a short-term gallery
- Compares returning identities using histogram correlation
- Handles short exits and re-entry scenarios

## Suggested Runtime Layout

```text
src/patient_monitoring/
├── detection/
├── tracking/
├── modules/
│   ├── occupancy.py
│   ├── fall_detection.py
│   ├── spatial_mapping.py
│   └── re_identification.py
├── visualization/
└── app.py
```

## Design Principles

- Keep detection, tracking, and application logic separated
- Use class-based modules with clear `update()` and `visualize()` methods
- Store calibration values in configuration files instead of hardcoding
- Keep videos, weights, and experiment outputs outside Git

