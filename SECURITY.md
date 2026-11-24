# Security Policy: local-ai-mobile Ecosystem

Security and privacy are core architectural foundations of the `local-ai-mobile` open-source ecosystem. Because our libraries execute machine learning models and tool operations locally on physical Android devices without relaying user prompts, sensor feeds, or private telemetry to cloud servers, protecting local application boundaries, IPC endpoints, and hardware resources is paramount.

---

## 1. Supported Versions

We actively maintain and provide security updates for the latest stable releases of each repository in the ecosystem:

| Repository | Supported Major/Minor Releases | Minimum Android API | Security Status |
| :--- | :--- | :--- | :--- |
| **`android-inference-engine`** | `1.0.x` | API 26 (Android 8.0) | Active Security Support |
| **`android-mcp-tools`** | `1.0.x` | API 26 (Android 8.0) | Active Security Support |
| **`android-agent-workflow`** | `1.0.x` | API 26 (Android 8.0) | Active Security Support |
| **`.github` (Org Profile & Community)** | Latest (`main`) | N/A | Active Security Support |

Earlier experimental snapshots or unofficial forks are not covered by official security advisories.

---

## 2. Threat Model for On-Device AI & MCP Tools

Operating autonomous agentic loops and Model Context Protocol (MCP) servers directly on client Android hardware introduces a unique threat model compared to traditional server-side AI architectures.

### 2.1 Adversarial Prompt Injection & Tool Hijacking
- **Risk**: Malicious input text (or unverified web/file content ingested via MCP tools) can attempt to manipulate model instructions to trigger unauthorized tool actions (e.g., accessing private notes, calendar events, or reading device files).
- **Mitigations**:
  - **4-Tier Approval Gating**: `ALWAYS_ASK`, `SENSITIVE_ONLY`, `AUTO_DECIDE`, and `NEVER_ASK`. High-risk operations (file writes, IPC calls, calendar changes) default to explicit user confirmation.
  - **Scratchpad Isolation**: Intermediate tool outputs and reasoning steps are strictly isolated in a sandboxed scratchpad to prevent prompt pollution and token poisoning of conversational history.
  - **Context Distillation**: Tool outputs are sanitized and compacted (capped at ~350 characters) before feeding back into reasoning prompts, limiting injection payload surface.

### 2.2 Local IPC & Service Access Control
- **Risk**: Malicious third-party apps installed on the same device might attempt to bind to local MCP services via AIDL, send arbitrary intents to BroadcastReceivers, or query ContentProviders.
- **Mitigations**:
  - **Calling Package Verification**: Services verify the UID and signature of caller packages via `PackageManager.getPackagesForUid(Binder.getCallingUid())`.
  - **Signature & Permission Guards**: Sensitive endpoints require signature-level custom permissions or explicit runtime authorization.
  - **Localhost Loopback Isolation**: Internal HTTP/SSE transports bind strictly to `127.0.0.1:8765` and do not expose ports to external network interfaces.

### 2.3 Sandboxing & Path Traversal Guards
- **Risk**: File inspector and storage tools could be exploited to read or write sensitive files outside application boundaries (such as private databases or shared credentials).
- **Mitigations**:
  - **Canonical Path Traversal Checks**: All file paths are resolved with `file.canonicalPath` and strictly verified against whitelisted app-private storage roots (`context.filesDir`, `context.cacheDir`). Paths containing directory traversal tokens (`../`) or pointing outside allowed roots are immediately rejected with security exceptions.

### 2.4 Resource Exhaustion, DoS & Thermal Safety
- **Risk**: Heavy continuous local LLM inference can cause device overheating, battery drain, or triggering Android's low-memory killer (LMK).
- **Mitigations**:
  - **DeviceThermalMonitor**: Dynamically monitors thermal status via Android `ThermalStatusListener` and throttles inference or drops execution priority when device temperature reaches `THERMAL_STATUS_SEVERE`.
  - **DevicePowerMonitor**: Blocks autonomous background agent execution via WorkManager if device battery is below 15% or Battery Saver mode is active.
  - **MemoryLimiterKillGuard**: Verifies available memory against model context size prior to allocation to prevent Out-Of-Memory (OOM) app crashes.

---

## 3. Reporting a Vulnerability

We welcome and appreciate responsible vulnerability disclosures from the security community and independent researchers.

### 3.1 Reporting Channel
- **Private Advisory**: Please submit security reports privately through GitHub's Security Advisories feature:
  - Navigate to the affected repository's **Security** tab -> **Advisories** -> **Report a vulnerability**.
- **Direct Contact**: If GitHub Private Advisory is unavailable, please send an encrypted or direct email to:
  - **Email**: `security@local-ai-mobile.dev`
  - **PGP Key ID**: `0x7B9E2A10C35F924D`
  - **Subject Line**: `[SECURITY VULNERABILITY] <Component Name>: <Brief Description>`

### 3.2 Information to Include in Your Report
To help us triage and resolve the issue quickly, please provide:
1. The affected repository and specific version/commit hash.
2. Type of vulnerability (e.g., prompt injection bypass, IPC privilege escalation, directory traversal, DoS/memory leak).
3. Detailed step-by-step reproduction instructions or a minimal Proof of Concept (PoC).
4. Device specifications used for reproduction (Android OS version, manufacturer, SoC/chipset, NPU model).
5. Potential impact on end users or host applications.

---

## 4. Vulnerability Response Timeline

Our maintainers follow a strict responsible disclosure workflow:

| Stage | Timeline | Description |
| :--- | :--- | :--- |
| **Initial Acknowledgment** | Within **48 hours** | We acknowledge receipt of your report and assign a tracking lead. |
| **Triage & Reproduction** | Within **5 business days** | We validate the reported behavior, determine severity, and reproduce the PoC. |
| **Patch & Fix Development**| Within **14 business days** | Maintainers draft, review, and test a targeted security patch. |
| **Pre-Release Validation** | Within **5 business days** | The reporter is invited to review and verify the fix in a private branch. |
| **Coordinated Disclosure** | Within **30-90 days** | Public release of patched version and published GitHub Security Advisory (CVE assignment). |

---

## 5. Responsible Disclosure Guidelines

We kindly ask reporters to adhere to standard responsible disclosure practices:
- Do not publicly disclose or discuss the vulnerability until a patch has been released and a coordinated disclosure date agreed upon.
- Avoid accessing, modifying, or destroying data belonging to other users or devices during testing.
- Conduct testing only on your own local test devices or emulators.

Thank you for helping keep the on-device AI ecosystem secure, robust, and privacy-preserving!
