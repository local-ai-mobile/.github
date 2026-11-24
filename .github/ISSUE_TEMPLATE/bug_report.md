---
name: "Bug Report"
about: "Report a bug or unexpected behavior in the on-device AI ecosystem"
title: "[BUG] <Brief summary of the issue>"
labels: ["bug", "triage"]
assignees: ""
---

<!-- 
Before submitting, please ensure you have searched existing issues to avoid duplicates.
For security vulnerabilities, please do NOT use this form; refer to SECURITY.md instead.
-->

### 1. Affected Repository / Component
- [ ] `android-inference-engine` (llama.cpp GGUF / LiteRT / Gemini Nano / Hardware Profiler)
- [ ] `android-mcp-tools` (Model Context Protocol / System Tools / Multi-IPC / Security)
- [ ] `android-agent-workflow` (Plan-Execute-Observe-Verify / Context Distillation / WorkManager)
- [ ] `.github` (Organization Profile / CI / Documentation)

### 2. Device & Hardware Environment
* **Device Manufacturer & Model**: (e.g., Google Pixel 8 Pro, Samsung Galaxy S24, Xiaomi 14)
* **Android OS Version**: (e.g., Android 14 / API 34, Android 15 / API 35)
* **Chipset / SoC**: (e.g., Qualcomm Snapdragon 8 Gen 3, MediaTek Dimensity 9300, Google Tensor G3)
* **Acceleration Backend Used**: (e.g., Qualcomm Hexagon HTP NPU, Vulkan GPU, OpenCL, CPU NEON, LiteRT Delegate)
* **RAM / Available Memory**: (e.g., 12 GB LPDDR5X, 4.2 GB free)

### 3. Library & Dependency Versions
* **Library Version**: (e.g., `1.0.0`)
* **Kotlin Version**: (e.g., `2.2.0`)
* **Android Gradle Plugin (AGP)**: (e.g., `8.8.0` / `9.1.1`)
* **Model Format & Size**: (e.g., `GGUF Q4_K_M 1.8GB`, `TFLite / LiteRT INT8 1.2GB`)

### 4. Description of Bug
A clear and concise description of what the bug is.

### 5. Steps to Reproduce
1. Initialize the component with options: `...`
2. Load model / register tool / trigger workflow: `...`
3. Execute: `...`
4. Observe the failure or crash.

### 6. Expected Behavior
A clear and concise description of what you expected to happen.

### 7. Actual Behavior
A clear and concise description of what actually happened (e.g., crash, corrupted tokens, silent timeout, IPC failure).

### 8. Logcat Output & Stack Trace
```text
// Paste relevant logcat or stack trace output here
```

### 9. Additional Context
Add any other context about the problem here (e.g., thermal status, battery level, background vs foreground execution).
