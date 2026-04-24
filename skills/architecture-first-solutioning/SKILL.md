# SKILL: architecture-first-solutioning

---

## 1. NAME

`architecture-first-solutioning`

---

## 2. DESCRIPTION

For medium-to-large tasks, forces a structured architecture analysis (data flow, control flow, state management, timing, hardware constraints, maintainability, scalability) before any code is written or solution is committed. Prevents premature implementation by ensuring the system's structure is understood and validated first.

---

## 3. PURPOSE

Writing code without understanding the architecture leads to rewrites, hidden coupling, and fragile systems. This skill exists to:

- Force the agent to think about the system as a whole before diving into implementation.
- Surface architectural risks (tight coupling, state explosion, timing issues) early.
- Produce a design that can be reviewed before implementation begins.
- Ensure non-functional requirements (maintainability, scalability, safety) are considered upfront.

---

## 4. USE WHEN

- Task involves designing a new system or subsystem.
- Task involves adding a significant feature that touches multiple modules.
- Task involves refactoring a major component.
- Task involves choosing between architectural patterns (event-driven vs polling, monolith vs modular).
- The request implies 3+ interacting components or modules.
- User says "design", "architect", "how should I structure", "what's the best way to organize."

---

## 5. DO NOT USE WHEN

- Task is a localized bug fix within a single function.
- Task is implementing a single, well-defined function where the design is already decided.
- Task is a configuration change.
- The architecture is already established and the task is "implement this known design."
- Task is a code review (use `review-debug-deep-mode`).
- Task is intake/clarification (use `requirement-intake` first, then this skill).

---

## 6. EXPECTED INPUTS

- Problem statement or feature request requiring multi-component design.
- Optionally: existing codebase, architecture diagrams, constraint documents.
- Optionally: output of `requirement-intake` skill (intake summary).

---

## 7. EXPECTED OUTPUTS

An architecture analysis document containing:

1. **SYSTEM OVERVIEW** — High-level description of the system and its boundaries.
2. **DATA FLOW** — How data moves through the system (sources, transformations, sinks).
3. **CONTROL FLOW** — What triggers actions, how decisions are made, what sequences must be followed.
4. **STATE MANAGEMENT** — What state exists, where it lives, how it transitions, what happens on failure.
5. **TIMING AND CONCURRENCY** — Timing requirements, concurrent execution, synchronization needs.
6. **CONSTRAINTS** — Hardware limits, resource budgets, compatibility requirements.
7. **LAYER DIAGRAM** — How the system is decomposed into layers or modules and their dependencies.
8. **RISKS AND TRADEOFFS** — Known risks, tradeoff decisions made, and their rationale.
9. **RECOMMENDED ARCHITECTURE** — The proposed design with justification.

---

## 8. WORKFLOW

1. **Confirm intake is complete.** If requirements are unclear, activate `requirement-intake` first.
2. **Identify system boundaries.** What is inside the system? What is external?
3. **Map data flow.** Trace data from sources through processing to outputs.
4. **Map control flow.** Trace decision points, triggers, and action sequences.
5. **Identify state.** List all stateful elements. Define valid states and transitions.
6. **Analyze timing.** Identify real-time constraints, latency budgets, update frequencies.
7. **Identify concurrency.** Are there parallel tasks? Shared resources? Synchronization needs?
8. **List constraints.** Hardware limits, memory budgets, power budgets, compatibility.
9. **Propose layer decomposition.** Separate concerns into layers/modules with clear interfaces.
10. **Assess risks.** What could go wrong? What are the architectural weaknesses?
11. **Document tradeoffs.** What alternatives were considered? Why was this design chosen?
12. **Present the architecture** for review before proceeding to implementation.

---

## 9. CONSTRAINTS

- MUST complete architecture analysis before writing implementation code.
- MUST address all 9 output sections (mark as "Not applicable — [reason]" if genuinely irrelevant).
- MUST identify at least one risk or tradeoff — no design is risk-free.
- MUST propose a layer decomposition — even simple systems benefit from separation.
- MUST NOT conflate architecture with implementation detail (e.g., specific variable names are implementation, not architecture).
- MUST present the architecture for user review before proceeding.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT invent hardware specifications (clock speeds, memory sizes, pin counts) unless provided by the user or verified from documentation.
- Do NOT claim a library or framework supports a feature without verification.
- Do NOT fabricate performance numbers for the proposed architecture.
- Do NOT present architectural opinions as universal facts. State them as recommendations with reasoning.
- If you don't know a hardware constraint, say so explicitly.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Design the software architecture for a multi-sensor IoT gateway."
2. "How should I structure the firmware for a device with BLE, WiFi, and a display?"
3. "I need to refactor this monolithic main.cpp into proper modules. How?"
4. "Architect a communication system between 5 ESP32 nodes and a central server."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "Fix the null pointer dereference in sensor_read()." → Bug fix. Use `review-debug-deep-mode`.
2. "Implement the PID controller using this formula." → Design is decided; implement directly.
3. "Change the WiFi SSID in config.h." → Configuration change.
4. "Compare FreeRTOS vs Zephyr." → Use `data-driven-tradeoff-analysis`.

---

## 13. ADAPTATION NOTES

- **For embedded projects:** Always include memory budget, power analysis, and RTOS task layout in the architecture.
- **For web projects:** Focus on API boundaries, database schema, and deployment topology.
- **For mixed projects:** Create separate architecture sections for firmware and backend.
- These adaptations go in a **project overlay**.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `docs/repo-philosophy.md` — Architecture First principle.
- Reference: `AGENTS.md` Section 7 — Embedded/automation defaults apply during architecture.
- No scripts or assets required.
