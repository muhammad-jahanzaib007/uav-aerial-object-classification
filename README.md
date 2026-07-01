# UAV Aerial Object Classification

> Multi-class classification of objects in drone aerial footage, with a focus on the two decisions that actually move the metric: **leakage-aware data splitting** and **class-imbalance handling**.

**Author:** Muhammad Jahanzaib Awan
**Context:** MSc Artificial Intelligence, Applied AI module, De Montfort University (2026)

> ⚠️ **Portfolio repository.** Documents approach, methodology, and results of a graded academic project. Full solution code and datasets are intentionally **not** published. Available on request for recruiters.

---

## Problem

From a VisDrone-style UAV video sequence (146 frames, 10,297 annotated object boxes, 189 tracked objects), build a multi-class image-classification dataset of cropped objects and compare models under severe real-world class imbalance.

## Key data challenges (measured, not assumed)

- Only **7 of 10** nominal classes present → reframed as a 7-class problem.
- Severe imbalance: `car` 42.1% vs `bicycle` 1.0%.
- Rare classes have very few *distinct* tracked objects (bus: 3, van: 4).
- Final dataset: **8,903 cropped objects**, all 7 classes in both train and test.

## The two decisions that drove the result

1. **Leakage-aware splitting.** Consecutive video frames contain near-identical crops of the *same* tracked object. A naïve random split leaks almost-duplicate images across train/test and **inflates accuracy**. I split by **track ID** (group split) so no object appears in both sets, then reported the naïve number too, to *quantify* the leakage effect.
2. **Imbalance handling.** Weighted loss + class-balanced sampling + augmentation, evaluated with **macro-F1 and per-class metrics**, not raw accuracy.

## Models compared

| Type | Models |
|------|--------|
| Transfer learning (main) | **ResNet18** (fine-tuned, imbalance-aware) |
| CNN comparisons | MobileNetV2, EfficientNet-B0 |
| Classical baseline | HOG features + Linear SVM / Random Forest |

Ablations: from-scratch vs transfer · with vs without imbalance handling · **track-split vs naïve-split**.

## Evaluation

Accuracy, macro & weighted Precision/Recall/F1, per-class report, confusion matrix, training curves.

## Skills demonstrated

`PyTorch` · `Computer Vision` · `Transfer Learning (ResNet/MobileNet/EfficientNet)` · `scikit-learn` · `HOG + SVM` · `Imbalanced-data methods` · `Leakage-aware experimental design`

---

© 2026 Muhammad Jahanzaib Awan. All rights reserved. See [LICENSE](LICENSE).
