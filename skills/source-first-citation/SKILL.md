# SKILL: source-first-citation

---

## 1. NAME

`source-first-citation`

---

## 2. DESCRIPTION

When the user provides source materials (code files, logs, documentation, configuration files, system descriptions, or error output), this skill ensures the agent treats those materials as primary evidence. The agent must cite specific locations (file, module, function, line number) from user-provided sources and rely on external knowledge only when the provided context is genuinely insufficient.

---

## 3. PURPOSE

AI agents tend to answer from general knowledge even when the user has provided specific context. This skill corrects that by enforcing a "use what you've been given first" discipline.

---

## 4. USE WHEN

- User has provided or referenced files (code, logs, docs, configs).
- User has pasted code snippets, error messages, or log output.
- User says "here is my code", "look at this", "based on this file", "this log shows."

---

## 5. DO NOT USE WHEN

- User asks a general knowledge question without providing source material.
- User asks about an external tool/API they haven't provided docs for.
- No source material is available in the context.

---

## 6. EXPECTED INPUTS

- User-provided source materials + a question or task related to those materials.

---

## 7. EXPECTED OUTPUTS

A response that:
1. Cites specific locations (file, module, function, line number).
2. Bases conclusions on provided evidence first.
3. Clearly marks external references when used.
4. Does NOT silently contradict the provided sources.

---

## 8. WORKFLOW

1. **Inventory provided sources.** List all files, snippets, logs, and documents given.
2. **Read all sources before responding.** Do not start answering after reading only part.
3. **Identify relevant sections.** Find specific locations relevant to the question.
4. **Form conclusions from sources first.** Build answer primarily from what sources show.
5. **Cite locations explicitly.** State file, function, and line number.
6. **Supplement with external knowledge only when needed.** Label clearly: "External reference: ..."
7. **Flag contradictions.** If external knowledge contradicts sources, call it out explicitly.

---

## 9. CONSTRAINTS

- MUST reference user-provided sources before using external knowledge.
- MUST cite specific locations (file, function, line) when referencing source material.
- MUST NOT silently override source material with general knowledge.
- MUST label all external references explicitly.
- MUST read ALL provided sources before beginning the response.
- MUST NOT claim a function/variable exists in the source unless it's visible in the provided material.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT invent function names, variable names, or code structures not in provided sources.
- Do NOT claim a file contains something you haven't actually seen.
- Do NOT fabricate line numbers. Say "approximately" if unsure.
- Do NOT assume the user's code follows standard patterns. Read what's actually there.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Here's my main.cpp. Why does the motor spin the wrong direction?" [code attached]
2. "Look at this log output. What's causing the timeout?" [log pasted]
3. "Based on this schematic, is my GPIO mapping correct?"
4. "I've attached my platformio.ini and driver code. Why does compilation fail?"
5. "Here's my state machine implementation. Is the transition from IDLE to RUNNING correct?"

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "How does I2C work?" → General knowledge question. No sources provided.
2. "What's the best RTOS for ESP32?" → Use `data-driven-tradeoff-analysis`.
3. "Explain the difference between UART and SPI." → General knowledge.
4. "Should I use PlatformIO or Arduino IDE?" → General comparison.

---

## 13. ADAPTATION NOTES

- **Add project-specific file conventions** (e.g., "source in `src/`, headers in `include/`").
- **Add project-specific source types** (e.g., "KiCad schematics — cite by sheet name").
- **Define project-specific external reference rules** (e.g., "cross-reference ESP-IDF docs").
- These adaptations go in a **project overlay**.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `AGENTS.md` Section 5 (Context First).
- No scripts or assets required.
