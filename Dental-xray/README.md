# 🦷 Dental Radiograph Analysis

## Overview
Deep learning pipeline for automated dental pathology detection and segmentation in X-ray images.

## Models
- **YOLOv8m** — object detection
- **SAM2** — pixel-level segmentation

## Pathologies Detected
- Caries
- Deep Caries
- Impacted Teeth
- Periapical Lesion

## Dataset
- 800 annotated dental X-ray images from Roboflow/DENTEX
- Train/Val/Test split

## Results
| Class | Precision | Recall | mAP50 |
|-------|-----------|--------|-------|
| All | 0.596 | 0.567 | 0.556 |
| Caries | 0.521 | 0.444 | 0.525 |
| Deep Caries | 0.531 | 0.625 | 0.576 |
| Impacted | 0.706 | 1.000 | 0.903 |
| Periapical Lesion | 0.625 | 0.200 | 0.221 |

## Tech Stack
Python, YOLOv8, SAM2, Roboflow, Google Colab
