# 🚀 Workshop 2 – Real-Time Object Detection Using Web Camera

A real-time object detection project using **YOLOv8**, **OpenCV**, and a computer's **webcam**. The system captures live video frames from the webcam, detects objects using a pretrained YOLOv8 model, and displays the detected objects with bounding boxes and labels.

---

## 📌 Project Overview

This workshop demonstrates how to implement **real-time object detection** using a webcam.

The project uses the **YOLOv8 Medium (`yolov8m.pt`)** pretrained model to identify objects from live webcam frames. Each captured frame is processed by the YOLO model, and the detected objects are displayed with bounding boxes and labels.

The implementation is performed in a **Jupyter Notebook using Python**.

---

## 🎯 Objectives

* Install and use the **Ultralytics YOLO** library.
* Load a pretrained **YOLOv8** object detection model.
* Access the computer's webcam using **OpenCV**.
* Perform real-time object detection on webcam frames.
* Draw bounding boxes and labels around detected objects.
* Display the processed frames inside Jupyter Notebook.
* Understand the basic workflow of real-time computer vision.

---

## 🛠️ Technologies Used

| Technology          | Purpose                     |
| ------------------- | --------------------------- |
| 🐍 Python           | Programming language        |
| 🤖 YOLOv8           | Object detection            |
| 📦 Ultralytics      | YOLO implementation         |
| 👁️ OpenCV          | Webcam and image processing |
| 📊 Matplotlib       | Displaying frames           |
| 📓 Jupyter Notebook | Development environment     |
| 🔥 PyTorch          | Deep learning backend       |

---

## 📂 Project Structure

```text
Workshop-2/
│
├── Workshop 2.ipynb
└── README.md
```

---

## ⚙️ Requirements

Make sure you have the following installed:

* Python 3.x
* Jupyter Notebook / JupyterLab
* Webcam
* Ultralytics
* OpenCV
* Matplotlib
* PyTorch

---

## 📥 Installation

### 1. Install Ultralytics

Open your Jupyter Notebook and run:

```python
%pip install ultralytics
```

---

### 2. Import Required Libraries

```python
from ultralytics import YOLO
import cv2
import matplotlib.pyplot as plt
from IPython.display import clear_output
```

---

## 🤖 Load the YOLOv8 Model

The project uses the pretrained **YOLOv8 Medium** model:

```python
model = YOLO("yolov8m.pt")
```

The model is automatically downloaded when it is used for the first time.

---

## 📷 Access the Webcam

Open the default webcam using OpenCV:

```python
cap = cv2.VideoCapture(0)
```

The value `0` normally represents the computer's default camera.

---

## 🔍 Real-Time Object Detection

The webcam is checked before starting the detection process:

```python
if not cap.isOpened():
    print("Error: Could not open webcam.")
```

If the webcam is available, frames are continuously captured:

```python
ret, frame = cap.read()
```

Each frame is passed to the YOLO model for object detection.

The confidence threshold used in this project is:

```python
conf=0.60
```

This means detections below the specified confidence threshold are filtered out.

---

## 🖼️ Bounding Boxes and Labels

The detected objects are visualized using:

```python
annotated_frame = results[0].plot()
```

This automatically draws bounding boxes and labels around detected objects.

The OpenCV image is then converted from **BGR to RGB** so that it can be correctly displayed using Matplotlib:

```python
annotated_frame = cv2.cvtColor(
    annotated_frame,
    cv2.COLOR_BGR2RGB
)
```

---

## 📊 Display Detection Results

The processed frame is displayed inside the Jupyter Notebook:

```python
clear_output(wait=True)

plt.figure(figsize=(10, 8))
plt.imshow(annotated_frame)
plt.title("Real-Time Object Detection")
plt.axis("off")
plt.show()
```

This continuously updates the notebook output with the latest webcam frame.

---

## 🔄 Complete Workflow

```text
Start
  │
  ▼
Install / Import Libraries
  │
  ▼
Load YOLOv8 Model
  │
  ▼
Open Webcam
  │
  ▼
Capture Video Frame
  │
  ▼
Send Frame to YOLO
  │
  ▼
Detect Objects
  │
  ▼
Draw Bounding Boxes
  │
  ▼
Convert BGR → RGB
  │
  ▼
Display Frame
  │
  └───────────────┐
                  │
                  ▼
            Capture Next Frame
```

---

## 💻 Complete Code

