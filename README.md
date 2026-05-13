# Traffic Light Recognition

This repository contains the training configuration, inference scripts, and experiment notes for a YOLO-based traffic light / traffic sign recognition project.

## Task
Train an object detection model with the provided YOLO dataset and predict objects on the hidden-label test set.

## Classes
Green Light, Red Light, Speed Limit 10, Speed Limit 100, Speed Limit 110, Speed Limit 120, Speed Limit 20, Speed Limit 30, Speed Limit 40, Speed Limit 50, Speed Limit 60, Speed Limit 70, Speed Limit 80, Speed Limit 90, Stop

## Files
- `data.yaml`: Ultralytics training config
- `baseline_infer.py`: basic inference-to-CSV script
- `baseline_infer_debug.py`: debug version for inspecting predictions
- `sample_submission.csv`: submission schema
- `requirements.txt`: Python dependency list
- `112304260116_zhangxiaomin.md`: experiment report

## Dataset
The original `train/`, `val/`, and `test/` folders are not included in this GitHub repository because they are large local dataset files.

## Submission
Submit one `submission.csv` file with these columns:
- `image_id`
- `class_id`
- `x_center`
- `y_center`
- `width`
- `height`
- `confidence`

All coordinates must be YOLO-style normalized values in `[0, 1]`.

## Metric
Ranking metric: `mAP@0.5`

## Example training
```bash
yolo detect train data=data.yaml model=yolov8n.pt epochs=50 imgsz=416
```

## Example submission generation
```bash
python baseline_infer.py --model runs/detect/train/weights/best.pt --test-dir test/images --output submission.csv
```
