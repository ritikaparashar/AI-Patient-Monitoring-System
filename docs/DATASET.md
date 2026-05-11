# Dataset Handling

## Why Videos Are Not Stored Here

The dataset for this project is video-based and can grow to several gigabytes. GitHub repositories are not designed for storing large raw video datasets. Keeping raw media in Git makes cloning slow, increases storage usage, and can cause pushes to fail.

## Recommended Storage Options

- Google Drive for private sharing
- Kaggle Datasets for public datasets
- Hugging Face Datasets for ML-friendly hosting
- Zenodo for academic dataset releases
- AWS S3, Google Cloud Storage, or Azure Blob Storage for scalable storage

## Suggested Local Structure

```text
data/
├── raw_videos/
│   ├── occupancy/
│   ├── fall_detection/
│   ├── spatial_mapping/
│   └── re_identification/
├── sample_frames/
├── annotations/
└── README.md
```

## What Can Be Committed

- Small anonymized sample frames
- Short compressed demo clips if privacy permissions allow it
- Annotation examples
- Calibration examples
- Dataset documentation

## What Should Not Be Committed

- Raw GB-scale videos
- Patient-identifiable media
- Large trained weights
- Experiment output folders
- Temporary tracking results

## Dataset Access Template

Add the external dataset link here when it is ready:

```text
Dataset access: <add external storage link>
Access notes: <public/private/request-based>
Video format: <mp4/avi/mov>
Frame rate: <fps>
Resolution: <width x height>
Privacy status: <anonymized/controlled/internal>
```

