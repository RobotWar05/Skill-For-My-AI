# SKILL: structured-technical-response

---

## 1. NAME

`structured-technical-response`

---

## 2. DESCRIPTION

Enforces a four-section response format (Summary of Request → Analysis/Architecture → Result/Solution → Additional Recommendations) for all non-trivial technical responses. This skill ensures that technical communication is clear, complete, and easy to follow — preventing stream-of-consciousness answers that bury the key information.

---

## 3. PURPOSE

Unstructured technical responses are hard to review, easy to misinterpret, and difficult to act on. This skill exists to:

- Ensure the agent demonstrates it understood the question before answering.
- Force analytical depth before jumping to solutions.
- Make responses scannable — readers can jump to the section they need.
- Capture secondary recommendations that would otherwise be forgotten.

---

## 4. USE WHEN

- The agent is producing a technical response longer than a short paragraph.
- The response involves analysis, architecture, implementation plans, or technical explanations.
- The user asks "how should I...", "what's the best approach to...", "explain...", "propose a solution for..."
- The response would benefit from structure (more than 3 paragraphs of content).

---

## 5. DO NOT USE WHEN

- The response is trivially short: a one-line answer, a yes/no, a single code snippet with obvious context.
- The `requirement-intake` skill is active (it has its own output format; do not double-format).
- The user explicitly asks for a quick/short answer.
- The response is purely a code block with minimal explanation needed.
- The task is a review/debug task (use `review-debug-deep-mode` which has its own finding format).

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
2. **Determine if this skill applies.** If the response would be under ~5 sentences, this skill is overhead — answer directly.
3. **Write Section 1 (Summary).** Demonstrate understanding. Flag ambiguities.
4. **Write Section 2 (Analysis).** Break down the technical aspects. Consider architecture, constraints, and alternatives.
5. **Write Section 3 (Solution).** Provide the concrete answer. Include code, configs, or steps as needed.
6. **Write Section 4 (Recommendations).** Add value beyond the direct answer: risks, improvements, testing.
7. **Review the response.** Does each section serve its purpose? Is there redundancy between sections? Trim if needed.

---

## 9. CONSTRAINTS

- MUST include all four section headers, even if a section is brief.
- MUST NOT merge sections (e.g., combining Analysis and Solution into one block).
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

- Reference: `AGENTS.md` Section 6 (Response Structure) — this skill is the detailed implementation of that rule.
- No scripts or assets required.
