# Surface_Water_Pollution_Monitoring_Thesis

An end-to-end Computer Vision pipeline designed to detect body of water and classify surface water pollution types from drone footage.

---

## Project Overview
Monitoring surface water pollution manually using drones is time-consuming. This project introduces a **dual-model framework** that combines time-series video recognition with high-accuracy spatial image classification to automate real-time water quality monitoring.

### Key Features:
* **Stage 1 (Water Detection):** Uses a 3D CNN (**SlowFast / Slow_R50**) to analyze temporal features across 16 frames and confirm if water is present.
* **Stage 2 (Pollution Classification):** Automatically extracts and zooms into keyframes to classify contaminants using **ConvNeXt-Tiny** (98% accuracy) and a lightweight **Custom Architecture** (89% accuracy).
* **6 Pollution Classes:** `algal_blooms`, `chemical`, `clean_water`, `foam`, `plastic`, and `sediment`.

---

## Architecture Pipeline

1. **Input:** Drone Video Clip
2. **Model 1 (3D ResNet-50):** Detects `Water` vs `No_Water`
3. **Frame Extractor & Zoom:** Crops central surface water regions
4. **Model 2 (ConvNeXt-Tiny / Custom CNN):** Predicts Pollution Category

---

## Model Performance & Trade-off Analysis

| Model Architecture | Training Approach | Dataset Size | Accuracy | Deployment Target |
|-------------------|------------------|--------------|----------|-------------------|
| **ConvNeXt-Tiny** | Transfer Learning | ~5,000 images | **98%** | High-performance Server / Cloud |
| **Custom CNN** | From Scratch | ~5,000 images | **89%** | Edge Devices (Drones / Embedded Systems) |

> **Key Research Insight:** While ConvNeXt achieves superior accuracy via Transfer Learning, the Custom CNN offers a lightweight footprint ideal for resource-constrained edge computing without relying on pre-trained weights.

---

