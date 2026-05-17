# Facial Expression Recognition

This repository contains a Facial Expression Recognition project built using a custom Convolutional Neural Network (CNN) in TensorFlow, paired with a C++ GUI frontend using the Qt framework.

The application classifies human facial expressions into one of seven emotion categories: **Angry, Disgust, Fear, Happy, Neutral, Sad,** and **Surprise**. It provides an interactive GUI that allows users to easily select an image file, run the prediction model, and view the results.

---

## 🔹 Prerequisites

### System Requirements

* **Operating System:** Linux (The GUI application is developed using Qt and is currently tested on Linux systems).

### Python (Backend)

Ensure Python 3.x is installed along with the following libraries:

* `tensorflow`
* `opencv-python`
* `numpy`
* `splitfolders`
* `matplotlib`

### C++ & Qt (Frontend)

The frontend utilizes the Qt5 framework (specifically `QApplication`, `QProcess`, `QLabel`, `QFileDialog`, and `QPixmap`). To install the necessary C++ Qt libraries on Ubuntu/Debian-based systems, run:

```bash
sudo apt install qtbase5-dev

```

---

## 🔹 Installation & Usage

**1. Clone the repository:**
Download the project files to your local Linux machine.

**2. Compile the C++ Frontend:**
Navigate to the repository directory in your terminal and compile `main.cpp` into an executable named `qt_app` using the following command:

```bash
g++ -fPIC main.cpp -o qt_app $(pkg-config --cflags --libs Qt5Widgets)

```

*(Alternatively, you can build `main.cpp` using Qt Creator or CMake).*

**3. Set up the directory:**
Ensure that your trained Keras model (`custom1.h5`) and the Python backend script (`model.py`) are placed in the exact same directory as your newly compiled `qt_app` executable.

**4. Run the application:**
Execute the compiled application:

```bash
./qt_app

```

Use the GUI to select an image file and classify the facial expression!

---

## 🔹 How It Works

1. **Image Selection:** The user selects an image file through the C++ Qt GUI.
2. **Process Communication:** The frontend passes the absolute image path to the Python backend utilizing `QProcess`.
3. **Backend Execution (`model.py`):**
* Detects and preprocesses the face in the image.
* Loads the custom CNN model (`custom1.h5`).
* Runs the inference/prediction.


4. **Result Display:** The predicted emotion is returned to the C++ frontend and displayed on the GUI.

---

## 🔹 Model & Architecture Details

* **Architecture:** Custom Convolutional Neural Network (CNN)
* **Accuracy:** ~75% on the test set
* **Input Size:** 64x64 grayscale face image
* **Model File:** `custom1.h5` (Trained Keras model)

---

## 🔹 Preprocessing Techniques

Before the model makes a prediction, the input image undergoes the following automated preprocessing steps via `model.py`:

* **Face Detection:** Locates the face using OpenCV Haar Cascades (`haarcascade_frontalface_default.xml`).
* **Color Conversion:** Converts the image to grayscale.
* **Cropping & Resizing:** Isolates the detected face region and resizes it to the required 64x64 resolution.
* **Normalization:** Scales pixel values appropriately (handled internally by the model if applicable).

*Note: If no face is detected by the Haar Cascade during preprocessing, the program will return an error message.*

---

## 🔹 Notes & Future Enhancements

* **Single Face Processing:** Currently, only one face is processed per image (the program selects the first detected face).
* **Optimal Conditions:** Predictions are most accurate when the subject's face is clearly visible, well-lit, and front-facing.
* **Future Work:** Real-world performance can be improved by introducing dataset augmentation and integrating real-time webcam video feeds.
