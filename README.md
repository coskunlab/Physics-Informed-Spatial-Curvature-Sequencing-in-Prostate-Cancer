# CurvSeq / Physics-Informed-Spatial-Curvature-Sequencing-in-Prostate-Cancer

This repository hosts the code, data processing scripts, and visualization tools developed for the **CurvSeq** project — a pipeline linking **glandular curvature**, **molecular expression**, **AFM-measured stiffness** in prostate adenocarcinoma tissues.

---

## 🔬 Overview

CurvSeq (short for *Curvature Sequencing*) provides a reproducible workflow to:
- Extract curvature metrics from segmented gland contours (QuPath, Cellpose-SAM, or manual masks)
- Visualize correlations between curvature and gene/protein data


---

## 📁 Repository Structure


## 💻 System Requirements

| Component | Requirement | Notes |
|------------|--------------|-------|
| **Operating System** | Windows 10 or Windows 11 | Tested primarily on Windows 11 (64-bit) |
| **Python Version** | 3.10.x | Works best with Conda or venv environments |
| **RAM** | ≥ 16 GB | Large TIFF/NumPy operations benefit from higher memory |
| **Storage** | ≥ 50 GB free | Required for AFM exports, TIFF masks, and processed datasets |
| **GPU (optional)** | NVIDIA CUDA-enabled | Recommended for Cellpose-SAM acceleration |
|  **Dependencies** | Listed in `environment.yml` | Includes `numpy`, `scikit-image`, `tifffile`, `napari`, `scanpy`, `hdbscan`, `matplotlib`, and others |


