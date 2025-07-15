import streamlit as st
import cv2
import numpy as np
from PIL import Image
import io

# Title and Instructions
st.title("🔍 Face Detection App using Viola–Jones (Haar Cascade)")
st.markdown("""
Welcome to the Face Detection App!

This app detects faces in uploaded images using OpenCV's Haar Cascade classifier.

### 👉 How to Use:
1. Upload an image.
2. Pick a rectangle color.
3. Adjust detection parameters (`scaleFactor` and `minNeighbors`).
4. Click **Detect Faces**.
5. Download the output image if you like!
""")

# Load Haar cascade
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

# Upload image
uploaded_file = st.file_uploader("📤 Upload an Image", type=['jpg', 'jpeg', 'png'])

# Pick color
rect_color = st.color_picker("🎨 Pick Rectangle Color", "#00FF00")

# Convert hex to BGR
def hex_to_bgr(hex_color):
    hex_color = hex_color.lstrip('#')
    rgb = tuple(int(hex_color[i:i+2], 16) for i in (0, 2, 4))
    return rgb[::-1]  # RGB to BGR

# Detection parameters
scale_factor = st.slider("🔧 Scale Factor", min_value=1.05, max_value=1.5, value=1.1, step=0.05)
min_neighbors = st.slider("👥 Min Neighbors", min_value=1, max_value=10, value=5)

if uploaded_file is not None:
    image = Image.open(uploaded_file).convert('RGB')
    img_array = np.array(image)
    gray = cv2.cvtColor(img_array, cv2.COLOR_RGB2GRAY)

    if st.button("🔍 Detect Faces"):
        faces = face_cascade.detectMultiScale(
            gray, scaleFactor=scale_factor, minNeighbors=min_neighbors
        )

        for (x, y, w, h) in faces:
            cv2.rectangle(img_array, (x, y), (x + w, y + h), hex_to_bgr(rect_color), 2)

        st.image(img_array, caption=f"✅ {len(faces)} face(s) detected", use_column_width=True)

        # Save result
        result_img = Image.fromarray(img_array)
        buf = io.BytesIO()
        result_img.save(buf, format="JPEG")
        byte_im = buf.getvalue()

        # Download button
        st.download_button(
            label="📥 Download Processed Image",
            data=byte_im,
            file_name="detected_faces.jpg",
            mime="image/jpeg"
        )
