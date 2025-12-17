# DJI Tello Object Following using Fuzzy Logic & Computer Vision

This project implements an autonomous object-tracking system for the **DJI Tello Drone**. It utilizes **Computer Vision (OpenCV)** to detect objects based on color and applies **Fuzzy Logic Control** to smooth the drone's movements (Yaw, Pitch, Throttle) in real-time.

## 🎥 Project Demo
> https://github.com/user-attachments/assets/5e86c58f-9971-4242-9b5a-934fbc9f69a2



## 📂 File Structure & Description

The project is organized into source code, assets, and legacy files for better maintainability.

### 🧠 Core System (`/src`)
* **`src/main.py`**
    The main execution script. It connects to the drone, handles the video stream, orchestrates the tracking logic, and sends commands to the Tello. **Run this file to start.**

* **`src/Color_tracking.py`**
    The computer vision module. It handles image processing tasks such as:
    * Converting frames to HSV color space.
    * Creating masks for the target color.
    * Calculating contours and the center point $(cx, cy)$ of the object.

* **`src/Fuzzy.py`**
    The "Brain" of the control system. Unlike standard PID, this file implements **Fuzzy Logic** membership functions (e.g., Close, Ideal, Far) to determine the drone's velocity. It makes the drone's movement smoother and more human-like compared to rigid PID controllers.

### 🛠️ Utilities (`/src`)
* **`src/hsv_trackbar.py`**
    A calibration tool. Run this script to open a window with sliders (trackbars). It allows you to manually tune the **HSV (Hue, Saturation, Value)** lower and upper bounds to find the perfect color detection settings for your specific environment.

* **`src/Response_monitor.py`**
    A data visualization tool. It plots the system's response (Error vs. Time) or logs data to analyze stability and correction speed.

### 🗄️ Archives (`/legacy`)
* **`legacy/legacy_control.py`**
    *Experimental/Backup File*. Contains previous iterations of the control algorithms (standard PID tests). Kept for educational reference.

## 🚀 How to Run

1.  **Install Dependencies**
    Ensure you have Python installed, then install the required libraries listed in `requirements.txt`:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Calibrate Color (Optional)**
    If the lighting conditions change, run the trackbar tool to get new HSV values:
    ```bash
    python src/hsv_trackbar.py
    ```

3.  **Start Tracking**
    Connect your laptop to the Tello Wi-Fi and run the main script:
    ```bash
    python src/main.py
    ```

## ⚠️ Safety Precautions
* **Emergency Stop:** Always be ready to terminate the script (Ctrl+C) or grab the drone if it behaves unexpectedly.
* **Lighting:** Ensure the environment is well-lit for accurate color detection.
* **Space:** Test in an open area to avoid collisions.

---
*Created for the Final Project on Intelligent Control Systems (Sistem Kendali Cerdas).*
