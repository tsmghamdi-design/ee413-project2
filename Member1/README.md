# EE 413 — Member 1: Dataset Setup, ResNet-18 Fine-tuning & Baseline Evaluation

## Overview
This module covers:
- Mini-ImageNet dataset extraction and organisation
- ResNet-18 fine-tuning on the uncompressed training set
- Baseline evaluation on the uncompressed test set

## Baseline Result
| Metric | Value |
|--------|-------|
| Model | ResNet-18 (ImageNet pre-trained) |
| Dataset | Mini-ImageNet (100 classes, uncompressed) |
| Image Size | 96×96 |
| Test Accuracy | 0.25% |
| Test Loss | 6.3266 |
| Best Val Accuracy | 76.48% |

## Training Strategy
- **Phase 1** (5 epochs): Backbone frozen, only classifier head trained (Adam, lr=1e-3)
- **Phase 2** (30 epochs): Full fine-tuning (SGD, backbone lr=1e-4, head lr=1e-3, StepLR)
- Label smoothing = 0.1, Weight decay = 0.0001

## Output Files
| File | Description |
|------|-------------|
| `resnet18_best.pth` | Best model checkpoint (by val accuracy) |
| `training_history.json` | Loss & accuracy per epoch |
| `baseline_results.json` | Scalar baseline metrics |
| `classification_report.txt` | Per-class precision/recall/F1 |
| `per_class_accuracy.json` | Per-class accuracy (for teammate use) |
| `training_curves.png` | Loss & accuracy plots |
| `per_class_accuracy.png` | Bar chart of class-wise accuracy |
| `confusion_matrix_full.png` | Full 100×100 confusion matrix |
| `confusion_matrix_bottom20.png` | Zoomed view of hardest 20 classes |
| `sample_images.png` | Random training samples |
| `sample_predictions.png` | Test predictions (correct/wrong) |
| `top_bottom_classes.txt` | Best and worst classified classes |

## Dataset
- **Source**: Mini-ImageNet
- **Classes**: 64
- **Structure**: `train/` `val/` `test/` each containing `<class_id>/` subdirectories
- **Normalisation**: ImageNet mean/std ([0.485, 0.456, 0.406] / [0.229, 0.224, 0.225])

## Dependencies
See `requirements.txt`.

## Reproducibility
All results are reproducible with seed=42.
Run cells in order from Cell 1 to Cell 25.

## Notes for Teammates
- `per_class_accuracy.json` — class-wise accuracy on uncompressed test set for comparison
- `baseline_results.json` — scalar metrics to tabulate against compressed results
- Checkpoint `resnet18_best.pth` is ready for wavelet-compressed test set evaluation
