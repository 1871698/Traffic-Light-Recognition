# Traffic Light Recognition

A YOLOv8-based traffic light and traffic sign detection project for model training, validation analysis, and competition-style submission generation.

## Overview

This repository contains the core code and experiment materials for a traffic light recognition task built with Ultralytics YOLO. The project focuses on:

- training an object detection model on a custom traffic dataset
- evaluating model quality with mAP, precision, recall, and confusion matrices
- generating a submission file for hidden-label test images
- documenting the full experiment process and conclusions

## Highlights

- Model: `YOLOv8s`
- Input size: `640`
- Epochs: `80`
- Optimizer: `AdamW`
- Validation `mAP@0.5`: `0.968`
- Validation `mAP@0.5:0.95`: `0.839`
- Competition score: `0.9336`
- Current ranking noted in report: `2`

## Detection Classes

`Green Light`, `Red Light`, `Speed Limit 10`, `Speed Limit 20`, `Speed Limit 30`, `Speed Limit 40`, `Speed Limit 50`, `Speed Limit 60`, `Speed Limit 70`, `Speed Limit 80`, `Speed Limit 90`, `Speed Limit 100`, `Speed Limit 110`, `Speed Limit 120`, `Stop`

## Repository Structure

```text
.
├── baseline_infer.py
├── baseline_infer_debug.py
├── data.yaml
├── requirements.txt
├── sample_submission.csv
├── 112304260116_zhangxiaomin.md
└── assets/
    └── report/
```

## Environment

- Python `3.11`
- PyTorch `2.5.1+cu121`
- Ultralytics YOLO `8.4.49`
- GPU: `NVIDIA GeForce RTX 3090`

## Quick Start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Train the model

```bash
yolo detect train data=data.yaml model=yolov8s.pt epochs=80 imgsz=640 batch=32 device=0 workers=8 patience=20 name=round1_yolov8s_640
```

### 3. Generate predictions for submission

```bash
python baseline_infer.py --model runs/detect/round1_yolov8s_640/weights/best.pt --test-dir test/images --output submission.csv
```

## Dataset Note

The original `train/`, `val/`, `test/`, local weight files, and full training output folders are not committed to GitHub because they are large local assets. This repository keeps the code, configuration, report, and selected result visualizations needed for project presentation and reproduction.

## Result Preview

### Training Curves

![Training curves](assets/report/results.png)

### Confusion Matrix

![Confusion matrix](assets/report/confusion_matrix.png)

### Sample Predictions

![Prediction example 1](assets/report/val_batch0_pred.jpg)
![Prediction example 2](assets/report/val_batch1_pred.jpg)

## Experiment Report

The full experiment write-up is available here:

- [112304260116_zhangxiaomin.md](112304260116_zhangxiaomin.md)

## Core Files

- `baseline_infer.py`: converts model predictions into the required CSV format
- `baseline_infer_debug.py`: debugging helper for inspecting prediction results
- `data.yaml`: dataset and class configuration for YOLO
- `sample_submission.csv`: expected submission schema

## Future Improvements

- strengthen recognition of `Green Light` and `Red Light`
- improve small-object detection for distant traffic signs
- try larger backbones such as `YOLOv8m` or `YOLOv8l`
- optimize data augmentation and hyperparameters for better generalization
