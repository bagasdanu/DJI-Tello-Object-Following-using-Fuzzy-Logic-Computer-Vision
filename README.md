# DJI Tello Object Following using Fuzzy Logic & Computer Vision

![Python](https://img.shields.io/badge/Code-Python_3.8+-blue?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/Vision-OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![DJI Tello](https://img.shields.io/badge/Drone-DJI_Tello-orange?style=for-the-badge&logo=dji&logoColor=white)
![Fuzzy Logic](https://img.shields.io/badge/Control-Fuzzy_Logic-red?style=for-the-badge)

This project implements an autonomous object-tracking system for the **DJI Tello Drone**. It utilizes **Computer Vision** (OpenCV) to detect objects based on specific colors and applies a **Fuzzy Logic Controller** to smooth the drone's movements (Yaw, Pitch, Throttle) in real-time, providing a more human-like response compared to traditional PID.

## Project Demo 

> **Watch the drone in action:** Tracking a colored object autonomously.

https://github.com/user-attachments/assets/5e86c58f-9971-4242-9b5a-934fbc9f69a2

## Tech Stack & Libraries

| Component | Library/Tool | Function |
|:---|:---|:---|
| **Drone SDK** | `djitellopy` | Official Python wrapper to communicate with Tello via Wi-Fi (UDP). |
| **Vision** | `opencv-python` | Image processing, HSV color conversion, and contour detection. |
| **Control Logic** | `scikit-fuzzy` / Custom | Implementation of Fuzzy Membership Functions (Low, Medium, High). |
| **Visualization** | `matplotlib` | Real-time plotting of error response (optional debug tool). |

## File Structure & Description

The project is organized into source code, assets, and legacy files for better maintainability.

### Core System (`/src`)

* **`src/main.py`**  
  The main execution script. It connects to the drone, handles the video stream, orchestrates the tracking logic, and sends commands to the Tello. **Run this file to start.**

* **`src/color_tracking.py`**  
  The computer vision module. It handles image processing tasks such as:
  * Converting frames to HSV color space.
  * Creating masks for the target color.
  * Calculating contours and the center point $(cx, cy)$ of the object.

* **`src/fuzzy_logic.py`**  
  The "Brain" of the control system. Unlike standard PID, this file implements **Fuzzy Logic** membership functions (e.g., Close, Ideal, Far) to determine the drone's velocity. It makes the drone's movement smoother and more human-like.

### Utilities (`/src`)

* **`src/hsv_trackbar.py`**  
  A calibration tool. Run this script to open a window with sliders (trackbars). It allows you to manually tune the **HSV (Hue, Saturation, Value)** lower and upper bounds to find the perfect color detection settings for your specific environment.

* **`src/response_monitor.py`**  
  A data visualization tool. It plots the system's response (Error vs. Time) or logs data to analyze stability and correction speed.

### Archives (`/legacy`)

* **`legacy/legacy_control.py`**  
  *Experimental/Backup File*. Contains previous iterations of the control algorithms (standard PID tests). Kept for educational reference.

## How to Run

### 1. Prerequisites

Ensure you have Python installed, then install the required libraries:
```bash
pip install -r requirements.txt
```

*(If `requirements.txt` is missing, run: `pip install djitellopy opencv-python numpy scikit-fuzzy`)*

### 2. Calibrate Color (Optional)

Lighting conditions affect color detection. If the drone doesn't detect the object, run the calibration tool:
```bash
python src/hsv_trackbar.py
```

*Adjust the sliders until only your target object is white (in the mask window) and the background is black.*

### 3. Start Tracking

Connect your laptop to the Tello Wi-Fi and run the main script:
```bash
python src/main.py
```

## Safety Precautions

* **Emergency Stop:** Always be ready to terminate the script (Ctrl+C) or grab the drone if it behaves unexpectedly.
* **Lighting:** Ensure the environment is well-lit for accurate color detection.
* **Space:** Test in an open area to avoid collisions.
