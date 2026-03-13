# 🔎 MoodLens — On-Device AI Emotion Detector

![AI](https://img.shields.io/badge/AI-On--Device-blue)
![Platform](https://img.shields.io/badge/Platform-Web-green)
![Privacy](https://img.shields.io/badge/Privacy-100%25_On_Device-brightgreen)

MoodLens is a privacy-first facial emotion detection application that runs AI **directly on the device**.  
It analyzes facial expressions from the camera and detects emotions in real time without sending any data to the cloud.

This project was built for the **Melange On-Device AI Hackathon**.

---

# 🎯 Problem

Most emotion detection systems rely on **cloud-based AI APIs**.

This creates several issues:

❌ Privacy risk — face data is sent to remote servers  
❌ Requires internet connection  
❌ Slow due to network latency  
❌ Expensive API usage  

Users should be able to analyze emotions **without uploading their face data anywhere**.

---

# ✅ Solution — MoodLens

MoodLens performs **real-time emotion detection directly on-device**.

The app uses the device camera to analyze facial expressions and classify emotions locally.

No images or video leave the device.

---

# 🧠 AI Model

MoodLens integrates the **FaceEmotionRecognition** model deployed through the Melange platform.

Model used:

HF / FaceEmotionRecognition

The model detects six emotions:

• Happy  
• Sad  
• Angry  
• Surprised  
• Fearful  
• Neutral  

Inference is designed to run locally using **Melange On-Device AI**.

---

# ⚡ Features

| Feature | Description |
|------|-------------|
| 6 Emotion Detection | Happy, Sad, Angry, Surprised, Fearful, Neutral |
| Real-Time Analysis | Updates approximately every 0.5 seconds |
| On-Device AI | No cloud processing |
| Privacy First | Face data never leaves the device |
| Lightweight | Runs directly in the browser |

---

# 📱 Demo

Live Demo:

https://rohi-nagedram.github.io/moodlens/

Open the link on a mobile device and allow camera access to test the emotion detection.

---

# 🔧 How It Works

1. The device camera captures live frames.
2. The face region is detected.
3. The emotion recognition model analyzes facial expressions.
4. The predicted emotion is displayed in real time.

All processing is designed to run **locally on the device**.

---

# 🧩 Melange Integration

This project integrates **Melange On-Device AI** for deploying the emotion recognition model.

Platform: Melange  
Model: HF / FaceEmotionRecognition  

The deployment configuration and integration prompt used for Melange are included in:

melange_integration.md

---

# 🔒 Privacy

MoodLens was built with **privacy as the main priority**.

• No images are stored  
• No data is sent to servers  
• All AI inference runs locally  

This ensures users maintain full control of their facial data.

---

# 🏁 Hackathon Submission

Project Name: MoodLens  
Category: On-Device AI  
Platform: Melange  

Built for the **Melange On-Device AI Hackathon**.

---

# 📜 License

MIT License
