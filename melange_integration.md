## Melange On-Device AI Integration

MoodLens uses the Melange FaceEmotionRecognition model for real-time facial emotion recognition directly on-device.

Model: HF/FaceEmotionRecognition
Platform: Melange
Inference: On-device (no cloud API)

Integration details: see melange_integration.md

## 🚀 1) Project Vision

**Q: Describe what your project is for?**  
This project aims to develop a mobile application that utilizes advanced machine learning capabilities to recognize and interpret human emotions through facial expressions. The app is designed for users who want to enhance their emotional awareness, improve interpersonal communication, and gain insights into their emotional states. It targets individuals interested in mental health, self-improvement, and emotional intelligence, providing them with a tool to better understand their feelings and reactions in various situations.

**Q: Describe what your app should do?**  
The application will leverage the `HF/FaceEmotionRecognition` model to analyze live video feeds from the device's camera, detecting and interpreting facial expressions in real-time. Users will be able to start a session where the app captures their facial expressions and provides immediate feedback on their emotional state, such as happiness, sadness, anger, or surprise. The app will also include a history feature that allows users to review past sessions, track emotional trends over time, and receive personalized insights based on their emotional data. Additionally, the app will feature a diagnostics screen to help users understand the model's performance and adjust settings as needed.

**Q: Describe how the interface works or looks?**  
The interface will feature a clean and modern design, utilizing a dark theme with vibrant accent colors that evoke a calming yet engaging atmosphere. The main screen will display a live camera feed with an overlay that highlights detected facial features and emotions. Users will have intuitive controls to start and stop the session, with visual and haptic feedback during the analysis. Navigation will be smooth, with a bottom tab bar for easy access to the history, settings, and diagnostics screens. The app will also incorporate animations to enhance user engagement and provide a polished experience.

**Q: Which language or platform should the app be generated for? (Choose one only.)**  
android-kotlin

---

## 🔑 2) Zetic Melange Configuration

- **Model ID**: HF/FaceEmotionRecognition
- **Personal Key**: dev_8b233396b5714f2797209d5223d2079b

> [!IMPORTANT]
> **These six fields above (project description, features, interface description, language, Model ID, Personal Key) are the *only* user-provided inputs you may rely on.**
> Everything else (screens, modality, pipelines, I/O specs, UI style, architecture, persistence needs) **must be inferred** from the project description + model ID + feature list.
> You may ask a question **only** if the Model ID, Personal Key, or **Language** is missing or unclear.

---

## 🎯 3) Role & Output Goal

You must:
1. **Analyze** the user's vision and feature requests.
2. **Infer** all necessary native capabilities from the Model ID + description (vision/audio/text/multimodal) and implement them end-to-end.
3. **Architect** a clean solution (UI + domain + data + inference + compatibility layer).
4. **Generate a full codebase only for the single language or platform the user selected in §1 (Language). Do not generate code for any other platform.**
   For the selected option, use this stack:
   - **Android (Kotlin)**: Kotlin + Jetpack Compose + Material 3
5. **Produce code** that is copy‑paste runnable with build files, permissions, and complete implementations of any helper/extension you use.

---

## 🧱 4) Absolute Rules (Non‑Negotiable)

### 4.1 No placeholders for core features
No `TODO`, `FIXME`, "omitted for brevity", or `...` in:
- Camera/microphone capture
- Frame/audio buffering
- Tensor preparation
- `model.run(...)` execution
- Post-processing + overlay rendering
- Navigation, state management, persistence
- Permissions + lifecycle handling
- Build configuration

### 4.2 No missing helpers/extensions
If you reference any helper/extension/utility class/function, you **MUST** include its full implementation in the output.

### 4.3 No unnecessary questions
Do not ask the user for clarifications on obvious requirements.
- If it smells like **vision** → implement camera.
- If it smells like **audio** → implement microphone.
- If it smells like **chat** → implement chat UX.

You may ask questions **ONLY** if:
- Model ID is missing, or
- Personal Key is missing, or
- Language (platform selection) is missing or ambiguous.

### 4.4 Security & privacy
- **Never log or print the Personal Key.**
- Provide user-facing privacy explanation in Settings.
- Default to **local-only storage** unless the user explicitly asked for cloud.

### 4.5 Performance & threading
- **Inference must never run on UI thread.**
- **Vision**: throttle FPS, reuse buffers, avoid per-frame allocations.
- **Audio**: use efficient buffering (ring buffer / frame windows), background inference.
- Show **telemetry**: latency ms, FPS (vision), and last error status.

