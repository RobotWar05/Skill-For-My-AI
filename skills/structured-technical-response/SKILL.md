---
name: structured-technical-response
description: Use when the primary task is to shape a non-trivial technical answer into the user's preferred structured format, without replacing a more specific domain skill's workflow or overriding evidence, review, architecture, or comparison processes.
---

# SKILL: structured-technical-response

---

## 1. NAME

`structured-technical-response`

---

## 2. DESCRIPTION

Shapes a non-trivial technical answer into the user's preferred four-section format (Summary of Request -> Analysis/Architecture -> Result/Solution -> Additional Recommendations) when response structure is the primary need. This skill improves communication clarity without replacing a more specific domain workflow such as review/debug, architecture design, embedded design, source citation, or tradeoff analysis.

---

## 3. PURPOSE

Unstructured technical responses are hard to review, easy to misinterpret, and difficult to act on. This skill exists to:

- Ensure the agent demonstrates it understood the question before answering.
- Add communication structure when no more specific skill already defines the main workflow.
- Make responses scannable — readers can jump to the section they need.
- Capture secondary recommendations that would otherwise be forgotten.

---

## 4. USE WHEN

- The primary task is shaping a technical answer into the repo's standard structured response style.
- The user explicitly asks for a structured answer, organized technical explanation, implementation plan, or solution write-up.
- The response would otherwise be more than 3 paragraphs and no more specific skill defines the main workflow.
- The skill is being combined with another skill only to format the final answer after that skill's workflow is complete.

---

## 5. DO NOT USE WHEN

- The response is trivially short: a one-line answer, a yes/no, a single code snippet with obvious context.
- The `requirement-intake` skill is active (it has its own output format; do not double-format).
- The user explicitly asks for a quick/short answer.
- The response is purely a code block with minimal explanation needed.
- The task is a review/debug task (use `review-debug-deep-mode` which has its own finding format).
- The task is primarily architecture, embedded design, source-grounded citation, or option comparison; use the relevant domain skill first and apply only basic response structure unless the user asks for this format.

---

## 6. EXPECTED INPUTS

- A technical question, problem description, or discussion topic from the user.
- Optionally: code, diagrams, logs, or documentation as context.

---

## 7. EXPECTED OUTPUTS

A response organized into four sections:

### Section 1: SUMMARY OF REQUEST
- Restate what the user asked in 1–3 sentences.
- Demonstrate understanding before providing the answer.
- If the request has ambiguity, note it here.

### Section 2: ANALYSIS / ARCHITECTURE
- Technical breakdown of the problem.
- For implementation questions: discuss architecture, data flow, state, constraints.
- For explanation questions: break down the concept into components.
- For comparison questions: defer to `data-driven-tradeoff-analysis` skill.

### Section 3: RESULT / SOLUTION
- The concrete answer, implementation, or recommendation.
- Code if applicable.
- Configuration if applicable.
- Step-by-step instructions if applicable.

### Section 4: ADDITIONAL RECOMMENDATIONS
- What else the user should consider.
- Potential risks or limitations of the solution.
- Future improvements or alternative approaches.
- Testing suggestions.

---

## 8. WORKFLOW

1. **Read the full request** before starting the response.
2. **Determine if this skill applies.** If a more specific skill defines the main workflow, do not replace it; only use this skill to shape the final response when useful.
3. **Write Section 1 (Summary).** Demonstrate understanding. Flag ambiguities.
4. **Write Section 2 (Analysis).** Break down the technical aspects. Consider architecture, constraints, and alternatives.
5. **Write Section 3 (Solution).** Provide the concrete answer. Include code, configs, or steps as needed.
6. **Write Section 4 (Recommendations).** Add value beyond the direct answer: risks, improvements, testing.
7. **Review the response.** Does each section serve its purpose? Is there redundancy between sections? Trim if needed.

---

## 9. CONSTRAINTS

- MUST include all four section headers, even if a section is brief.
- MUST NOT merge sections (e.g., combining Analysis and Solution into one block).
- MUST NOT override the workflow or output obligations of a more specific active skill.
- MUST keep Section 1 (Summary) concise — 1-3 sentences maximum.
- MUST ensure Section 3 (Solution) is actionable — the user should be able to act on it without re-reading the Analysis.
- MUST NOT pad sections with filler text. If a section is genuinely short, that's fine.
- Section 4 (Recommendations) MUST contain at least one concrete recommendation, not a generic "consider testing."

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT fabricate technical details in the Analysis section to appear thorough.
- Do NOT recommend libraries, tools, or APIs you're not confident exist.
- Do NOT claim performance characteristics without evidence or measurement.
- In the Summary section, do NOT add requirements the user didn't mention.
- In the Recommendations section, do NOT recommend actions without explaining WHY.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "How should I implement a communication protocol between an ESP32 and a Raspberry Pi over UART?"
2. "Explain how FreeRTOS task priorities work and how to avoid priority inversion."
3. "What's the best approach to handle OTA firmware updates on a resource-constrained MCU?"
4. "Propose a solution for synchronizing data between a local SQLite database and a cloud backend."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "What is the default baud rate for Serial.begin()?" → One-line answer. No structure needed.
2. "Here's my code, find the bugs." → Use `review-debug-deep-mode` instead.
3. "I need to build a complete monitoring system..." → Use `requirement-intake` first.
4. "Should I use MQTT or CoAP?" → Use `data-driven-tradeoff-analysis` instead.
5. "Yes." / "No." / "42." → Trivial response. No structure needed.

---

## 13. ADAPTATION NOTES

When adapting for a specific project:

- **Section headers can be renamed** to match project conventions (e.g., "ARCHITECTURAL IMPACT" instead of "ANALYSIS / ARCHITECTURE") — but all four sections must remain.
- **Section 2 (Analysis)** can be tailored to emphasize project-specific concerns (e.g., for embedded projects: always address memory and timing; for web projects: always address latency and scaling).
- **Section 4 (Recommendations)** can include project-specific checklists (e.g., "update the CHANGELOG", "run the integration test suite").
- These adaptations go in a **project overlay**, not in this canonical skill.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `AGENTS.md` response structure rule — this skill is the detailed communication workflow for cases where structured presentation is the primary need.
- No scripts or assets required.
