# Member 3 Final Project Package — Wavelet Compression

This package is the complete Member 3 part for EE 413 Project 2.

## Main File
- `notebooks/EE_413_Project_2_member3_wavelet_final.ipynb`

## What It Does
- Loads ResNet-18 from Member 1.
- Loads MobileNetV2 from Member 2.
- Applies wavelet compression to validation images.
- Tests compression ratios: 2:1, 5:1, 10:1.
- Generates accuracy/loss plots.
- Generates class-wise drop analysis.
- Generates confusion matrices and sample predictions.
- Saves CSV, JSON, figures, and a final ZIP inside Colab.

## Where to Put It
Run it after:
1. Member 1 notebook cells 1–25
2. Member 2 notebook cells 1–26

Then run Member 3 from Cell 27 onward.

## GitHub Commit Messages
Use these:
- Add Member 3 wavelet compression pipeline
- Add ResNet-18 and MobileNetV2 compression evaluation
- Add compression visualizations and class-wise drop analysis
- Add Member 3 README and reproducibility notes