# Image Compression and Classification with Deep Learning
### EE 413: Applied Digital Signal Processing — Project 2
**King Fahd University of Petroleum and Minerals | Spring 2026 (252)**

---

## Team Members

| Member | ID | Contribution |
|--------|----|--------------|
| Saad Alriyan | 202181050 | Dataset, Preprocessing, and ResNet-18 (Model 1) |
| Talal Alghamdi | 202178870 | MobileNetV2 (Model 2), Training Pipeline, and Model Comparison |
| Abdulrahman Alburaikan | 202175630 | Wavelet Compression and Compression Analysis |

---

## Project Overview

This project investigates the effect of wavelet-based image compression on deep learning classification performance using the Mini-ImageNet dataset. Two pre-trained models (ResNet-18 and MobileNetV2) are fine-tuned on the uncompressed dataset, then evaluated against compressed versions at multiple compression ratios.

The project applies three course topics:
- **Wavelet Transform** — image compression at multiple ratios
- **Convex Optimization** — model fine-tuning and loss minimization
- **Compressed Sensing** — signal acquisition and reconstruction

---

## Project Objective

- Apply pre-trained deep learning models to image classification tasks
- Implement wavelet-based image compression at various compression ratios
- Evaluate the impact of compression on classification performance
- Compare model performance across different compression scenarios
- Gain experience with PyTorch for deep learning and image processing
- Connect practical implementation results to theoretical DSP concepts

---

## Dataset

This project uses the **Mini-ImageNet** dataset — a widely used benchmark for few-shot learning and image classification research.

### Characteristics
- Subset of ImageNet with **100 classes**
- **600 images per class** (500 training, 100 testing)
- Images resized to **96×96 pixels**
- Splits are **non-overlapping by design** (64 train / 16 val / 20 test classes)
- Diverse object categories suitable for compression experiments

> **Note:** Because the splits are disjoint, the meaningful baseline metric is **validation accuracy on the 64 training classes**, not test split accuracy.

### Source
```
https://huggingface.co/datasets/timm/mini-imagenet
```


---

## Methodology

### Member 1 — Dataset, Preprocessing, and ResNet-18
- Download and organize Mini-ImageNet
- Build PyTorch datasets and dataloaders with ImageNet normalization
- Fine-tune ResNet-18 using a two-phase training strategy
- Record baseline accuracy, loss, and confusion matrix

### Member 2 — MobileNetV2 and Model Comparison
- Fine-tune MobileNetV2 using the exact same setup as Member 1
- Compare ResNet-18 vs MobileNetV2 on uncompressed validation images
- Document model architecture differences and parameter counts

### Member 3 — Wavelet Compression Analysis
- Implement wavelet-based image compression using PyWavelets
- Generate compressed validation images at three ratios: **2:1, 5:1, 10:1**
- Apply soft/hard thresholding on wavelet coefficients
- Evaluate both models on compressed images
- Analyze which classes are most affected by compression

---

## Training Strategy (identical for both models)

| Setting | Value |
|---------|-------|
| Phase 1 | 5 epochs, backbone frozen, Adam lr=1e-3 |
| Phase 2 | 30 epochs, full fine-tuning, SGD |
| Backbone LR | 1e-4 |
| Head LR | 1e-3 |
| Weight Decay | 1e-4 |
| Label Smoothing | 0.1 |
| Image Size | 96×96 |
| Seed | 42 |
| Normalization | ImageNet mean/std |

---

## Dependencies

```
pip install -r requirements.txt
```

```
torch>=2.0.0
torchvision>=0.15.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
scikit-learn>=1.2.0
PyWavelets>=1.4.0
timm>=0.9.0
Pillow>=9.0.0
```

---

## How to Run

1. **Member 1** — Run `member1_resnet18/notebook/EE413_Member1_ResNet18.ipynb` cells 1–25
2. **Member 2** — Run `member2_mobilenetv2/notebook/EE413_Member2_MobileNetV2.ipynb` cells 1–26
3. **Member 3** — Run `member3_wavelet/notebook/EE413_Member3_Wavelet.ipynb` (requires checkpoints from Members 1 & 2)

---

## Reproducibility

All experiments use `seed = 42`. Run notebooks in order: Member 1 → Member 2 → Member 3.

---

## Results Summary

| Domain | Model | Baseline Val Accuracy |
|--------|-------|-----------------------|
| Uncompressed | ResNet-18 | 76.48% |
| Uncompressed | MobileNetV2 | TBD |
| Compressed 2:1 | ResNet-18 | TBD |
| Compressed 2:1 | MobileNetV2 | TBD |
| Compressed 5:1 | ResNet-18 | TBD |
| Compressed 5:1 | MobileNetV2 | TBD |
| Compressed 10:1 | ResNet-18 | TBD |
| Compressed 10:1 | MobileNetV2 | TBD |


---

## References

- Mini-ImageNet Dataset: https://huggingface.co/datasets/timm/mini-imagenet
- PyWavelets Documentation: https://pywavelets.readthedocs.io
- Oppenheim & Schafer, *Discrete-Time Signal Processing*
- Course material: EE 413, KFUPM Spring 2026
