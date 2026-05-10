# Hand Gesture Mouse Control

A computer vision application that lets you control your mouse using hand gestures captured from a webcam. Built with Google MediaPipe for hand landmark detection and PyAutoGUI for mouse automation.


---

## How It Works

The system detects 21 hand keypoints per frame using a pre-trained MediaPipe model, classifies the hand pose into one of five gestures, and maps each gesture to a mouse action in real time.

| Gesture | Action |
|---|---|
| Pointing (index finger extended) | Move cursor in the indicated direction |
| Fist | Left click |
| Peace sign (index + middle) | Right click |
| Open hand | Idle / stop |

Pointing supports 8 directions: UP, DOWN, LEFT, RIGHT, and the four diagonals.

---

## Requirements

- Python 3.x
- Webcam
- Local machine access (webcam + mouse control cannot run in the cloud)

```bash
pip install mediapipe opencv-python pyautogui numpy
```

The pre-trained model file `hand_landmarker.task` is included in the repo. If it's missing, the notebook will download it automatically from Google's MediaPipe model registry.

---

## Running the Project

**Option A — Local Jupyter:**

1. Clone the repo
2. Install dependencies (above)
3. Update the folder path variable in the notebook to your local directory
4. Run all cells in `CV_Hand_Gesture_Recognition.ipynb`

**Option B — Google Colab with local runtime:**

1. Install dependencies on your local machine
2. Start a local Jupyter server: `jupyter server`
3. In Colab, connect to a local runtime using the server URL
4. Run the notebook — webcam and mouse control go through your machine

---

## Gesture Detection Details

- **Model:** MediaPipe `hand_landmarker` (TensorFlow Lite, float16)
- **Detection confidence:** 0.7
- **Max hands:** 1
- **Cursor speed:** 8 px/frame
- **Click cooldown:** 15 frames (prevents accidental double-clicks)
- **PyAutoGUI fail-safe:** enabled — move cursor to a screen corner to abort

---

## Project Structure

```
.
├── CV_Hand_Gesture_Recognition.ipynb   # Main application notebook
└── hand_landmarker.task                # Pre-trained MediaPipe model (7.8 MB)
```

---

## Notes

- Designed for single-hand use
- Assumes ~30 FPS webcam for accurate frame timing
- PyAutoGUI's fail-safe will terminate the session if the cursor reaches a screen corner — this is intentional
