---
name: requirement-intake
description: Use when the user presents a medium or large technical task and the agent must restate requirements, identify constraints, list missing information, and define the true engineering goal before proposing architecture, code, or a final solution.
---

# SKILL: requirement-intake

---

## 1. NAME

`requirement-intake`

---

## 2. DESCRIPTION

Enforces a structured intake process for medium-to-large technical requirements: summarizes the request, identifies explicit and implicit constraints, lists missing information that blocks proper solution design, and defines the true technical objective before any solution work begins. This skill prevents premature implementation by ensuring the problem is fully understood first.

---

## 3. PURPOSE

Many technical tasks fail not because of poor implementation but because of poor requirement understanding. This skill exists to:

- Force a deliberate pause between "receiving a request" and "starting to solve it."
- Surface hidden constraints and assumptions early.
- Identify what information is missing before committing to a direction.
- Translate vague user intent into a concrete technical objective.

---

## 4. USE WHEN

- User provides a multi-paragraph problem statement that requires decomposition.
- User describes a feature or system with multiple interacting requirements.
- User provides a project brief or specification document.
- The request involves designing or building something with non-trivial scope (more than a single function or file).
- The request has ambiguity: the user's words could be interpreted in multiple ways.
- User says "build me...", "I need a system that...", "design a...", "create a solution for..."

---

## 5. DO NOT USE WHEN

- User asks a direct factual question with no ambiguity (e.g., "What is the baud rate for UART0?").
- User requests a single-line code fix or syntax correction.
- The requirement is already clear, atomic, and fully specified.
- User explicitly says "skip the analysis, just implement."
- The task is a review or debug task (use `review-debug-deep-mode` instead).
- User is comparing options (use `data-driven-tradeoff-analysis` instead).

---

## 6. EXPECTED INPUTS

- A problem statement, feature request, system design brief, or specification document from the user.
- Optionally: existing code, architecture diagrams, or constraints documents.
- Optionally: user-stated priorities or non-functional requirements.

---

## 7. EXPECTED OUTPUTS

A structured intake document containing:

1. **REQUEST SUMMARY** — A concise restatement of what the user is asking for, in the agent's own words.
2. **CONSTRAINTS IDENTIFIED** — Both explicit (stated by user) and implicit (inferred from context), each labeled as EXPLICIT or INFERRED.
3. **MISSING INFORMATION** — Specific questions or data gaps that prevent a complete solution, prioritized by impact.
4. **TRUE TECHNICAL OBJECTIVE** — The underlying technical goal, which may differ from the user's surface-level request.
5. **ASSUMPTIONS** — Any assumptions made during intake, each labeled `ASSUMPTION` with reasoning.
6. **RECOMMENDED NEXT STEP** — What should happen after intake: proceed to architecture? Clarify with user? Prototype?

---

## 8. WORKFLOW

1. **Read the request completely.** Do not start summarizing until you have processed the entire input.
2. **Identify the request type.** Is this a new system, a feature addition, a migration, a redesign, or something else?
3. **Summarize the request** in your own words. The summary should be shorter than the original but preserve all key information.
4. **Extract explicit constraints.** These are things the user directly stated: technology choices, performance targets, deadlines, platform requirements.
5. **Infer implicit constraints.** These are things the user didn't say but that logically follow: if they mention ESP32, they're constrained to ~520KB RAM. Label each as `INFERRED`.
6. **List missing information.** For each gap, state:
   - What information is missing.
   - Why it matters (what decision it blocks).
   - What you would assume if the user doesn't clarify (label as `ASSUMPTION`).
7. **Define the true technical objective.** Strip away UI-level language and state what technically needs to happen. "I want a smart home dashboard" → "Render sensor data on a touch display with real-time updates and user-configurable thresholds."
8. **List all assumptions** made during intake.
9. **Recommend the next step.** Based on what you know and what's missing, what should happen next?

---

## 9. CONSTRAINTS

- MUST NOT propose solutions during intake. This skill is about understanding, not solving.
- MUST explicitly label every assumption.
- MUST distinguish between explicit constraints (user said it) and inferred constraints (agent derived it).
- MUST list missing information even if the agent can "guess" the answer — the user needs to confirm.
- MUST keep the summary shorter than the original request.
- MUST NOT skip the "true technical objective" step, even if the user's request seems clear.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT invent requirements the user didn't mention or imply.
- Do NOT assume technology choices unless the user specified them.
- Do NOT fabricate performance targets, deadlines, or resource constraints.
- Do NOT claim to have identified "all" constraints — always note that more may exist.
- If you infer a constraint, explain the reasoning chain that led to the inference.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "I want to build an IoT monitoring system that reads temperature and humidity from 5 sensors, displays data on an LCD, and sends alerts to my phone when values exceed thresholds."
2. "Design a communication protocol between an ESP32 master and 3 PIC slave devices over RS485. It needs to handle packet loss, support firmware updates, and work at 115200 baud."
3. "I need a web-based dashboard for my smart home. It should show real-time sensor data, allow me to control lights and HVAC, and have user authentication."
4. "Build me an automated testing rig that controls power supplies, reads ADC values, and generates test reports."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "What's the syntax for a switch statement in C?" → Direct factual question. No intake needed.
2. "Fix the off-by-one error on line 42 of main.c" → Single-line fix. No intake needed.
3. "Review this code for bugs" → Use `review-debug-deep-mode` instead.
4. "Should I use MQTT or HTTP for this?" → Use `data-driven-tradeoff-analysis` instead.
5. "Here's my design doc, please implement step 3" → Requirement is already specified. Proceed to implementation.

---

## 13. ADAPTATION NOTES

When adapting for a specific project:

- **Add project-specific constraint categories** to step 4 (e.g., for an automotive project: functional safety level, AUTOSAR compliance).
- **Add project-specific "missing info" checklist** items (e.g., for embedded: target MCU, RAM/Flash budget, RTOS choice, power budget).
- **Adjust the "true technical objective" framing** to match the project domain (e.g., for a web project, focus on API contracts and data models rather than hardware constraints).
- These adaptations go in a **project overlay**, not in this canonical skill.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `docs/repo-philosophy.md` — explains the "understand before solving" principle.
- No scripts or assets required for this skill.
