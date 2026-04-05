# Multi-Modal Sensor Fusion & Static Map Generation (NuScenes)

This repository implements an end-to-end perception pipeline for autonomous vehicle data using the **NuScenes (v1.0-mini)** dataset. The project focuses on high-fidelity environmental reconstruction through 3D LiDAR aggregation, dynamic object filtering, and multi-view camera-to-LiDAR colorization.

## Processed Results Visualization
The following animation demonstrates the full perception pipeline, featuring the aggregated point cloud and the integrated GNSS-INS trajectory:

![GNSS Recording Visualization](GNSS_visualization.gif)

---

## Key Technical Pipelines

### 1. Global Point Cloud Aggregation
* **Ego-Motion Compensation**: Implements precise spatial synchronization by transforming local LiDAR frames into a global coordinate system using GNSS-INS translation and rotation data.
* **Trajectory Reconstruction**: Uses interpolated GNSS positions and speed-aware heading estimation to correct for the vehicle's movement between 8Hz LiDAR scans.

### 2. Temporal Static Mapping (Ghosting Removal)
* **Dynamic Agent Filtering**: Identifies and isolates non-stationary objects (such as cars and pedestrians) using dataset annotations to prevent "ghosting" artifacts in the final map.
* **Static Map Generation**: Results in a clean, high-fidelity environmental representation by pruning points within the 3D bounding boxes of moving agents.

### 3. Multi-View Camera Fusion & Colorization
* **3D-to-2D Projection**: Projects 3D LiDAR points into six synchronized cameras providing 360° coverage.
* **RGB Mapping**: Uses intrinsic and extrinsic calibration matrices to map pixel-level color data onto the point cloud for a photorealistic 3D representation.

---

## Technical Stack & Dataset
* **Core Framework**: `nuscenes-devkit` for data abstraction and metadata handling.
* **Processing**: `Open3D` and `NumPy` for point cloud manipulation and KDTree-based spatial search.
* **Math & Geometry**: `PyQuaternion` for handling complex 3D rotations and spatial transforms.
* **Dataset**: NuScenes v1.0-mini (includes LiDAR, 6 Cameras, and RTK-corrected GNSS-INS).

## Folder Structure
```text
├── assignment.ipynb        # Main processing and fusion notebook
├── GNSS_visualization.gif  # Visualization of the processed trajectory
├── maps/                   # Base maps used for local projection
├── samples/                # Extracted dataset samples
└── v1.0-mini/              # NuScenes dataset metadata and blobs
```

## Installation & Setup
To reproduce the results, install the perception toolkit:
```bash
pip install nuscenes-devkit open3d pyquaternion
```

---
**Academic Context**: This work was developed for the **3D Sensing and Robotic Perception** course at **Eötvös Loránd University (ELTE)**.  
**Developer**: Rihab Laroussi (XMHGAU)  
**Supervisor**: Hajder Levente
