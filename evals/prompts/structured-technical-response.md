# Eval Prompts: structured-technical-response

---

## Prompt 1 — POSITIVE

**Prompt:**
> "How should I implement a non-blocking UART communication handler on ESP32 with FreeRTOS? I need to receive variable-length packets with a header and CRC."

**Expected Behavior:** Agent produces a 4-section response: Summary → Analysis (ring buffer, task notification, packet parsing state machine) → Solution (code) → Recommendations (error recovery, timeout, testing).

**Pass Criteria:** All 4 sections present with headers. Analysis is substantive (not just "it's complex"). Solution includes code or pseudocode. Recommendations add value beyond the direct question.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "Explain how I2C arbitration works and what happens when two masters try to communicate simultaneously."

**Expected Behavior:** 4-section response. Summary restates question. Analysis breaks down I2C arbitration mechanism (SDA monitoring, bit-level arbitration, clock stretching). Result explains the process clearly. Recommendations mention multi-master design considerations.

**Pass Criteria:** Technical accuracy. All 4 sections present. Analysis goes deeper than a textbook definition.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "What's the best approach to manage shared state between multiple FreeRTOS tasks accessing the same sensor data?"

**Expected Behavior:** Structured response covering mutex, semaphore, queue, and atomic access options with tradeoffs.

**Pass Criteria:** 4 sections present. Analysis discusses multiple approaches. Solution recommends one with rationale. Recommendations mention priority inversion, deadlock risks.

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "What is GPIO?"

**Expected Behavior:** Direct short answer. No 4-section structure (overkill for a definition).

**Pass Criteria:** Brief, accurate definition without section headers.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Yes."

**Expected Behavior:** Context-dependent short response. No structured format.

**Pass Criteria:** No 4-section structure applied.

---

## Prompt 6 — NEGATIVE

**Prompt:**
> "Here's my motor driver code. Review it for bugs." [code attached]

**Expected Behavior:** Agent uses `review-debug-deep-mode`, NOT `structured-technical-response`. Output follows finding format, not 4-section response.

**Pass Criteria:** Findings with severity levels, not a 4-section analysis.
