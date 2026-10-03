<div align="center">

# Vision Reality
### Webcam computer vision, gesture control, and augmented reality

**Python · OpenCV · MediaPipe · YOLOv8 · PyTorch**

[Setup](#setup) · [Controls](#controls) · [Architecture](#architecture)

</div>

## Overview

Vision Reality combines webcam-based hand tracking, person segmentation, background replacement, object detection, and marker-based AR in one interactive desktop application.

The OpenCV window is named **RealityFrame** in the current source. The GitHub repository is **Vision-Reality**.

## Capabilities

- Switch between portal and full-person invisibility with a pinch gesture.
- Capture a reference background and blend it into selected regions.
- Draw an AR overlay on an ArUco marker.
- Select a focus region with the mouse.
- Show YOLO labels, confidence values, FPS, and GPU status.
- Cache object detections between inference frames.

## Setup

### Hardware and dependencies

A webcam and a desktop environment capable of opening an OpenCV window are required.

**The current YOLO module explicitly selects CUDA.** A compatible NVIDIA GPU and CUDA-enabled PyTorch are required for the code as written; CPU fallback is not implemented in that module.

```bash
git clone https://github.com/SuhaibIqbal12/Vision-Reality.git
cd Vision-Reality
python -m venv .venv
```

Activate the environment:

```bash
# macOS / Linux
source .venv/bin/activate
```

```powershell
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
```

Install a CUDA-enabled PyTorch build appropriate to your machine, then the remaining dependencies:

```bash
pip install -r requirements.txt
pip install ultralytics
```

The checked-in requirements file lists OpenCV, MediaPipe, and NumPy, but does not list PyTorch or Ultralytics even though the source imports them. MediaPipe must provide the `mp.solutions` APIs used by the code. Dependency versions are currently unpinned.

## Run

```bash
python main.py
```

Keep the camera stationary and the scene clear during initial background capture. The YOLO detector uses `yolov8m.pt`; the model weights are not committed and may need to download on first use.

For AR mode, use [the included marker](assets/marker_0.png). Marker utilities are in `tools/`.

## Controls

| Input | Action |
| --- | --- |
| Pinch gesture | Switch portal / full-person invisibility |
| `q` | Quit |
| `b` | Capture a new reference background |
| `r`, then four mouse clicks | Reset and select a focus region |
| `f` | Toggle focus after a region has been selected |
| `a` | Toggle AR overlay |
| `v` | Toggle AR tracking frame |

## Architecture

| Path | Responsibility |
| --- | --- |
| `main.py` | Webcam loop, effects, controls, and frame composition |
| `vision/` | Hand tracking, gestures, portals, and YOLO detection |
| `core/background.py` | Reference background capture |
| `graphics/renderer.py` | HUD and portal graphics |
| `ar/` | Marker tracking and perspective overlay |
| `assets/` | Marker image |
| `tools/` | Marker generation and inspection |

## Current limitations

- Camera, lighting, background stability, and GPU performance affect the experience.
- Dependency compatibility needs to be checked on the target machine.
- The repository includes marker utilities rather than a complete automated test suite.
- Privacy and surveillance uses are possible areas of exploration, not validated capabilities.

## Future directions

Voice commands, custom detection models, and richer spatial AR remain future work.

Maintained by **Mohammed Suhaib Iqbal** · B.Tech CSE (AI & ML).
