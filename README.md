# Industrial AI Vision

A real-time **Industrial AI Vision** system for detecting Personal Protective Equipment (PPE) on workers using **YOLO (Ultralytics)** and **OpenCV**.

The system analyzes video files or a live webcam feed, draws bounding boxes for detected safety gear, and can export an annotated output video.

## Detected classes

| Class   | Description        |
|---------|--------------------|
| Person  | Worker / human     |
| Helmet  | Hard hat / helmet  |
| Vest    | Safety vest        |
| Boots   | Safety boots       |

## Features

- Real-time PPE detection with YOLOv8 (Ultralytics)
- Supports dedicated PPE weights (`yolov8n-ppe.pt`, `best.pt`, `ppe.pt`) or COCO person detection with zone-based PPE estimation
- Video file input (auto-detects `.mp4`, `.avi`, `.mov`, `.mkv` in the project folder) or webcam
- Automatic installation of missing Python dependencies on first run
- Optional GPU acceleration (CUDA) with CPU fallback
- Annotated preview window and exported video (`output_detected.mp4`)
- Color-coded labels per class with confidence scores

## Requirements

- Python 3.8+
- Webcam (optional, for live mode)
- NVIDIA GPU with CUDA (optional, for faster inference)

Core packages (installed automatically if missing): `ultralytics`, `opencv-python`, `torch`, `torchvision`, `numpy`, `tqdm`.

## Quick start

Clone the repository and run:

```bash
python work.py
```

If no video path is given, the script uses the first supported video file found in the current directory.

### Usage

```bash
# Process a specific video file
python work.py path/to/your_video.mp4

# Use the default webcam (index 0)
python work.py --webcam

# Use a specific camera index
python work.py --webcam 1
```

Press **Q** in the preview window to stop.

## PPE model (optional)

Place a trained YOLO weights file in the project root with one of these names:

- `yolov8n-ppe.pt`
- `best.pt`
- `ppe.pt`

If none are found, the system falls back to `yolov8n.pt` (COCO) and estimates helmet, vest, and boot regions from detected persons.

## Output

- **Preview:** OpenCV window titled `PPE`
- **Video:** `output_detected.mp4` (saved when processing a file)

## Project structure

```
Industrial-AI-Vision/
├── work.py              # Main detection script
├── README.md
├── LICENSE
└── output_detected.mp4  # Generated after video processing
```

## How it works

1. Loads a YOLO model (PPE-specific weights if available, otherwise COCO).
2. Runs inference on each frame at 640×640 with configurable confidence and IoU thresholds.
3. Normalizes class names (e.g. `hard hat` → `helmet`) and draws bounding boxes.
4. In COCO mode, simulates PPE zones on each detected person using fixed relative regions (head, torso, feet).

## License

This project is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 [Prince Maurya](https://github.com/alwaysprince05).

## Author

**Prince Maurya** — [@alwaysprince05](https://github.com/alwaysprince05)
