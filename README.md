# GNSS-INS Point Cloud Processing

This directory contains an implementation for processing multi-modal sensor data from an autonomous vehicle. The project focuses on aggregating LiDAR scans, filtering dynamic objects, and colorizing point clouds using camera fusion.

## 📌 Project Overview
![GNSS Recording Visualization](GNSS_visualization.gif)

The core of this work is contained in `assignment.ipynb`, which leverages the **NuScenes (v1.0-mini)** dataset. The vehicle is equipped with:
- **Top LiDAR**: High-resolution 3D point cloud data.
- **GNSS-INS System**: Provides precise ego-motion and spatial orientation (RTK corrected).
- **Cameras**: 6 synchronized cameras (360° coverage for colorization).

## 🚀 Key Tasks

### 1. Point Cloud Aggregation
- Combines individual LiDAR frames into a global coordinate system.
- Uses **ego-motion data** (translation and rotation) from the GNSS-INS system.
- Corrects for the vehicle's movement between scans to build a consistent spatial map.

### 2. Moving Object Filtering
- Identifies dynamic agents (cars, pedestrians, etc.) using NuScenes annotations.
- Filters out "ghosting" effects in the aggregated map by removing points within bounding boxes of non-stationary objects.
- Results in a high-fidelity **static map** of the environment.

### 3. Point Cloud Colorization
- Multi-view fusion: projects 3D LiDAR points into 2D camera images.
- Maps RGB values from images onto corresponding points.
- Uses intrinsic/extrinsic calibration matrices for accurate point-to-pixel mapping.

## 📂 Folder Structure
- `assignment.ipynb` - Main processing notebook.
- `GNSS_recording.mp4` - Video visualization of the processed trajectory.
- `maps/` - Base maps used for local projection.
- `samples/` - Extracted dataset samples.
- `v1.0-mini/` - Subset of the NuScenes dataset.

## 🛠 Installation & Setup
To run the notebook, install the following dependencies:
```bash
pip install nuscenes-devkit open3d pyquaternion
```

---
**Course**: 3D Sensing and Robotic Perception  
**University**: Eötvös Loránd University (ELTE)  
**Student**: Rihab Laroussi (XMHGAU)
