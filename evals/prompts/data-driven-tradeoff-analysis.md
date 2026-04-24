# Eval Prompts: data-driven-tradeoff-analysis

---

## Prompt 1 — POSITIVE

**Prompt:**
> "Should I use MQTT or CoAP for communication between my ESP32 sensor nodes and a Raspberry Pi gateway? The sensors send 100-byte payloads every 10 seconds over WiFi. Battery life matters."

**Expected Behavior:** Agent activates `data-driven-tradeoff-analysis`. Produces comparison matrix with criteria: bandwidth, overhead, power consumption, reliability, complexity. Evaluates MQTT and CoAP against each criterion with evidence.

**Pass Criteria:** Comparison matrix present. Both options have advantages AND disadvantages listed. Recommendation ties to stated priorities (battery life). "When NOT to use" section for each option.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "Compare FreeRTOS, Zephyr, and bare-metal for a motor controller on STM32F4. Hard real-time requirement: 10kHz control loop."

**Expected Behavior:** Three-way comparison. Criteria include: real-time guarantees, overhead, complexity, ecosystem, learning curve. The 10kHz requirement heavily constrains the analysis.

**Pass Criteria:** Addresses 10kHz constraint directly. Bare-metal acknowledged as lowest overhead but highest complexity. Reversibility assessment included.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "LVGL vs TFT_eSPI for my ESP32-S3 display project. I need widgets, touch support, and animations on a 480x320 screen."

**Expected Behavior:** Structured comparison. LVGL: full widget toolkit, built-in touch, animation engine, higher memory usage. TFT_eSPI: graphics primitives only, need manual widget implementation, lower memory.

**Pass Criteria:** Criteria match the user's needs (widgets, touch, animations). Memory/Flash usage quantified where possible. Recommendation with reasoning.

---

## Prompt 4 — POSITIVE

**Prompt:**
> "Pros and cons of using PlatformIO vs ESP-IDF native toolchain for an industrial IoT product?"

**Expected Behavior:** Comparison covering: build system, debugging, library management, CI/CD integration, long-term support, team adoption.

**Pass Criteria:** Both options have listed disadvantages. "When NOT to use" for each. Addresses "industrial IoT product" context (long-term support matters more than convenience).

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "I've decided to use MQTT. How do I implement a publish/subscribe client on ESP32?"

**Expected Behavior:** Decision already made. No comparison needed. Use `structured-technical-response` or `embedded-automation-design`.

**Pass Criteria:** No comparison matrix. Direct implementation guidance.

---

## Prompt 6 — NEGATIVE

**Prompt:**
> "What is MQTT?"

**Expected Behavior:** Factual question. Direct answer. No tradeoff analysis.

**Pass Criteria:** Brief definition without comparison structure.

---

## Prompt 7 — NEGATIVE (Boundary)

**Prompt:**
> "Tell me about the differences between SPI and I2C."

**Expected Behavior:** This is an educational explanation, not a decision-making comparison. Use `structured-technical-response` to explain differences. Only trigger `data-driven-tradeoff-analysis` if the user has a specific project context and needs to CHOOSE between them.

**Pass Criteria:** Educational explanation format, not comparison matrix with recommendation.
