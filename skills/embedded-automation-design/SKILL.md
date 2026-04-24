# SKILL: embedded-automation-design

---

## 1. NAME

`embedded-automation-design`

---

## 2. DESCRIPTION

Applies production-grade embedded and automation design principles when working on firmware, real-time systems, or hardware-interfacing code. Enforces non-blocking architecture, explicit state machines, timeout-protected operations, watchdog-safe design, clean layer separation (hardware → driver → transport → logic → application), short ISR handlers, and controlled resource allocation. Rejects blocking delays, infinite waits, heavy ISR processing, and uncontrolled dynamic allocation.

---

## 3. PURPOSE

Embedded systems that "work on the bench" often fail in production because they ignore real-world constraints: watchdog resets, interrupt latency, memory fragmentation, and timing-dependent failures. This skill exists to:

- Apply production-tested design patterns from day one.
- Prevent "works in demo, breaks in field" failures.
- Enforce patterns that are debuggable, testable, and maintainable.
- Keep firmware modular so that changing hardware doesn't require rewriting logic.

---

## 4. USE WHEN

- Task involves firmware development for any microcontroller (ESP32, STM32, PIC, AVR, etc.).
- Task involves RTOS task design, scheduling, or inter-task communication.
- Task involves interrupt handlers (ISR) or hardware interrupts.
- Task involves communication protocol implementation (UART, SPI, I2C, CAN, RS485, BLE, WiFi).
- Task involves hardware abstraction layer design.
- Task involves real-time control (PID, motor control, sensor fusion).
- Task involves power management, sleep modes, or low-power design.

---

## 5. DO NOT USE WHEN

- Task is pure software with no embedded/hardware/real-time constraints.
- Task is web development, data science, or desktop application development.
- Task is reviewing/debugging (use `review-debug-deep-mode` with embedded overlay).
- Task is architectural planning (use `architecture-first-solutioning` — but this skill should inform the architecture).

---

## 6. EXPECTED INPUTS

- Firmware design task, implementation request, or hardware interface requirement.
- Optionally: target MCU datasheet, schematic, existing codebase, RTOS choice.
- Optionally: timing requirements, memory budget, power budget.

---

## 7. EXPECTED OUTPUTS

Design or implementation that demonstrates:

1. **Non-blocking patterns** — no `delay()`, no blocking waits without timeout.
2. **State machine structure** — explicit states, transitions, and guards where applicable.
3. **Timeout protection** — all waits have defined timeouts with error handling.
4. **Layer separation** — clear boundaries between hardware, driver, transport, logic, app.
5. **ISR discipline** — ISRs set flags or enqueue data; processing happens in main loop/task.
6. **Resource management** — static allocation preferred; any dynamic allocation justified and bounded.
7. **Rationale** — each design pattern choice explained (why non-blocking here? why state machine there?).

---

## 8. WORKFLOW

1. **Identify the hardware context.** Target MCU, clock speed, available peripherals, memory.
2. **Identify real-time constraints.** What must happen within what time? What are the latency budgets?
3. **Design the layer structure:**
   - **HAL/Driver layer:** Direct hardware register access, peripheral init, low-level I/O.
   - **Transport layer:** Protocol handling (packet framing, CRC, retransmission).
   - **Logic layer:** Business logic, state machines, decision making.
   - **Application layer:** User-facing behavior, task orchestration.
4. **Design state machines** for any component with multiple modes of operation.
5. **Design interrupt handling:**
   - ISR: Set flag, enqueue data, or increment counter. Exit immediately.
   - Main loop / RTOS task: Process the flag/data.
6. **Add timeout protection** to every blocking-capable operation.
7. **Add watchdog integration** — ensure every long-running path feeds the watchdog.
8. **Design error handling** — what happens when a sensor fails? When communication drops? When power brownouts?
9. **Document memory allocation strategy** — static preferred, pooled if dynamic needed, never unbounded malloc.
10. **Verify testability** — can each module be unit tested without hardware?

---

## 9. CONSTRAINTS

- MUST NOT use `delay()` or any blocking wait in production code without explicit justification.
- MUST NOT perform heavy computation inside ISRs.
- MUST NOT use `while(1)` waits without timeout and exit conditions.
- MUST NOT use unbounded dynamic memory allocation (`malloc` without size limits or pool).
- MUST separate hardware access from business logic — at minimum 2 layers.
- MUST define explicit timeouts for all communication operations.
- MUST design for watchdog compatibility — no code path should block longer than the watchdog period.
- MUST document the rationale for each pattern choice.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT invent register names, peripheral addresses, or pin functions not from the datasheet.
- Do NOT claim an MCU has a peripheral (DMA, hardware CRC, etc.) without verification.
- Do NOT fabricate timing specifications (interrupt latency, ADC conversion time).
- Do NOT assume RTOS API signatures — check the specific RTOS version.
- Do NOT claim a driver library exists for a specific peripheral without verification.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Implement UART communication on ESP32 with packet framing and error recovery."
2. "Design the state machine for a motor controller with IDLE, RUNNING, FAULT states."
3. "Write an I2C sensor driver with timeout and retry logic."
4. "How should I structure the firmware for a device with BLE + WiFi + display?"
5. "Implement a non-blocking ADC sampling system with DMA."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "Build a REST API in Node.js." → Web development. Not embedded.
2. "Train a neural network on sensor data." → Data science. Not firmware.
3. "Review this ISR for bugs." → Use `review-debug-deep-mode`.
4. "Compare ESP32 vs STM32 for this project." → Use `data-driven-tradeoff-analysis`.

---

## 13. ADAPTATION NOTES

- **Per-project:** Add target MCU specs (RAM, Flash, clock), RTOS choice, watchdog period, ISR latency budget.
- **Per-board:** Add pin mapping, peripheral assignments, power rail specifications.
- **Per-protocol:** Add protocol-specific constraints (CAN bus load limits, BLE MTU size).
- These adaptations go in a **project overlay** (e.g., "This project uses ESP32-S3 @ 240MHz, FreeRTOS, 8KB stack per task, 2s watchdog timeout").

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `AGENTS.md` Section 7 — Embedded/Automation Defaults.
- No scripts or assets required for the canonical skill.
