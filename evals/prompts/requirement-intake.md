# Eval Prompts: requirement-intake

---

## Prompt 1 — POSITIVE

**Prompt:**
> "I want to build an IoT weather station. It should read temperature, humidity, pressure, and air quality from sensors. Display data on a 3.5-inch TFT. Send data to a cloud dashboard every 5 minutes. Run on battery for at least 7 days. Use ESP32."

**Expected Behavior:** Agent activates `requirement-intake`. Produces intake summary with: request summary, explicit constraints (ESP32, 3.5" TFT, 7-day battery, 5-min cloud push), inferred constraints (battery → low power design, ESP32 → RAM/Flash limits), missing information (which sensors? which cloud? WiFi availability?), true technical objective.

**Pass Criteria:** All 6 output sections present. Constraints clearly labeled EXPLICIT vs INFERRED. At least 3 missing information items identified. No solution proposed.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "Design a protocol for communicating between 1 master ESP32 and 4 slave PIC16F controllers over RS485. Needs to handle sensor data polling, command dispatch, and firmware update. Must tolerate packet loss up to 5%."

**Expected Criteria:** Intake summary with protocol-specific constraints. Missing info should include: polling frequency, firmware update size, RS485 baud rate, max latency tolerance, packet format preferences.

**Pass Criteria:** True technical objective identifies this as a multi-drop half-duplex protocol design problem. No protocol implementation proposed during intake.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "I need a web dashboard for my factory. It should display real-time machine status from 20 PLCs, alert operators when a machine goes down, show historical trends, and support role-based access control. Must work on tablets."

**Expected Behavior:** Intake captures: 20 PLCs, real-time status, alerting, historical data, RBAC, tablet-responsive. Missing info: PLC communication protocol, data update frequency, alert delivery method, authentication system, historical data retention period.

**Pass Criteria:** Identifies both explicit constraints and inferred constraints (20 PLCs → scalability concern, real-time → WebSocket or similar).

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "What's the maximum clock speed of ESP32-S3?"

**Expected Behavior:** Agent does NOT activate `requirement-intake`. Answers directly: 240 MHz.

**Pass Criteria:** No intake summary generated. Direct factual answer provided.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Fix the null pointer dereference on line 87 of sensor_driver.c."

**Expected Behavior:** Agent does NOT activate `requirement-intake`. Proceeds to debug/fix or asks to see the code.

**Pass Criteria:** No intake summary generated. Agent treats this as a localized fix.

---

## Prompt 6 — NEGATIVE (Boundary)

**Prompt:**
> "Add a temperature reading feature to my existing weather station code. Here's the current main.cpp: [code]."

**Expected Behavior:** This is a small, well-defined addition to existing code. Agent should NOT activate full `requirement-intake`. May briefly clarify (which sensor?) but should proceed to implementation.

**Pass Criteria:** No full intake document. At most a brief clarifying question before implementation.

---

## Prompt 7 — POSITIVE (Boundary)

**Prompt:**
> "Add support for OTA updates, a touchscreen UI, and BLE provisioning to my existing ESP32 weather station firmware. Also needs to work with the new sensor board revision that uses different I2C addresses."

**Expected Behavior:** Multiple significant features = medium-to-large scope. Agent SHOULD activate `requirement-intake`.

**Pass Criteria:** Full intake summary generated. Identifies that this is 3+ separate concerns (OTA, UI, BLE, hardware change) requiring decomposition.
