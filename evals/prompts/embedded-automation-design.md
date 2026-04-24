# Eval Prompts: embedded-automation-design

---

## Prompt 1 — POSITIVE

**Prompt:**
> "Implement UART communication on ESP32 with packet framing (STX/ETX), CRC-16 checksum, and retry on timeout. Must be non-blocking."

**Expected Behavior:** Agent applies embedded design principles: non-blocking receive with ring buffer, state machine for packet parsing (WAIT_STX → HEADER → PAYLOAD → CRC → WAIT_ETX), timeout on incomplete packets, retry mechanism with backoff. No `delay()` or blocking waits.

**Pass Criteria:** State machine clearly defined. No blocking calls. Timeout specified with value. Layer separation (transport vs protocol logic). CRC verified before processing.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "Design the state machine for a motor controller with states: IDLE, STARTING, RUNNING, FAULT, STOPPING. The motor has an overcurrent sensor and an emergency stop button."

**Expected Behavior:** Full state machine with: all 5 states, transition conditions, guards (overcurrent threshold), actions on entry/exit, emergency stop handling (any state → FAULT or STOPPING), watchdog feeding in each state, timeout in STARTING state.

**Pass Criteria:** State machine diagram or table. Emergency stop reachable from all states. Timeout in STARTING prevents stuck start. FAULT state has defined recovery path or requires manual reset.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "Write an I2C sensor driver for the SHT30 humidity sensor. It should retry on NACK and timeout after 100ms."

**Expected Behavior:** Driver with: non-blocking I2C read, timeout mechanism, retry with count limit, error reporting, separation of driver layer from application layer. No infinite retry loops.

**Pass Criteria:** Timeout value defined (100ms). Retry count limited. Error returned to caller on failure. No `while(1)` without exit.

---

## Prompt 4 — POSITIVE

**Prompt:**
> "How should I structure FreeRTOS tasks for a device with BLE, WiFi, display, and sensor sampling?"

**Expected Behavior:** Task architecture with: task priorities justified, stack sizes estimated, inter-task communication (queues/events), shared resource protection (mutexes), watchdog feeding strategy.

**Pass Criteria:** Each task has defined priority with rationale. Shared resources identified. Communication mechanism chosen with reasoning.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Build a REST API in Python Flask for sensor data."

**Expected Behavior:** Web development task. Not embedded. Answer directly or use `structured-technical-response`.

**Pass Criteria:** No embedded design principles applied. No state machine, no ISR discussion.

---

## Prompt 6 — NEGATIVE

**Prompt:**
> "Compare FreeRTOS vs Zephyr for this project."

**Expected Behavior:** Comparison task. Use `data-driven-tradeoff-analysis`.

**Pass Criteria:** Structured comparison format, not embedded design format.

---

## Prompt 7 — POSITIVE (Boundary)

**Prompt:**
> "Add a simple LED blink to my ESP32 project using a timer."

**Expected Behavior:** Even for simple tasks, embedded principles apply: use hardware timer or software timer callback (not `delay()`), non-blocking pattern, clean GPIO abstraction.

**Pass Criteria:** Uses timer-based approach, not `delay()`. Even for a simple task, demonstrates non-blocking discipline.
