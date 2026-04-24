# SKILL: data-driven-tradeoff-analysis

---

## 1. NAME

`data-driven-tradeoff-analysis`

---

## 2. DESCRIPTION

Conducts evidence-based comparison of two or more technical alternatives when a decision has multiple viable paths. For each option, documents the rationale, concrete advantages, concrete disadvantages, and specific conditions where it should or should not be used. Produces a structured recommendation with explicit reasoning, not opinion.

---

## 3. PURPOSE

Technical decisions made on gut feeling or vendor marketing lead to regret. This skill exists to:

- Structure comparison so that no important criterion is overlooked.
- Force the agent to document WHY an option is better, not just THAT it is.
- Ensure disadvantages and failure conditions are stated, not hidden.
- Produce a referenceable decision record.

---

## 4. USE WHEN

- User asks to compare two or more technologies, frameworks, libraries, or approaches.
- User asks "which should I use?", "A vs B?", "pros and cons of X?"
- A technical decision has multiple viable paths and the tradeoffs need analysis.
- User asks to evaluate options for a design decision (architecture, protocol, tool choice).

---

## 5. DO NOT USE WHEN

- The decision is already made and the task is implementation.
- Only one option exists (no comparison needed).
- The comparison is non-technical (business strategy, team organization).
- The user is asking how to USE a specific technology (use `structured-technical-response`).
- The user needs requirements clarification first (use `requirement-intake`).

---

## 6. EXPECTED INPUTS

- Two or more technical alternatives to compare.
- Context: what is the use case? What are the priorities (performance, cost, time, reliability)?
- Optionally: constraints that favor or eliminate certain options.

---

## 7. EXPECTED OUTPUTS

A structured comparison containing:

1. **DECISION CONTEXT** — What decision is being made and why it matters.
2. **EVALUATION CRITERIA** — The criteria used for comparison, ordered by priority.
3. **COMPARISON MATRIX** — For each option, score against each criterion with evidence.
4. **DETAILED ANALYSIS** — For each option:
   - Rationale: why consider this option?
   - Advantages: concrete, not vague ("30% less RAM" not "more efficient").
   - Disadvantages: concrete, not hidden.
   - When NOT to use: specific conditions where this option fails.
5. **RECOMMENDATION** — Which option to choose, with explicit reasoning.
6. **REVERSIBILITY** — How hard is it to switch to a different option later?

---

## 8. WORKFLOW

1. **Clarify the decision.** What exactly is being chosen? What are the constraints?
2. **List the options.** Verify each option is technically viable (eliminate obviously impossible ones).
3. **Define evaluation criteria.** Ask the user for priorities, or propose reasonable defaults:
   - Performance, resource usage, complexity, learning curve, community/support, cost, portability, maintainability.
4. **Research each option against each criterion.** Use facts: benchmarks, documentation, known limitations.
5. **Build the comparison matrix.** Fill every cell. If data is unavailable, say "DATA NEEDED" — do NOT guess.
6. **Write detailed analysis** for each option: rationale, advantages, disadvantages, failure conditions.
7. **Assess reversibility.** Can the team switch later without major rewrite?
8. **Make a recommendation.** State which option you recommend, tie it to the criteria and constraints, and explain the tradeoff accepted.
9. **State what would change the recommendation.** "If [condition changes], then [other option] would be better because [reason]."

---

## 9. CONSTRAINTS

- MUST compare against defined criteria, not vague impressions.
- MUST state disadvantages for EVERY option, including the recommended one.
- MUST cite evidence (benchmarks, documentation, known issues) where available.
- MUST mark cells as "DATA NEEDED" rather than guessing when evidence is unavailable.
- MUST include a "When NOT to use" section for each option.
- MUST assess reversibility.
- MUST NOT present the recommendation as the only possible choice. It's the best choice given the stated criteria and constraints.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT fabricate benchmark numbers or performance claims.
- Do NOT invent library features or capabilities.
- Do NOT claim community support levels without evidence (GitHub stars, npm downloads, forum activity).
- Do NOT present pricing or licensing terms you're not confident about.
- Do NOT claim compatibility without verification.
- If you lack data for a comparison cell, say so explicitly.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Should I use FreeRTOS or Zephyr for this ESP32 project?"
2. "Compare MQTT, CoAP, and HTTP for IoT device communication."
3. "Pros and cons of using PlatformIO vs ESP-IDF directly?"
4. "Which display library should I use: LVGL, TFT_eSPI, or U8g2?"
5. "Evaluate React vs Vue vs Svelte for this dashboard."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "I've decided to use MQTT. How do I implement it?" → Decision made. Use `structured-technical-response` or `embedded-automation-design`.
2. "Fix this MQTT connection bug." → Debug task. Use `review-debug-deep-mode`.
3. "Design the architecture for my IoT system." → Use `architecture-first-solutioning`.
4. "What is MQTT?" → Factual question. Answer directly or use `structured-technical-response`.

---

## 13. ADAPTATION NOTES

- **Per project:** Add project-specific evaluation criteria (e.g., "must support OTA updates", "must fit in 256KB Flash").
- **Per domain:** Weight criteria differently (embedded: resource usage high priority; web: developer velocity high priority).
- These adaptations go in a **project overlay**.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `AGENTS.md` Section 4 — Data-driven decision making.
- No scripts or assets required.
