# 🚗 SafeDrive.ai v3.0

### Real-Time Driver Safety Monitoring System
> *Accident Prevention · Before It Happens*

---

## ✅ All 8 Objectives — Working

| # | Objective | Module | Method |
|---|-----------|--------|--------|
| 1 | Drowsiness & Yawning | `drowsiness_detection.py` | EAR < 0.25 → Drowsy · MAR > 0.60 → Yawn |
| 2 | Emotion Detection | `emotion_detection.py` | 6-class geometry from 468 landmarks |
| 3 | Voice Stress | `stress_detection.py` | MFCC + Pitch + RMS + ZCR → RandomForest |
| 4 | Visibility Detection | `visibility_detection.py` | Brightness / Contrast / Laplacian |
| 5 | Child in Locked Vehicle | `visibility_detection.py` | Frame differencing when engine OFF |
| 6 | Real-time Risk Score | `risk_engine.py` | Weighted 0–10 with 30-frame smoothing |
| 7 | Web Dashboard + Alarms | `frontend/index.html` | Full cockpit UI with audio alarms |
| 8 | Deployment | `backend/app.py` | Flask server OR direct HTML |

---

## 🚀 Quick Start

### Option 1: Browser Only (No Installation Required)
```
1. Open:  frontend/index.html  in Chrome or Edge
2. Login: demo@test.com / demo1234
3. Click  ▶ Start  → Allow camera & microphone
4. Click  🔔 Test Alarm  to test the alarm system
```

### Option 2: Flask Server (Full Features)
```bash
pip install -r requirements.txt
cd backend
python app.py
# Visit: http://localhost:5000
```

### Option 3: Windows Batch (Easiest)
```
Double-click start.bat → Choose option
```

### Option 4: Python Direct (Testing Modules)
```bash
cd backend
python run_all.py
# Controls: E=engine toggle | R=reset | Q=quit
```

---

## 🔐 Login Credentials

| Email | Password | Role |
|-------|----------|------|
| `demo@test.com` | `demo1234` | Driver |
| `admin@safedrive.ai` | `admin123` | Admin |
| `test@driver.com` | `test1234` | Driver |
| Guest button | — | Limited |

---

## 🚨 Alarm System (v3.0 Feature)

SafeDrive.ai v3 includes a complete multi-level alarm system:

| Alarm Type | Trigger | Sound |
|------------|---------|-------|
| 🚨 High Danger | Risk score ≥ 7 for 5 frames | Emergency siren |
| 😴 Drowsiness | EAR < 0.25 for 18 frames | Alert tone (×3) |
| 🥱 Yawning | MAR > 0.60 for 12 frames | Single beep |
| 👶 Child in Vehicle | Motion + engine OFF | Emergency siren |
| 😰 High Stress | Voice stress detected | Alert tone |
| 🌫️ Poor Visibility | Low brightness/contrast/blur | Beep |

**Features:**
- Real audio via Web Audio API (no external files)
- Animated alarm modal with risk score display
- Full-screen danger glow effect
- Snooze (60 seconds) or Acknowledge
- Sound on/off toggle
- Alarm history log
- Auto-dismiss when risk drops below threshold

---

## 📁 Project Structure

```
SafeDrive_v3/
├── frontend/
│   └── index.html              ← Full dashboard (open in Chrome)
├── backend/
│   ├── app.py                  ← Flask server (v3.0)
│   ├── drowsiness_detection.py ← EAR/MAR detection
│   ├── emotion_detection.py    ← 6-class emotion
│   ├── stress_detection.py     ← Voice stress analysis
│   ├── visibility_detection.py ← Visibility + child
│   ├── risk_engine.py          ← Weighted risk scoring
│   └── run_all.py              ← All modules combined
├── docs/
│   ├── API_DOCUMENTATION.md
│   ├── CONFIGURATION.md
│   ├── DEPLOYMENT.md
│   └── VIVA_NOTES.md
├── requirements.txt            ← Pinned dependencies
├── start.bat                   ← Windows launcher
├── .gitignore
└── README.md
```

---

## 📐 Key Formulas

```
EAR = (||p2-p6|| + ||p3-p5||) / (2 × ||p1-p4||)
      EAR < 0.25 for 18 frames → DROWSY

MAR = (A + B + C) / (2D)
      MAR > 0.60 for 12 frames → YAWNING

Risk = (Drowsiness × 0.35) + (Stress × 0.25) + (Environment × 0.20) + (Child × 0.20)
       Smoothed over 30-frame rolling window
       0–3 = Low  ·  3–6 = Medium  ·  6–10 = High
```

---

## 🔧 Tech Stack

| Component | Technology |
|-----------|-----------|
| Face Detection | MediaPipe FaceMesh (468 landmarks) |
| Computer Vision | OpenCV |
| Audio Analysis | Librosa (MFCC, pYIN, RMS, ZCR) |
| ML Classifier | scikit-learn RandomForest |
| Alarm Audio | Web Audio API (synthesised) |
| Web Framework | Flask 3.0 |
| Frontend | HTML5 / CSS3 / Vanilla JS |

---

## 🧪 Test Individual Modules

```bash
cd backend

python drowsiness_detection.py  # EAR, MAR, blinks
python emotion_detection.py     # 6 emotions live
python stress_detection.py      # Voice analysis
python visibility_detection.py  # Fog/blur/low-light + child
python risk_engine.py           # Risk scoring demo
```

---

## ⚙️ Quick Configuration

```python
# drowsiness_detection.py
EAR_THRESH = 0.25    # Lower = more sensitive (0.20 for night)
MAR_THRESH = 0.60    # Yawn threshold
EAR_CONSEC = 18      # Frames until trigger (~0.9s at 20fps)

# risk_engine.py
WEIGHTS = {"drowsiness": 0.35, "stress": 0.25, "environment": 0.20, "child": 0.20}
```

---

## 📊 Performance

| Metric | Value |
|--------|-------|
| Detection FPS | 20–30 |
| Drowsiness accuracy | ~92% |
| Stress accuracy | ~78% (demo model) |
| Visibility accuracy | ~88% |
| Alert latency | < 200ms |
| Memory usage | 200–400MB |

---

*SafeDrive.ai v3.0 · CSE Mini Project · Real-time accident prevention*