### 4.6 Premium UI/UX requirement
The app must look polished (not "Hello World"):
- Coherent theme, spacing, typography
- Tasteful motion/animations
- Vibe matches the user's feature request (e.g., neon futuristic vs calm minimal)

---

## 🧠 5) Modality & Native Feature Inference Rules

### 5.1 Infer modality from Model ID keywords (primary signal)
- **Vision**: yolo, detect, detection, pose, keypoint, segmentation, depth, ocr, vision, image, cv, resnet, efficientnet
- **Audio**: whisper, asr, stt, speech, keyword, audio, vad, tts, sound
- **Sensor/Tabular**: tabular, fraud, sensor, time-series

> **NOTE**: If the user asks for an LLM (Text Generation), **STOP** and inform them to use the "Zetic LLM Prompt" instead, as the SDK classes differ (`ZeticMLangeLLMModel`). This prompt is for Vision/Audio/General ML only.

### 5.2 Infer modality from the project description/features (secondary signal)
- Mentions camera/live view/overlay → **Vision**
- Mentions voice/speech/mic/recording → **Audio**
- Mentions chat/writing/summarize/translate → **Text**
- Mentions combined workflows → **Multimodal**

### 5.3 Must implement implied native pipelines automatically
- **Vision** → CameraX / AVFoundation, preview UI, frame extraction, preprocessing, overlay rendering
- **Audio** → Microphone permissions, capture pipeline, buffering to frames, preprocessing
- **Text** → Premium compose UI (chat/compose), state management, settings controls
- **Multimodal** → Combined pipelines with a clear UX and concurrency safety

> **You MUST state the inferred modality and why in the final output's "Inference Summary".**

---

## 🔌 6) Zetic Melange Integration Requirements (Mandatory)

You **MUST** integrate using the official SDK patterns below. Replace `PERSONAL_KEY` and `MODEL_ID` (or `MODEL_NAME` in Java) with the exact strings from §2. Use **`modelMode`** `RUN_AUTO` (hardcoded for now).

### 6.1 Android (Kotlin)
**Gradle**
Add:
```kotlin
implementation("com.zeticai.mlange:mlange:+")
```
Add:
```kotlin
android {
    packaging {
        jniLibs {
            useLegacyPackaging = true
        }
    }
}
```

**Model load + run** (in Activity):
```kotlin
// modelMode: RUN_AUTO. onProgress: optional (0.0 to 1.0)
val model = ZeticMLangeModel(context, PERSONAL_KEY, MODEL_ID, modelMode = ModelMode.RUN_AUTO, onProgress = { progress -> /* 0.0 to 1.0 */ })

val inputs: Array<Tensor> = // Prepare your inputs
val outputs = model.run(inputs)
```

### 6.2 Android (Java)
Same Gradle dependency and packaging block as Kotlin (see 6.1).

**Model load + run** (in Activity):
```java
// modelMode: RUN_AUTO. Progress callback: 0.0f to 1.0f
String personalKey = "PERSONAL_KEY";
String modelName = "MODEL_ID";
ZeticMLangeModel model = new ZeticMLangeModel(context, personalKey, modelName, ModelMode.RUN_AUTO, progress -> { /* 0.0f to 1.0f */ });

Tensor[] inputs = // Prepare your inputs
Tensor[] outputs = model.run(inputs);
```

### 6.3 iOS (Swift)
**Swift Package**
Add package dependency:
`https://github.com/zetic-ai/ZeticMLangeiOS.git`

**Model load + run:**
```swift
// modelMode: .RUN_AUTO. onDownload: optional (0.0 to 1.0)
let model = try ZeticMLangeModel(personalKey: PERSONAL_KEY, name: MODEL_ID, modelMode: ModelMode.RUN_AUTO, onDownload: { progress in /* 0.0 to 1.0 */ })

let inputs: [Tensor] = [] // Prepare your inputs
let outputs = try model.run(inputs)
```

### 6.4 Critical replacement rule
In the generated code, you **MUST**:
- Replace `PERSONAL_KEY` with the exact **Personal Key** string from the top section.
- Replace `MODEL_ID` (or `MODEL_NAME` in Java) with the exact **Model ID** string from the top section.
- **Do not leave placeholders.**

### 6.5 Model download/load screen and progress callbacks (Mandatory)
You **MUST** use the SDK’s progress callbacks so the app shows a **dedicated load/download screen** (or equivalent UI state). If you do not, the generated app may never show a loading screen and can **hang on the main screen** (camera, chat, or other UI) while the model downloads or loads in the background.

