# Eval Prompts: architecture-first-solutioning

---

## Prompt 1 — POSITIVE

**Prompt:**
> "Design the software architecture for a smart home hub that connects to Zigbee sensors, provides a local touchscreen UI, and syncs data to a cloud backend via MQTT. Target platform is ESP32-S3."

**Expected Behavior:** Agent produces a full architecture analysis BEFORE any code: system overview, data flow (sensors → Zigbee → ESP32 → MQTT → cloud, and ESP32 → display), control flow, state management, timing (sensor polling vs display refresh vs MQTT publish), constraints (ESP32-S3 resources), layer diagram, risks, recommended architecture.

**Pass Criteria:** All 9 output sections present. No implementation code produced before architecture is reviewed. Risks section identifies at least 2 concerns.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "How should I structure the firmware for a device that has BLE provisioning, WiFi data upload, a local display, and an SD card logger? They all need to run concurrently on ESP32."

**Expected Behavior:** Architecture analysis focusing on RTOS task design, shared resource management, state machines for BLE and WiFi, and layer separation.

**Pass Criteria:** Addresses concurrency (task priorities, shared resources), timing (BLE advertising vs WiFi connected), and state management (provisioning flow states).

---

## Prompt 3 — POSITIVE

**Prompt:**
> "I need to refactor this monolithic 2000-line main.cpp into proper modules. What architecture should I use?"

**Expected Behavior:** Architecture analysis for modularization: identify current responsibilities in the monolith, propose module boundaries, define interfaces, plan the refactoring.

**Pass Criteria:** Proposes specific module boundaries with rationale. Identifies dependencies between proposed modules. Does not just say "split it up."

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "Fix the null pointer on line 42 of mqtt_handler.c."

**Expected Behavior:** Localized bug fix. No architecture analysis needed. Use `review-debug-deep-mode`.

**Pass Criteria:** No architecture document produced. Proceeds to debug.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Implement the PID controller using this transfer function: Kp=2.0, Ki=0.5, Kd=0.1."

**Expected Behavior:** Design is already specified. Implementation task. Proceed directly.

**Pass Criteria:** No architecture analysis. Implements the PID as specified.

---

## Prompt 6 — NEGATIVE (Boundary)

**Prompt:**
> "Add an LED blink function to my existing project."

**Expected Behavior:** Trivially small task. No architecture needed.

**Pass Criteria:** Direct implementation without architecture analysis.

---

## Prompt 7 — POSITIVE (Boundary)

**Prompt:**
> "Add MQTT support to my existing BLE-only sensor device. This means adding WiFi, connection management, data serialization, and a publish queue."

**Expected Behavior:** Multiple new subsystems = architectural impact. Should trigger architecture analysis: how WiFi coexists with BLE, task priorities, memory impact, state management for connection lifecycle.

**Pass Criteria:** Architecture analysis covers WiFi+BLE coexistence, connection state machines, queue design, and memory impact assessment.
