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

## 🚀 How to Run & Test the Pipeline

Follow these simple instructions to test the dual-model water detection and pollution classification pipeline:

### **Step 1: Download Pre-Trained Model Weights**
Download both model files from Google Drive and upload/save them directly to your Google Drive root folder:
* **Drone Video Segmentation Model (SlowFast / 3D CNN):** [Download Model 1 (.pth)](https://drive.google.com/file/d/1ejBV1iYLA-iML6JOT8Ndku0mlE2xmzyx/view?usp=sharing)
* **Water Pollution Classification Model (ConvNeXt-Tiny):** [Download Model 2 (.h5)](https://drive.google.com/file/d/1HDwtuHd6PZD40OdUyTMs3fCNpHSzZLjN/view?usp=sharing)

---

### **Step 2: Execution via Google Colab**
1. Open the testing notebook in Google Colab: **`Water_detect_and_pollutiondetect.ipynb`**
2. Mount your Google Drive to load the saved `.pth` and `.h5` model files.
3. Run **Cell 1** to initialize and load both deep learning models.
4. Upload any target sample drone video (in `.mp4` format) to the Colab workspace.
5. Run **Cell 3 (Pipeline Execution)** by providing the uploaded video path.

---

### **Step 3: Automated Pipeline Workflow**
Once executed, you can observe the real-time pipeline in action:
* **Stage 1 Output:** Model 1 scans 16 temporal video frames to confirm `WATER DETECTED` or `NO WATER DETECTED`.
* **Stage 2 Output:** If water is detected, the pipeline automatically extracts localized keyframes, zooms into the water surface, and passes them to Model 2.
* **Final Output:** Predicts the exact contaminant category (`algal_blooms`, `chemical`, `clean_water`, `foam`, `plastic`, or `sediment`).

