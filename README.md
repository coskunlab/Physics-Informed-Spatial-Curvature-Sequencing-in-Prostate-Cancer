# CurvSeq / Physics-Informed-Spatial-Curvature-Sequencing-in-Prostate-Cancer

This repository hosts the code, data processing scripts, and visualization tools developed for the **CurvSeq** project — a pipeline linking **glandular curvature**, **molecular expression**, **AFM-measured stiffness** in prostate adenocarcinoma tissues.

---

## 🔬 Overview

CurvSeq (short for *Curvature Sequencing*) provides a reproducible workflow to:
- Extract curvature metrics from segmented gland contours (QuPath, Cellpose-SAM, or manual masks)
- Visualize correlations between curvature and gene/protein data
---

## 📁 Repository Structure
curvseq/
├─ src/curvseq/ # Core modules for curvature, AFM, and analysis
│ ├─ metrics.py # Curvature computation utilities
│ ├─ plots.py # Visualization and figure generation
│ ├─ afm.py # AFM stiffness extraction and Hertz fits
│ └─ pipeline.py # Main pipeline for combining curvature, AFM, and molecular data
│
├─ scripts/ # Command-line scripts for reproducible runs
│ ├─ extract_curvature.py
│ ├─ merge_afm_curvature.py
│ └─ make_figures.py
│
├─ notebooks/ # Interactive Jupyter notebooks
│ └─ Curvature_and_Correlation.ipynb # Demonstrates how to compute curvature and correlate it with gene/protein expression
│
├─ data/ # Input and processed data folders
│ ├─ raw/ # Original masks, AFM files, and spatial data
│ ├─ processed/ # Cleaned and merged CSV or AnnData files
│ └─ interim/ # Intermediate results
│
├─ figures/ # Exported figures and plots
├─ tests/ # Unit tests for core functions
├─ requirements.txt
├─ environment.yml
├─ README.md
└─ LICENSE

## 💻 System Requirements

| Component | Requirement | Notes |
|------------|--------------|-------|
| **Operating System** | Windows 10 or Windows 11 | Tested primarily on Windows 11 (64-bit) |
| **Python Version** | 3.10.x | Works best with Conda or venv environments |
| **RAM** | ≥ 16 GB | Large TIFF/NumPy operations benefit from higher memory |
| **Storage** | ≥ 50 GB free | Required for AFM exports, TIFF masks, and processed datasets |
| **GPU (optional)** | NVIDIA CUDA-enabled | Recommended for Cellpose-SAM acceleration |
|  **Dependencies** | Listed in `environment.yml` | Includes `numpy`, `scikit-image`, `tifffile`, `napari`, `scanpy`, `hdbscan`, `matplotlib`, and others |

## ⚙️ Usage – Computing Curvature

The curvature computation module extracts local curvature values from a gland boundary represented as a 2D curve.

### Input Format
The pipeline expects a **2D NumPy array** of shape `(N, 2)` representing the coordinates of the gland boundary:
```python
import numpy as np

# Example: a gland contour stored as (y, x) or (row, col)
coords = np.load("path/to/gland_boundary.npy")  # shape (N, 2)
```
## AnnData Input
When integrating molecular or intensity data, the pipeline accepts an AnnData (.h5ad) file that stores spatial transcriptomics or imaging-derived intensity features for each observation.

```python
Typical format:
AnnData object with n_obs × n_vars = 71380 × 2
obs: 'X', 'Y',
```
Where X and Y are the cell coordinates, the vars are the genes of interest


## Python Packages

The following Python packages are required to run the CurvSeq pipeline:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import os
import re
import tifffile as tif
import scanpy as sc
import cv2
from scipy.ndimage import gaussian_filter1d
from hdbscan import HDBSCAN
from scipy.stats import pearsonr, spearmanr
import seaborn as sns


