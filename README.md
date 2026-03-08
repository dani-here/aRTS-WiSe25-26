# Real-Time Obstacle Detection: Optical vs. Sensor Fusion

This repository contains the experimental notebooks accompanying the paper:

**"Evaluating Real-Time Obstacle Detection: Optical vs. Sensor Fusion Approaches"**

The project evaluates the **accuracy–latency trade-offs** between a vision-only object detection pipeline and a **vision–LiDAR late fusion pipeline** under real-time constraints using the KITTI dataset.

---

### 1. `01_vision_pipeline.ipynb`

Implements the **vision-only obstacle detection pipeline**.

Main components:

- YOLOv8-based object detection
- Training and validation on the KITTI dataset
- Image preprocessing and augmentation
- Evaluation metrics:
  - Precision
  - Recall
  - mAP
  - Latency and FPS
- Robustness testing with injected degradations:
  - Gaussian noise
  - Motion blur
  - Brightness/contrast variation

This notebook establishes the **baseline optical detection performance**.

---

### 2. `02_lidar_fusion_pipeline.ipynb`

Implements the **Vision–LiDAR late fusion pipeline**.

Main components:

- YOLOv8 visual detection
- LiDAR point cloud processing using Open3D
- ROI filtering and voxel downsampling
- Ground plane removal
- DBSCAN clustering for obstacle candidate generation
- Projection of LiDAR clusters to the image plane
- IoU-based association between camera detections and LiDAR clusters

The notebook evaluates the **fusion pipeline under real-time constraints**.

---

## Dataset

Experiments were conducted using the **KITTI dataset**.

Sources used:

- KITTI dataset (Kaggle mirror)
- KITTI annotations converted to YOLO format

Dataset split:

| Split | Samples |
|------|--------|
| Train | 5984 |
| Validation | 1047 |
| Test | 450 |

Images were resized to **640×640** during training.

---

## Evaluation Metrics

The experiments evaluate both **detection performance** and **real-time feasibility**.

Detection metrics:

- Precision
- Recall
- mAP50
- mAP50–95
- F1 score

Real-time metrics:

- Average inference latency
- Throughput (FPS)
- Missed Deadline Rate (DMR)

The real-time deadline used in the experiments is: 100 ms per frame (≈10 FPS requirement)


---

## Hardware and Software

### Hardware

Experiments were executed on Kaggle compute instances:

- CPU: 4 vCPU (Intel Xeon ~2.0 GHz)
- RAM: 30 GB
- GPU: NVIDIA T4 (16 GB VRAM)

### Software

- Python
- Ultralytics YOLOv8
- Open3D
- PyTorch
- NumPy
- OpenCV

---

## Key Findings

- The **vision-only pipeline** achieved:
  - Higher detection accuracy
  - Lower latency (~15 ms per frame)

- The **late fusion pipeline** provided geometric depth information but introduced significant overhead:
  - ~87 ms average latency due to LiDAR clustering and fusion steps

- Both pipelines satisfied the **100 ms real-time constraint**, resulting in **0% missed deadlines**.

---

## Reproducibility

Kaggle cloud notebooks were used to carry out the pipeline creation and inference tasks.

---

## Contributors

- Hamza Asaad
- Salman Younus
- Danish Ali