- **Android**: Use the **`onProgress`** option when creating or using **`ZeticMLangeModel`**. Show download/load progress in the UI (e.g. progress bar or percentage). Only navigate to the main feature screen (camera, inference, etc.) once the model is ready.
- **iOS**: Use the **`onDownload`** option when creating or using **`ZeticMLangeModel`**. Show download/load progress in the UI. Only present the main feature screen once the model is ready.

Implement a clear loading state (e.g. “Downloading model…”, “Loading model…”) and transition to the main flow only after the model is loaded. See the sample apps repository above for reference implementations.

---

## 🧪 7) SDK Surface Discovery Rule (Prevents Fake APIs)

> [!WARNING]
> **You are not allowed to invent SDK APIs for Tensor creation.**

Before writing final code, you **MUST** inspect the installed SDK symbols to discover how to create Tensor inputs correctly:
- **Android (Kotlin)**: use IDE symbol search / Gradle sources / jar browsing to locate Tensor constructors/factories and required dtypes/shapes.
- **Android (Java)**: same SDK; locate Tensor constructors/factories and required dtypes/shapes in the Java API.
- **iOS**: use Xcode symbol search / Swift package source browsing to locate Tensor initializers/factories.

Then implement a single, centralized adapter per platform:
- `ZeticTensorFactory` (Android Kotlin)
- `ZeticTensorFactory` (Android Java)
- `ZeticTensorFactory` (iOS)

All preprocessing code must feed into these factories so input-shape fixes are localized.
*You may not ask the user for extra details here. You must discover the APIs yourself via source/symbol inspection.*

---

## 🧩 8) Model Compatibility Layer (Mandatory)

Because model input/output specs are often unknown, you **MUST** implement a **Model Compatibility Layer** that makes the app robust.

### 8.1 Persisted ModelInputSpec
Persist a spec that can be adjusted in-app:
- **Vision**: input width/height, color space (RGB/BGR), normalization (0..1 / -1..1 / ImageNet / 0..255), **rotation degrees (0/90/180/270)**, lens (front/back)
- **Audio**: sample rate, channels, frame length (ms), format (int16/float32)
- **Text**: max tokens, optional prompt template

**Persistence:**
- **Android**: DataStore
- **iOS**: UserDefaults (or a lightweight wrapper)

### 8.2 Diagnostics Screen (Required)
Implement a Diagnostics screen that shows:
- Inferred modality + short reasoning
- Current `ModelInputSpec` (editable controls)
- Last inference latency (ms), fps (vision), last error (human-friendly)
- Raw output viewer (first N values + shapes if available), "copy" button

### 8.3 Safe defaults
If the model spec is unknown, default to:
- **Vision**: 224×224, RGB, float32, normalization 0..1, 15 FPS, front lens if it's a self/fitness app vibe; otherwise back.
- **Audio**: mono, 16 kHz, 20 ms frames, float32
- **Text**: reasonable token limit (e.g., 256–512)

*The app must still run and the user can tweak these defaults.*

---

## 📱 9) Required App Features (End‑to‑End)

Regardless of the specific app idea, implement these screens and flows:

### 9.1 Live screen (core)
- Real-time inference
- Start/Stop session controls
- Live feedback (text + haptics; add voice if it fits the requested features)
- **Telemetry**: inference latency, FPS (vision), error status
- **Vision**: overlay visualization above the camera preview
- **Audio**: live mic indicator + result UI (transcription/keyword/level/intent)
- **Text**: premium compose UI for prompts/responses

### 9.2 History screen
- Persist session summaries locally
- **Charts**: Android: Compose Canvas chart (or configured chart dependency); iOS: Swift Charts if available; otherwise custom SwiftUI chart

### 9.3 Settings screen
- Theme controls: light/dark + accent derived from "vibe" inference
- Performance controls: FPS/resolution presets; battery saver
- Privacy controls: data retention, permissions status, clear history

### 9.4 Diagnostics screen
- As defined in Section 8.

---

## 🛠️ 10) Platform-Specific Implementation Requirements

### 10.1 Android (Kotlin + Compose + Material 3)
**Must use:**
- Jetpack Compose (Material 3)
- CameraX for vision (`PreviewView` inside Compose via `AndroidView`)
- Coroutines + ViewModel + StateFlow
- DataStore for settings persistence

**Vision pipeline must include:** CameraX `ImageAnalysis` frame acquisition (`ImageProxy`), YUV → RGB conversion, resize to `ModelInputSpec`, normalization per spec, Tensor creation via `ZeticTensorFactory`, `model.run(inputs)` off UI thread, postprocess + overlay (pose/detection/segmentation/unknown).

**Audio pipeline (if inferred):** Microphone capture + permissions, buffering to frames, `ZeticTensorFactory`, inference + UI feedback.

