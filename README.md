# 🔍 MoodLens — On-Device AI Emotion Detector

![On-Device AI](https://img.shields.io/badge/AI-On--Device-7C6AFF?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Android-green?style=for-the-badge)
![Privacy](https://img.shields.io/badge/Privacy-100%25-4fffb0?style=for-the-badge)

> Real-time facial emotion detection running **100% on your Android device** — no cloud, no internet required.

---

## 🎯 Problem

Most emotion detection apps rely on cloud APIs:
- ❌ Privacy risk — your face data goes to remote servers
- ❌ Fails without internet
- ❌ Slow due to network latency
- ❌ Costly API calls

## ✅ Solution — MoodLens

MoodLens runs all AI inference **directly on your Android device** using real-time camera pixel analysis. Zero data leaves your phone.

---

## 📱 Demo

🔗 **Live App:** https://rohi-nagedram.github.io/moodlens/

---

## ⭐ Features

| Feature | Detail |
|---|---|
| 6 Emotions | Happy, Sad, Angry, Surprised, Fearful, Neutral |
| Real-Time | Updates every ~0.5 seconds |
| 100% On-Device | Zero cloud API calls |
| Works Offline | Airplane mode supported |
| Privacy First | No data stored or transmitted |
| Beautiful UI | Dark theme with gradient design |

---

## 🛠️ Tech Stack

- **MIT App Inventor** — Android app framework
- **WebViewer** — Renders AI interface
- **HTML5 + JavaScript** — On-device AI engine
- **Canvas API** — Real-time pixel analysis
- **GitHub Pages** — Hosting

---

## 🧠 How On-Device AI Works

```
Camera Frame
     ↓
Canvas Pixel Analysis (on-device)
     ↓
Brightness + Redness + Warmth + Contrast Metrics
     ↓
Emotion Score Computation
     ↓
Real-Time Result Display
```

All steps happen **locally on the device**. No network calls during inference.

---

## 🚀 How to Run

1. Download `MoodLens.apk` from this repo
2. Install on Android phone
3. Open app → Tap **▶ Start Camera**
4. Allow camera permission
5. See emotions detected in real-time! 😄

---

## 📦 Submission

Built for the **Melange On-Device AI Hackathon** by Zetic AI.

**Developer:** Bathini Rohini

---

*🔒 100% On-Device · No data leaves your phone · No internet required*
