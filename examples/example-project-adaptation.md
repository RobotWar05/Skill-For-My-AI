# Example: Project Adaptation — ESP32-S3 Smart Home Hub

This example demonstrates how to adapt the canonical skill repository for a specific project.

---

## Project Context

**Project:** Smart Home Hub with touchscreen display, multiple sensors, WiFi cloud sync, and BLE provisioning.
**Hardware:** ESP32-S3-WROOM-1 (240MHz, 512KB SRAM, 8MB Flash), 3.5" IPS touch display (JC3248W535), SHT30 temp/humidity sensor, BH1750 light sensor.
**Software:** PlatformIO + Arduino framework, LVGL for UI, MQTT for cloud sync.

---

## Step 1: Read AGENTS.md

Done. The 10 repo-wide rules are internalized.

---

## Step 2: Read Skill Catalog

Reviewed `skills/_catalog/README.md`. Relevant skills for this project:

| Skill | Relevant? | Why |
|---|---|---|
| `requirement-intake` | Yes | Initial feature decomposition needed |
| `structured-technical-response` | Yes | General technical discussions |
| `source-first-citation` | Yes | Will work with existing codebase |
| `architecture-first-solutioning` | Yes | Multi-component system design |
| `review-debug-deep-mode` | Yes | Debug hardware/software issues |
| `embedded-automation-design` | Yes | Core firmware development |
| `data-driven-tradeoff-analysis` | Yes | Technology choices (display lib, protocol) |
| `skill-scaffolder` | Maybe | If project-unique workflows emerge |

---

## Step 3: Identify Gaps

Tasks expected in this project:
1. ✅ Feature intake → `requirement-intake`
2. ✅ System architecture → `architecture-first-solutioning`
3. ✅ Firmware implementation → `embedded-automation-design`
4. ✅ Code review/debug → `review-debug-deep-mode`
5. ✅ Technology comparisons → `data-driven-tradeoff-analysis`
6. ⚠️ LVGL UI layout design → No exact match (UI-specific workflow)
7. ⚠️ OTA update procedure → No exact match (project-specific)

**Gaps identified:** UI layout design and OTA update flow.

---

## Step 4: Fill Gaps

### Gap 1: LVGL UI Layout Design

**Decision:** This is a recurring task that could be reusable across multiple embedded display projects. → Create a canonical skill.

Used `skill-scaffolder` to create `skills/ui-layout-design/SKILL.md` with:
- USE WHEN: designing touchscreen UI layouts for embedded displays.
- DO NOT USE WHEN: web UI design, backend API design.
- Workflow: identify screens → define navigation flow → design component hierarchy → specify constraints (resolution, touch targets) → mock layout → implement.

### Gap 2: OTA Update Procedure

**Decision:** This is specific to this project's dual-partition ESP32 OTA scheme. → Create project-specific skill in project overlay.

Created `project-skills/ota-update-flow/SKILL.md` in the project repo (not the canonical repo).

---

## Step 5: Create Project Overlay

Created `PROJECT_OVERLAY.md` in the project repo:

```markdown
# Project Overlay: Smart Home Hub

## 1. PROJECT IDENTITY
- Project Name: Smart Home Hub
- Platform: ESP32-S3-WROOM-1
- Toolchain: PlatformIO + Arduino framework
- RTOS: FreeRTOS (bundled with Arduino-ESP32)
- Language: C++

## 2. ACTIVE CANONICAL SKILLS
| Skill | Active | Adjustments |
|---|---|---|
| requirement-intake | Yes | Add: sensor list, display resolution, power source to intake |
| architecture-first-solutioning | Yes | Must include LVGL task, sensor task, MQTT task, BLE task |
| embedded-automation-design | Yes | Watchdog: 5s. Stack: 8192 per task. Max ISR: 5μs |
| review-debug-deep-mode | Yes | Add: LVGL memory leak check, touch calibration verification |

## 3. PROJECT CONSTRAINTS
### Hardware
- MCU: ESP32-S3 @ 240MHz, 512KB SRAM, 8MB Flash
- Display: JC3248W535 3.5" IPS 320x480, SPI interface
- Sensors: SHT30 (I2C 0x44), BH1750 (I2C 0x23)
- Pin Mapping: SDA=GPIO5, SCL=GPIO6, DISPLAY_CS=GPIO10, DISPLAY_DC=GPIO11

### Software
- LVGL buffer: 320*40*2 = 25.6KB double buffer
- MQTT broker: mosquitto on local RPi
- WiFi: WPA2-PSK, SSID from BLE provisioning

## 4. FILE MAP
| Content | Path |
|---|---|
| Source | src/ |
| Headers | include/ |
| LVGL config | include/lv_conf.h |
| PlatformIO config | platformio.ini |
| UI assets | assets/ |
```

---

## Step 6: Record Assumptions

- **ASSUMPTION:** BLE provisioning only needed once per device (not re-provisioning). Reasoning: typical consumer IoT pattern.
- **ASSUMPTION:** MQTT QoS 1 sufficient for sensor data. Reasoning: sensor data is periodic; missing one reading is acceptable.
- **ASSUMPTION:** Display refresh at 30 FPS for animations, 1 FPS for static. Reasoning: balance between visual quality and CPU/memory usage.

---

## Step 7: Begin Work

The agent now operates with:
- `AGENTS.md` → always-on rules.
- Selected canonical skills → task-specific workflows.
- `PROJECT_OVERLAY.md` → project context and constraints.

First task: run `requirement-intake` on the full feature list to decompose into implementation phases.