### 10.2 Android (Java)
Same Gradle dependency and packaging as Kotlin. Use `ZeticMLangeModel(Context, PERSONAL_KEY, MODEL_NAME)` and `model.run(inputs)` as in §6.2.

**Must use:** CameraX (or Camera2) for vision; run inference off the UI thread (e.g., ExecutorService or background thread). DataStore or SharedPreferences for settings. Vision pipeline: frame acquisition → resize/normalize per ModelInputSpec → Tensor via `ZeticTensorFactory` (Java) → `model.run(inputs)` off UI thread → postprocess + overlay. Audio pipeline (if inferred): microphone capture, buffering, `ZeticTensorFactory`, inference off UI thread. Implement `ZeticTensorFactory` (Java) for `Tensor[]` creation; do not invent APIs—discover from SDK.

### 10.3 iOS (Swift + SwiftUI + AVFoundation)
**Must use:** SwiftUI navigation + screens; AVFoundation (vision: `AVCaptureSession` + `AVCaptureVideoDataOutput`; audio: `AVAudioEngine` or equivalent); Swift concurrency for inference; UserDefaults for settings.

**Vision pipeline must include:** Capture frames (`CMSampleBuffer` → `CVPixelBuffer`), resize + normalize per `ModelInputSpec`, Tensor creation via `ZeticTensorFactory`, `try model.run(inputs)` off main thread, overlay drawing with SwiftUI Canvas or `CALayer`. **Must provide a full Xcode project structure (`App.swift`, `ContentView.swift`, correct folder hierarchy).**

---

## 📦 11) Output Format Contract (Strict — Follow Exactly)

You **MUST** output in this exact structure, **but only include the section that matches the user's selected language from §1. Omit the other platform entirely.**

### A) Inference Summary & Assumptions
- Inferred modality and why (bullets)
- Inferred vibe theme (palette/typography/motion notes)
- Default `ModelInputSpec` values and how to change them in Diagnostics
- Chosen output interpretation (pose/detection/segmentation/unknown) and visualization approach
- **Selected language for this output (echo the user's choice)**

### B) ANDROID (only if user selected Android (Kotlin) or Android (Java))
Include B only when the user selected that Android option. Otherwise omit B entirely.
- File tree (paths)
- Full contents of every file, each preceded by a path header, e.g.:
```
--- path: android/app/build.gradle.kts ---
// full file content here
```
If Kotlin: `--- path: android/app/src/.../MainActivity.kt ---`  
If Java: `--- path: android/app/src/.../MainActivity.java ---`  
**Must include at minimum:** `settings.gradle(.kts)`, `app/build.gradle.kts` or `build.gradle` (with Zetic dependency + packaging block), `AndroidManifest.xml`, all Kotlin or Java source files (UI, ViewModels/Activities, inference, tensor factory, overlay), resources (themes, colors, strings, etc.)

### C) iOS (only if user selected iOS)
Include C only when the user selected iOS. Omit entirely otherwise.
- File tree (paths)
- Full contents of every file, each preceded by a path header, e.g.:
```
--- path: ios/App/App.swift ---
// full file content here
```
**Must include at minimum:** Swift Package dependency steps, `Info.plist` keys to add, all Swift source files (UI, inference pipeline, tensor factory, overlay, settings)

### D) Build & Run Instructions
Include **only** the steps for the selected platform: Android Studio for Android, Xcode for iOS.
- Permissions checklist (for the selected platform)
- Troubleshooting: camera black screen, denied permissions, low FPS / battery drain, model input mismatch (tell user to adjust `ModelInputSpec` in Diagnostics)

> **If the output is too long for one message: continue in additional messages until complete. Do not truncate. Maintain the file-by-file structure.**

---

## ✅ 12) Quality Gates (Self‑Check Before Final Answer)

**Before finalizing, verify:**
- [ ] No `TODO`/`FIXME`/placeholders in core flows
- [ ] No `...` in code blocks
- [ ] Every referenced helper/extension exists and is implemented
- [ ] Permissions included and handled gracefully
- [ ] Inference runs off the UI thread
- [ ] Live preview + overlay works (for vision)
- [ ] Diagnostics screen exists and edits `ModelInputSpec`
- [ ] UI looks premium and matches the inferred vibe
- [ ] Personal Key is **never** logged

---

## 🟢 NOW GENERATE THE COMPLETE APP

**Generate the complete application for the single language or platform the user selected in §1 (Language) only. Do not generate code for any other platform. Strictly follow the Output Format Contract.**  
**Do not ask follow-up questions unless the Model ID, Personal Key, or Language is missing or unclear.**
