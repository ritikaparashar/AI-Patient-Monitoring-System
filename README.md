# AI-Enhanced Patient Monitoring System

A computer vision system for patient room monitoring using standard video feeds. The project combines object detection, multi-object tracking, fall detection, spatial mapping, occupancy counting, and lightweight person re-identification to support real-time awareness in healthcare environments without requiring wearable sensors.

## Overview

Hospitals and care facilities often need continuous awareness of patient movement, room occupancy, and emergency events such as falls. This project uses camera-based AI to analyze patient activity from video streams and generate interpretable monitoring signals for caregivers.

The system is designed around four core capabilities:

- Real-time patient and occupancy detection from video frames
- Fall detection using posture, overlap, and spatial context checks
- Room-level spatial localization using homography-based floor mapping
- Person re-identification using visual appearance matching across re-entry events

## Key Results

| Capability | Result |
| --- | --- |
| Fall detection | 88.9% detection rate on staged fall sequences |
| False alarm reduction | 83.3% reduction compared with aspect-ratio-only baseline |
| Spatial mapping | 18.7 cm mean position error using homography mapping |
| Re-identification | 79.2% correct re-identification across re-entry events |
| Runtime performance | 24.3 FPS average integrated throughput |
| Occupancy direction | Approximately 97% directional accuracy |

## System Architecture

```text
Video Feed
   |
   v
YOLOv8 Person Detection
   |
   v
ByteTrack Multi-Object Tracking
   |
   +--> Occupancy Counting
   +--> Fall Detection
   +--> Spatial Mapping
   +--> Person Re-Identification
   |
   v
Dashboard / Alert Layer
```

## Core Modules

### 1. Occupancy Counting

The occupancy module detects people entering and leaving a monitored room using a virtual doorway line. Person centroids are tracked across frames, and crossing direction is calculated using trajectory movement relative to the boundary.

Highlights:

- YOLOv8-based person detection
- ByteTrack-based identity assignment
- Virtual boundary crossing logic
- Multi-frame hysteresis to reduce noisy crossing events

### 2. Fall Detection

The fall detection pipeline combines multiple checks instead of relying on a single bounding-box rule. This helps reduce false alarms when a patient lies on a bed or appears horizontal during normal activity.

Pipeline stages:

- Fall-specific detection corroboration using Intersection over Minimum Area
- Posture analysis using bounding-box orientation and aspect behavior
- Bed-region filtering using overlap with predefined bed zones

### 3. Spatial Mapping

The system maps image coordinates to room-level floor coordinates using perspective transformation. The bottom-center point of a tracked person bounding box is used as the floor contact point.

Highlights:

- Four-point homography calibration
- Pixel-to-room coordinate transformation
- Distance estimation using mapped floor-plane positions
- Improved accuracy compared with basic pixel-per-meter scaling

### 4. Person Re-Identification

The re-identification module stores lightweight appearance descriptors for tracked people and compares them when a person re-enters the scene.

Highlights:

- HSV histogram-based appearance encoding
- Correlation-based matching
- Time-limited gallery storage
- Re-entry matching across short-duration occlusions or exits

## Tech Stack

- Python 3.10
- OpenCV
- Ultralytics YOLOv8
- ByteTrack
- NumPy
- SciPy
- PyTorch

## Repository Structure

```text
AI-Patient-Monitoring-System/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DATASET.md
│   └── PROJECT_SUMMARY.md
├── media/
│   └── .gitkeep
└── src/
    └── patient_monitoring/
        └── README.md
```

## Dataset Note

The original dataset contains large video files and is not stored in this repository. Large media files should be hosted externally using a storage service such as Google Drive, Kaggle Datasets, Hugging Face Datasets, Zenodo, or cloud object storage.

Recommended approach:

- Keep raw videos outside Git
- Add only small, anonymized demo clips or sample frames if permitted
- Document dataset structure in `data/README.md`
- Store trained model weights outside the repository or through a release asset if they are small enough

## Local Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Place local videos using the structure described in `data/README.md`. Raw videos, model weights, experiment outputs, and tracking runs are ignored by Git.

## Current Status

This repository documents the project architecture, methodology, performance results, and expected implementation structure. Source files can be added under `src/patient_monitoring/` when the implementation code is available.

## Future Improvements

- Improve re-identification robustness for similar clothing and poor lighting
- Add multi-camera support for larger room and ward coverage
- Integrate alert notifications with hospital communication systems
- Add temporal motion analysis to better separate bed movement from fall events
- Package modules into a dashboard-ready real-time inference service

