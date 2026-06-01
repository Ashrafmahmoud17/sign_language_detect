# 🤟 Sign Language Detection

Real-time hand gesture recognition system that detects sign language using a webcam. Built with MediaPipe for hand landmark detection and Scikit-learn for classification.

---

## 📌 Overview

The system captures hand landmarks from a live webcam feed, extracts (x, y) coordinates of 21 hand keypoints, and classifies the gesture using a trained Logistic Regression model. Currently supports two gestures: **Hello** and **Love**.

---

## 🗂️ Project Structure

```
sign_language_detect/
│
├── collect_data.py        # Collect training data for each gesture via webcam
├── train_model.py         # Train and save the ML model and scaler
├── predict.py             # Real-time prediction using webcam
│
├── dataset.csv            # Collected hand landmark data (auto-generated)
├── scaler.pkl             # Saved MinMaxScaler (auto-generated)
└── model.pkl              # Saved Logistic Regression model (auto-generated)
```

---

## ⚙️ Requirements

```bash
pip install numpy opencv-python mediapipe scikit-learn pandas
```

---

## 🚀 How to Use

### Step 1 — Collect Data
Run the data collection script and perform each gesture in front of the webcam. Press **Q** to stop recording for each gesture.

```bash
python collect_data.py
```

This will generate `dataset.csv` with hand landmark coordinates labeled for each gesture.

---

### Step 2 — Train the Model
```bash
python train_model.py
```

This will:
- Load `dataset.csv`
- Split into train/test sets (90/10)
- Scale features using `MinMaxScaler`
- Train a `LogisticRegression` model
- Save `scaler.pkl` and `model.pkl`

---

### Step 3 — Run Real-Time Prediction
```bash
python predict.py
```

Point your hand at the webcam — the predicted gesture label will appear on screen. Press **Q** to quit.

---

## 🧠 Model Details

| Item | Detail |
|------|--------|
| Algorithm | Logistic Regression |
| Features | 42 values (x, y) × 21 MediaPipe hand landmarks |
| Scaler | MinMaxScaler |
| Supported Gestures | `hello`, `love` |
| Train/Test Split | 90% / 10% |

---

## ➕ Adding New Gestures

1. Add a new data collection block in `collect_data.py` (copy the `hello` or `love` block and rename the list and label)
2. Re-run `collect_data.py` to collect samples for the new gesture
3. Re-run `train_model.py` to retrain the model

---

## 📸 How It Works

```
Webcam Frame
     ↓
MediaPipe Hand Detection
     ↓
Extract 21 Landmarks (x, y) → 42 features
     ↓
MinMaxScaler normalize
     ↓
Logistic Regression predict
     ↓
Display label on frame
```

---

## 📝 Notes

- Make sure your webcam is properly connected before running any script
- Good lighting improves detection accuracy
- Collect at least 200–300 samples per gesture for better accuracy
- Update file paths in the scripts if your project folder is in a different location
