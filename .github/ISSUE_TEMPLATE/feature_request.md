---
name: "Feature Request"
about: "Suggest an idea, new MCP tool, hardware acceleration backend, or model architecture"
title: "[FEATURE] <Brief summary of proposed feature>"
labels: ["enhancement"]
assignees: ""
---

### 1. Target Repository / Area
- [ ] `android-inference-engine` (New hardware backend, quantized formats, kernel optimizations)
- [ ] `android-mcp-tools` (New system tool, IPC transport, protocol extension)
- [ ] `android-agent-workflow` (Planning strategy, context distillation, memory/persistence)
- [ ] Architecture / Ecosystem Documentation

### 2. Feature Category
- [ ] New Hardware Acceleration Backend (e.g., NPU delegate, OpenCL tuning, specialized DSP)
- [ ] New Model Architecture Support (e.g., vision-language models, whisper audio, embedding models)
- [ ] New On-Device MCP Tool (e.g., SQLite query tool, Bluetooth LE sensor, Location provider)
- [ ] Workflow & Reasoning Enhancement (e.g., Tree-of-Thought, dynamic tool pruning, speculative execution)
- [ ] IPC / Security Enhancement (e.g., biometric prompt integration, custom IPC transport)

### 3. Problem Statement & Motivation
Is your feature request related to a specific limitation or use case? Please describe the problem clearly (e.g., *"Current inference on Exynos chips defaults to CPU because Mali GPU OpenCL kernels are not tuned"* or *"We need an on-device contact lookup tool for local agent workflows"*).

### 4. Proposed Solution & Architecture
Describe the solution you'd like to see implemented:
* Proposed API signature or contract changes
* Interaction with existing modules (Inference Engine, MCP Tools, or Agent Workflow)
* Fallback strategies if the required hardware/feature is not available on older Android versions

### 5. On-Device Constraints & Performance Considerations
* **Memory Footprint**: Estimated RAM required
* **Battery / Thermal Impact**: Expected energy consumption or power trade-offs
* **Latency Expectation**: Target token generation speed (TPS) or tool execution latency (ms)
* **Minimum Android API**: (e.g., API 26+, API 31+, API 34+)

### 6. Alternatives Considered
Describe any alternative solutions, third-party libraries, or workarounds you have considered.

### 7. Additional Context / References
Add any references, academic papers, pull requests, or links to related upstream projects (e.g., llama.cpp, LiteRT, Model Context Protocol specs).
