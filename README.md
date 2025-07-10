🔐 CAPTCHA Solver Using Deep Learning (Chrome Extension Integration)

This project implements a powerful Text-based CAPTCHA Solver using a CNN + BiLSTM + CTC deep learning model. The solver is trained to decode alphanumeric CAPTCHA images using TensorFlow and integrates with a Chrome Extension to automatically solve CAPTCHAs on web pages in real-time.

🧠 Project Highlights

✅ Solves alphanumeric/text-based CAPTCHA images

🧠 Trained with CNN + BiLSTM + CTC loss (TensorFlow)

🔥 Dual-model comparison (fallback using 2 trained models)

🌐 Flask backend server for inference

💡 Chrome Extension integration (JavaScript)

🖼️ Automated preprocessed + predicted image visualization

⚙️ REST API for inference (/predict endpoint)

💾 Real-time prediction using uploaded images


🏗️ Tech Stack

Component	Tech Used

Model	CNN + BiLSTM + CTC (TensorFlow / Keras)

Training	Python, TensorFlow, Matplotlib

API Server	Flask

Browser	Chrome Extension (JavaScript)

Image Format	.png (grayscale, 200x80 resolution)

🧪 Model Architecture

Input Image (200x80x1)
│
├── Conv2D → MaxPool
├── Conv2D → MaxPool
├── Reshape
├── Dense → Dropout
├── BiLSTM → BiLSTM
└── Dense (Softmax) → CTC Loss

Two models are trained and compared in real-time:

Model 1: DATASET.h5 trained on segmented/filtered dataset

Model 2: ALL_IN_ONE.h5 trained on full-range CAPTCHAs

Final prediction is chosen based on model confidence score.

🛠️ Setup Instructions

1. 🧠 Train the Model

Skip this if you already have DATASET.h5 and ALL_IN_ONE.h5 inside MODELS/

python train.py

This will:

Load and preprocess CAPTCHA images

Build and train the model with CTC loss

Save best model to MODELS/DATASET.h5

Generate visual outputs in predicted_images/

2. 🚀 Start Flask Backend Server

python server.py: This will expose the /predict endpoint at http://localhost:5001/predict

Accepts image via POST (form-data)

Returns predicted CAPTCHA text

3. 🌐 Use Chrome Extension
   
Go to chrome://extensions

Enable Developer Mode

Click Load Unpacked and select chrome-extension/

Visit any CAPTCHA page where the extension is enabled

It will:

Capture CAPTCHA image

Upload it to backend

Auto-fill the input field with predicted text

Ensure server is running at http://localhost:5001 or update the content.js with your server's IP.

🖼️ Outputs and Visuals

During training:

Preprocessed image (transposed) → preprocessed_images/

Final prediction saved → predicted_images/

At inference:

Model 1 and Model 2 both print predicted output and confidence.

Model with higher score is selected.

⚙️ Prediction Logic

In server.py:

Load both models and define separate StringLookup vocabularies.

Preprocess the uploaded image (image.png)

Predict using both models

Decode outputs using ctc_decode

Compare model confidences

Return highest scoring prediction

