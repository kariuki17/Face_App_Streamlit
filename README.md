# Face Recognition App

A Streamlit-based application that performs real-time face recognition using OpenCV and the `face_recognition` Python library. The app captures live video from a webcam, detects faces, and identifies them against a known database of images.

## Features

* 📷 **Live Webcam Feed**: Capture video directly in the browser through Streamlit.
* 🔍 **Face Detection**: Detects multiple faces in real time.
* 🧑‍🤝‍🧑 **Face Recognition**: Matches detected faces against a known dataset.
* 📂 **Customizable Database**: Easily add or remove reference images for recognition.
* ✅ **User Feedback**: Displays bounding boxes with names for recognized individuals.

## Project Goals

This project demonstrates how computer vision and machine learning can be combined to build simple, accessible face recognition systems. It can be adapted for use cases such as attendance systems, access control, or personal projects.

## Tech Stack

* **Python**
* **Streamlit** (for the web interface)
* **OpenCV** (for image capture and processing)
* **face_recognition** (for encoding and comparing faces)
* **numpy, pandas** (for data handling)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/face-recognition-app.git
   cd face-recognition-app
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the app:

   ```bash
   streamlit run app.py
   ```

## Usage

1. Add known faces in the `images/` folder (e.g., `Esther.jpg`, `John.jpg`).
2. Start the app and allow webcam access.
3. The app will detect and recognize faces in real time.
4. Bounding boxes with names appear over detected faces.

## Future Improvements

* Attendance logging system (CSV/Database).
* Multi-camera support.
* Face recognition confidence scores.
* Deployment on Streamlit Cloud.

## Disclaimer

This project is for **educational and demonstration purposes**. It is not intended for security-critical applications.
