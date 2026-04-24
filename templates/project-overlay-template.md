# Project Overlay Template

> **Instructions:** Copy this file to your project repository (not the canonical skill repo).
> Fill in all sections with project-specific details.
> This overlay tells the AI agent how to apply canonical skills to your specific project.

---

## 1. PROJECT IDENTITY

- **Project Name:** [Your project name]
- **Platform:** [e.g., ESP32-S3, STM32F4, Raspberry Pi, Web/Node.js]
- **Toolchain:** [e.g., ESP-IDF 5.x, PlatformIO + Arduino, GCC ARM, npm/webpack]
- **RTOS:** [e.g., FreeRTOS, Zephyr, bare-metal, N/A]
- **Language:** [e.g., C, C++, Python, TypeScript]
- **Repository Location:** [e.g., https://github.com/user/project]

---

## 2. ACTIVE CANONICAL SKILLS

List which canonical skills from the base repo apply to this project, and any project-specific adjustments:

| Skill | Active? | Project-Specific Adjustments |
|---|---|---|
| `requirement-intake` | Yes/No | [e.g., "Add sensor count and sampling rate to intake checklist"] |
| `structured-technical-response` | Yes/No | [e.g., "Section 2 must always address memory impact"] |
| `source-first-citation` | Yes/No | [e.g., "Source files in src/, headers in include/"] |
| `architecture-first-solutioning` | Yes/No | [e.g., "Must include RTOS task layout and stack sizing"] |
| `review-debug-deep-mode` | Yes/No | [e.g., "Add ISR safety and watchdog checks to Pass 3"] |
| `embedded-automation-design` | Yes/No | [e.g., "Watchdog period: 2s. Max ISR duration: 10μs"] |
| `data-driven-tradeoff-analysis` | Yes/No | [Adjustments if any] |

---

## 3. PROJECT CONSTRAINTS

### Hardware
- **MCU/SoC:** [e.g., ESP32-S3-WROOM-1, 240MHz dual-core, 512KB SRAM, 8MB Flash]
- **Peripherals used:** [e.g., SPI display, I2C sensors, UART debug, BLE, WiFi]
- **Pin Mapping:** [e.g., "SDA=GPIO5, SCL=GPIO6, DISPLAY_CS=GPIO10"]
- **Power Budget:** [e.g., "Battery powered, target < 50mA average"]

### Software
- **Stack Size:** [e.g., "4096 bytes per FreeRTOS task minimum"]
- **Watchdog Period:** [e.g., "2 seconds"]
- **Memory Budget:** [e.g., "Max 300KB heap usage, leave 200KB for WiFi stack"]
- **Update Mechanism:** [e.g., "OTA via HTTPS"]

### Timing
- **Sensor Sampling Rate:** [e.g., "100Hz accelerometer, 1Hz temperature"]
- **Display Refresh Rate:** [e.g., "30 FPS for animations, 1 FPS for static"]
- **Communication Latency:** [e.g., "MQTT publish within 500ms of event"]

---

## 4. PROJECT-SPECIFIC SKILLS

List any skills created specifically for this project (not in the canonical repo):

| Skill Name | Path | Purpose |
|---|---|---|
| [e.g., `ota-update-flow`] | [e.g., `project-skills/ota-update-flow/SKILL.md`] | [e.g., "OTA update procedure specific to this project's dual-partition scheme"] |

---

## 5. FILE MAP

| Content Type | Path |
|---|---|
| Source code | [e.g., `src/`] |
| Headers | [e.g., `include/`] |
| Tests | [e.g., `test/`] |
| Configuration | [e.g., `platformio.ini`, `sdkconfig`] |
| Documentation | [e.g., `docs/`] |
| Schematics | [e.g., `hardware/`] |
| CI/CD | [e.g., `.github/workflows/`] |

---

## 6. ASSUMPTIONS

[List all assumptions about this project. Each labeled `ASSUMPTION` with reasoning.]

- **ASSUMPTION:** [description]. Reasoning: [why you assumed this].
- **ASSUMPTION:** [description]. Reasoning: [why you assumed this].

---

## 7. PROJECT-SPECIFIC RULES

[Any rules that apply ONLY to this project, beyond the canonical AGENTS.md rules.]

- [e.g., "All log messages must use ESP_LOGx macros, not printf."]
- [e.g., "Every new module must have a corresponding unit test in test/."]
- [e.g., "Commit messages must reference Jira ticket numbers."]
