# EE 413 — Member 2: MobileNetV2 Fine-tuning & Model Comparison

## Overview
This module covers:
- MobileNetV2 fine-tuning on Mini-ImageNet (same setup as Member 1 for fair comparison)
- Baseline evaluation on the uncompressed validation set
- Side-by-side comparison of ResNet-18 (Member 1) vs MobileNetV2 (Member 2)

## Baseline Result
| Metric | ResNet-18 (Member 1) | MobileNetV2 (Member 2) |
|--------|----------------------|------------------------|
| Val Accuracy | 76.48% | See baseline_results.json |
| Parameters | ~11.7M | ~3.5M |
| Image Size | 96x96 | 96x96 |

## Training Strategy (identical to Member 1)
- Phase 1 (5 epochs): Backbone frozen, only classifier head trained (Adam, lr=1e-3)
- Phase 2 (30 epochs): Full fine-tuning (SGD, backbone lr=1e-4, head lr=1e-3, StepLR)
- Label smoothing = 0.1, Weight decay = 0.0001
- Seed = 42, Image size = 96x96

## Output Files
| File | Description |
|------|-------------|
| mobilenetv2_best.pth | Best model checkpoint (by val accuracy) |
| training_history.json | Loss & accuracy per epoch |
| baseline_results.json | Scalar baseline metrics |
| classification_report.txt | Per-class precision/recall/F1 |
| per_class_accuracy.json | Per-class accuracy (for Member 3) |
| model_comparison.png | ResNet-18 vs MobileNetV2 accuracy & size |
| training_curves.png | Loss & accuracy plots |
| confusion_matrix_full.png | Full confusion matrix |
| sample_predictions.png | Sample predictions |

## Notes for Member 3 (Wavelet Compression)
- Load mobilenetv2_best.pth with build_mobilenetv2(NUM_CLASSES) then load_state_dict()
- Use per_class_accuracy.json as the uncompressed baseline to compare against
- Apply the same normalization: mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]
- Image size must be 96x96

## Reproducibility
All results reproducible with seed=42. Run cells 1-24 in order.
