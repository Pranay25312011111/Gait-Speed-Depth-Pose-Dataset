# Gait Speed Depth-Pose Dataset: Representative Subset

This repository holds a representative subset of the pose data used in the paper "A Spatiotemporal Deep Learning Architecture for Gait Speed Classification Using Depth-Based Pose Sequences" by Pranay Yadav, Vijay Bhaskar Semwal and Pankaj Kumar.

The complete dataset has 110 treadmill walking recordings from 10 participants. It is not public because of privacy and ethical considerations. This subset has the 24 recordings of two participants. It contains pose coordinates only, with no images, video or depth frames.

## Recording

- Camera: Intel RealSense D456 stereo depth camera
- Setting: treadmill walking in a laboratory, with healthy participants
- Speeds: 0.8 to 3.0 km/h at intervals of 0.2 km/h (0.22 to 0.83 m/s)
- Nominal rate: about 30 frames per second. Some frames are missing, so use `timestamp` rather than assuming even spacing.

## Files

Each recording is one CSV file named `<subject>_<speed>.csv`, where the speed is in km/h. For example, `1_0.8.csv` is subject 1 walking at 0.8 km/h.

| Column | Meaning |
|---|---|
| `frame` | Frame number within the recording |
| `timestamp` | Frame time in Unix seconds |
| `landmark` | Body joint name, such as `NOSE` or `LEFT_HIP`. Each complete frame has 33 joints |
| `x`, `y` | 2D joint coordinates from the RGB stream |
| `z` | Depth value at the joint. A value of 0 means the sensor returned no reading |

## Classes used in the paper

| Class | Speed (km/h) | Speed (m/s) |
|---|---|---|
| Slow | up to 0.8 | up to 0.22 |
| Moderate | above 0.8, up to 1.4 | above 0.22, up to 0.39 |
| Fast | above 1.4 | above 0.39 |

The class names are relative to the recorded range, which lies below typical adult walking speed.

The paper uses windows of 100 complete frames with a step of 25. Three recordings in this subset have fewer than 100 complete frames, so they give no windows: `1_2.0`, `1_2.8` and `2_1.4`.
