# Project Summary

## Problem

Patient monitoring in hospital and assisted-care environments often depends on manual observation or sensor-based systems. Wearable sensors can be intrusive, may be forgotten by patients, and can add operational overhead. This project explores a camera-based monitoring approach that uses AI and computer vision to detect patient movement, identify falls, count occupancy, and estimate room-level position from video.

## Solution

The system uses a modular video analytics pipeline built around YOLOv8 detection and ByteTrack tracking. Each tracked person is processed by independent modules for occupancy counting, fall detection, spatial mapping, and re-identification.

## Methodology

- Detect people in video frames using YOLOv8
- Assign persistent track IDs using ByteTrack
- Analyze centroid trajectories for entry and exit counting
- Detect falls using fall-specific model output, posture analysis, and bed-region filtering
- Convert image coordinates to room coordinates using homography transformation
- Re-identify people using HSV color histogram matching with time-limited gallery entries

## Evaluation Highlights

- Fall detection achieved 88.9% detection rate across staged fall events
- False alarms were reduced by 83.3% compared with an aspect-ratio-only baseline
- Spatial mapping achieved 18.7 cm mean absolute position error
- Re-identification achieved 79.2% accuracy across re-entry sequences
- Integrated processing achieved 24.3 FPS average throughput

## Practical Use Cases

- Patient fall alerting
- Room occupancy awareness
- Patient location estimation
- Caregiver dashboard integration
- Safety monitoring in controlled indoor environments