```python
# Install Ultralytics
%pip install ultralytics
```

```python
# Import libraries
from ultralytics import YOLO
import cv2
import matplotlib.pyplot as plt
from IPython.display import clear_output
```

```python
# Load YOLOv8 Medium model
model = YOLO("yolov8m.pt")
```

```python
# Open webcam
cap = cv2.VideoCapture(0)
```

```python
# Real-time object detection

if not cap.isOpened():
    print("Error: Could not open webcam.")
else:
    while True:
        ret, frame = cap.read()

        if not ret:
            print("Failed to capture frame.")
            break

        # Perform object detection
        results = model(
            frame,
            conf=0.60,
            verbose=False
        )

        # Draw bounding boxes and labels
        annotated_frame = results[0].plot()

        # Convert BGR to RGB for Matplotlib
        annotated_frame = cv2.cvtColor(
            annotated_frame,
            cv2.COLOR_BGR2RGB
        )

        # Display in Jupyter
        clear_output(wait=True)

        plt.figure(figsize=(10, 8))
        plt.imshow(annotated_frame)
        plt.title("Real-Time Object Detection")
        plt.axis("off")
        plt.show()

# Release webcam
cap.release()
cv2.destroyAllWindows()
```

---

## 📸 Expected Output

When the notebook is executed, the webcam feed is displayed in the Jupyter Notebook.

The YOLOv8 model identifies objects in the camera view and displays:

* Object name
* Bounding box
* Detection confidence
* Real-time annotated video frames

Example:


<img width="935" height="702" alt="image" src="https://github.com/user-attachments/assets/0604d419-18e4-4695-940b-1def1d80f089" />



---

## ⚠️ Troubleshooting

### Webcam Not Opening

If you get:

```text
Error: Could not open webcam.
```

Try the following:

1. Make sure your webcam is connected.
2. Close applications currently using the camera.
3. Check Windows camera permissions.
4. Try changing:

```python
cv2.VideoCapture(0)
```

to:

```python
cv2.VideoCapture(1)
```

if another camera is being detected first.

---

### Failed to Capture Frame

If you get:

```text
Failed to capture frame.
```

Check that the webcam is functioning properly and accessible by Python/OpenCV.

---

### YOLO Model Download

The first execution downloads:

```text
yolov8m.pt
```

This may take some time depending on your internet connection. After downloading, the model can be reused locally.

---

## 🔧 Key Parameters

### Confidence Threshold

The project uses:

```python
conf=0.60
```

You can modify this value depending on the required detection sensitivity.

For example:

```python
conf=0.50
```

or:

```python
conf=0.70
```

---

## 📚 Learning Outcomes

After completing this workshop, you should understand:

* Basics of object detection.
* How YOLO performs object detection.
* How to load a pretrained YOLO model.
* How to access a webcam using OpenCV.
* How to process video frames.
* How to visualize detection results.
* How confidence thresholds affect object detection.
* How Python libraries can be combined to create a computer vision application.

---

## 🌟 Applications

Real-time object detection can be used in many practical applications, such as:

* 🏠 Smart surveillance
* 🚗 Traffic monitoring
* 👤 People detection
* 🏭 Industrial monitoring
* 🔐 Security systems
* 🤖 Robotics
* 🚦 Intelligent transportation
* 🏪 Retail monitoring
* 📹 Smart camera systems

---

## 🚀 Future Improvements

The project can be further improved by adding:

* Real-time FPS display.
* Object counting.
* Object tracking.
* Custom-trained YOLO models.
* Detection history.
* Multiple camera support.
* Detection alerts.
* Video recording.
* Web-based interface.
* GPU acceleration.
* Custom classes for specific applications.

---

## 📝 Conclusion

This workshop successfully demonstrates **real-time object detection using a webcam** with the **YOLOv8 Medium model**.

By combining **Ultralytics YOLO, OpenCV, Matplotlib, and Python**, the system can capture live webcam frames, detect objects, annotate them with bounding boxes and labels, and display the results directly in a Jupyter Notebook.

This project provides a practical introduction to **computer vision and deep-learning-based object detection**.

---

## 👨‍💻 Author

**Sabarish A**

**Register Number:** 212225230232

---

## 📄 Project Information

**Workshop:** Workshop 2
**Topic:** Object Detection Using Web Camera
**Model:** YOLOv8 Medium (`yolov8m.pt`)
**Environment:** Jupyter Notebook
**Language:** Python

---

