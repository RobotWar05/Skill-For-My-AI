# Skill Catalog

> **Agents: Read this file to find the right skill for your current task.**
> If no skill matches, use `skill-scaffolder` to create a new one.

---

## Scope Classes

- **global**: Applies across most technical domains and agent workflows.
- **domain-specific**: Applies to a specific technical domain.
- **scaffolder/meta**: Creates or governs skills rather than solving a user-domain task directly.

---

## Catalog Index

| # | Skill Name | Scope | Purpose | Maturity |
|---|---|---|---|---|
| 1 | [requirement-intake](#1-requirement-intake) | global | Structured intake for medium-to-large requirements | Stable |
| 2 | [structured-technical-response](#2-structured-technical-response) | global | Shape technical answers into the repo's structured response style | Stable |
| 3 | [source-first-citation](#3-source-first-citation) | global | Prioritize user-provided sources over external knowledge | Stable |
| 4 | [architecture-first-solutioning](#4-architecture-first-solutioning) | global | Architecture analysis before implementation | Stable |
| 5 | [review-debug-deep-mode](#5-review-debug-deep-mode) | global | Deep analysis for review, debug, and optimization tasks | Stable |
| 6 | [embedded-automation-design](#6-embedded-automation-design) | domain-specific | Embedded/automation design with production constraints | Stable |
| 7 | [skill-scaffolder](#7-skill-scaffolder) | scaffolder/meta | Create new skills from template | Stable |
| 8 | [data-driven-tradeoff-analysis](#8-data-driven-tradeoff-analysis) | global | Evidence-based comparison of technical alternatives | Stable |
| 9 | [coding-agent-discipline](#9-coding-agent-discipline) | global | Keep AI coding changes focused, simple, and verifiable | Stable |

---

## Boundary Notes

- **requirement-intake vs architecture-first-solutioning:** Use `requirement-intake` when the problem is not yet well-defined. Use `architecture-first-solutioning` after requirements are clear and the system structure needs design.
- **architecture-first-solutioning vs embedded-automation-design:** Use `architecture-first-solutioning` for general multi-component design. Add `embedded-automation-design` when firmware, hardware, real-time, interrupt, watchdog, or resource constraints are central.
- **structured-technical-response vs AGENTS.md default response structure:** `AGENTS.md` defines the default response convention. Use `structured-technical-response` only when shaping the answer format is the primary task or the user explicitly wants a structured technical write-up.
- **review-debug-deep-mode vs embedded-automation-design:** Use `review-debug-deep-mode` for existing failures, bugs, or audits. Add embedded constraints from `embedded-automation-design` when the reviewed system is firmware or real-time automation.

---

## Skill Details

### 1. requirement-intake

- **Path:** `skills/requirement-intake/SKILL.md`
- **Scope:** global
- **Purpose:** Conducts structured intake of medium-to-large technical requirements before solution work begins.
- **Use when:** User provides a multi-paragraph problem statement, a feature request with multiple parts, or a system design brief that needs decomposition.
- **Do NOT use when:** User asks a direct factual question, requests a single-line code fix, or the requirement is already clear and atomic.
- **Trigger keywords:** "requirement", "specification", "feature request", "build me", "design a system", "project brief", "I need a system that..."
- **Anti-trigger keywords:** "fix this line", "what does X mean", "quick question"
- **Input:** Problem statement, feature description, or system brief from user.
- **Output:** Structured intake summary with request summary, constraints, missing information, and true technical objective.
- **Dependencies:** None.

---

### 2. structured-technical-response

- **Path:** `skills/structured-technical-response/SKILL.md`
- **Scope:** global
- **Purpose:** Shapes a non-trivial technical answer into the repo's four-section structured response style when response presentation is the primary need.
- **Use when:** User asks for a structured technical explanation, plan, solution write-up, or the answer would otherwise be long and no more specific skill defines the main workflow.
- **Do NOT use when:** Another domain skill already defines the main workflow and only basic response structure is needed.
- **Trigger keywords:** "structured answer", "organize this", "technical write-up", "implementation plan", "explain in sections"
- **Anti-trigger keywords:** "quick answer", "one-liner", "review this code", "A vs B", "intake this requirement"
- **Input:** A technical question, problem, or draft answer that needs structured presentation.
- **Output:** Four-section structured response.
- **Dependencies:** None. Can format the final output of another skill without overriding that skill's workflow.

---

### 3. source-first-citation

- **Path:** `skills/source-first-citation/SKILL.md`
- **Scope:** global
- **Purpose:** Ensures user-provided materials are treated as primary evidence and cited specifically.
- **Use when:** User has attached or referenced files, code snippets, log output, documentation, or system descriptions.
- **Do NOT use when:** User asks a general knowledge question without providing source material.
- **Trigger keywords:** "here is my code", "look at this file", "this log shows", "in my system", "attached documentation", "based on this"
- **Anti-trigger keywords:** "how does X generally work", "what is the standard for", "best practice for"
- **Input:** User-provided source material plus a question or task.
- **Output:** Response that cites specific files, modules, functions, or line numbers where possible.
- **Dependencies:** None. Typically active alongside other skills.

---

### 4. architecture-first-solutioning

- **Path:** `skills/architecture-first-solutioning/SKILL.md`
- **Scope:** global
- **Purpose:** Forces architecture analysis before implementation for medium-to-large technical tasks.
- **Use when:** Task involves designing a system, adding a significant feature, refactoring a major component, or making a multi-module design decision.
- **Do NOT use when:** Task is a localized bug fix, a single-function implementation, or a configuration change.
- **Trigger keywords:** "design a system", "architect", "how should I structure", "refactor this module", "add a major feature", "system design"
- **Anti-trigger keywords:** "fix this bug", "implement this function", "change this config", "the design is already decided"
- **Input:** Problem statement or feature request requiring multi-component design.
- **Output:** Architecture analysis covering data flow, control flow, state management, timing, constraints, and recommendations.
- **Dependencies:** Often preceded by `requirement-intake`.

---

### 5. review-debug-deep-mode

- **Path:** `skills/review-debug-deep-mode/SKILL.md`
- **Scope:** global
- **Purpose:** Activates systematic review/debug/optimization analysis with severity, root cause, and regression risk.
- **Use when:** User asks to review code, debug an issue, optimize performance, analyze a failure, or identify what is wrong in existing behavior.
- **Do NOT use when:** User asks to write new code from scratch or asks for a general explanation.
- **Trigger keywords:** "review this", "debug", "what's wrong", "why does this fail", "optimize", "find bugs", "code review", "root cause"
- **Anti-trigger keywords:** "write new code", "implement from scratch", "explain how X works in general"
- **Input:** Code, logs, error messages, or system description with a review/debug/optimization request.
- **Output:** Findings with severity classification, root cause analysis, fix proposals, and regression assessment.
- **Dependencies:** Follows `docs/review-debug-standards.md`.

---

### 6. embedded-automation-design

- **Path:** `skills/embedded-automation-design/SKILL.md`
- **Scope:** domain-specific
- **Purpose:** Applies production-grade embedded and automation design principles.
- **Use when:** Task involves firmware, RTOS tasks, interrupts, hardware abstraction, real-time control, communication protocols, or embedded system design.
- **Do NOT use when:** Task is pure software with no embedded, hardware, or real-time constraints.
- **Trigger keywords:** "firmware", "embedded", "RTOS", "ISR", "interrupt", "GPIO", "SPI", "I2C", "UART", "timer", "watchdog", "state machine", "non-blocking", "ESP32", "STM32", "PIC", "Arduino", "driver"
- **Anti-trigger keywords:** "web app", "REST API", "database", "frontend", "machine learning model", "cloud service"
- **Input:** Embedded system design task, firmware implementation request, or hardware abstraction design.
- **Output:** Design or implementation following embedded best practices with explicit rationale.
- **Dependencies:** Often combined with `architecture-first-solutioning` for larger designs.

---

### 7. skill-scaffolder

- **Path:** `skills/skill-scaffolder/SKILL.md`
- **Scope:** scaffolder/meta
- **Purpose:** Creates new skills from the canonical template when no existing skill matches the current task.
- **Use when:** The agent has checked the catalog, found no matching skill, and needs to create a new one, or the user explicitly asks to create a new skill.
- **Do NOT use when:** An existing skill already covers the task, the need is project-specific, or the content belongs in docs or AGENTS.md.
- **Trigger keywords:** "create a new skill", "no skill matches", "scaffold a skill", "I need a skill for"
- **Anti-trigger keywords:** "use existing skill", "run the review skill", "follow the template"
- **Input:** Description of the task type that needs a new skill.
- **Output:** Complete `SKILL.md`, catalog entry, eval prompts, and classification report.
- **Dependencies:** `templates/skill-template/SKILL.md`, `docs/skill-authoring-rules.md`.

---

### 8. data-driven-tradeoff-analysis

- **Path:** `skills/data-driven-tradeoff-analysis/SKILL.md`
- **Scope:** global
- **Purpose:** Conducts evidence-based comparison of two or more technical alternatives.
- **Use when:** User asks to compare technologies, frameworks, approaches, or design options with multiple viable paths.
- **Do NOT use when:** The decision is already made, only one option exists, or the comparison is non-technical.
- **Trigger keywords:** "compare", "which should I use", "tradeoff", "pros and cons", "A vs B", "evaluate options", "which is better"
- **Anti-trigger keywords:** "implement this", "I've already decided", "just use X", "how do I use X"
- **Input:** Two or more technical alternatives with use-case context.
- **Output:** Structured comparison matrix with evidence, recommendation, risks, and conditions for each option.
- **Dependencies:** May follow `requirement-intake` if criteria need clarification.

---

### 9. coding-agent-discipline

- **Path:** `skills/coding-agent-discipline/SKILL.md`
- **Scope:** global
- **Purpose:** Keeps AI coding changes simple, surgical, assumption-aware, and verifiable before code is modified.
- **Use when:** An AI coding agent is about to implement, refactor, or edit code and must define success criteria, avoid over-engineering, and preserve unrelated files.
- **Do NOT use when:** The user asks only for explanation, documentation, scheduling, or a non-coding analysis task.
- **Trigger keywords:** "implement", "refactor", "modify code", "fix this", "add feature", "make code changes", "patch"
- **Anti-trigger keywords:** "explain", "summarize", "compare options", "review only", "no code changes"
- **Input:** Coding task, codebase context, requested change, and constraints.
- **Output:** Brief execution discipline: assumptions, success criteria, surgical plan, verification approach, and focused implementation behavior.
- **Dependencies:** Can combine with `review-debug-deep-mode`, `architecture-first-solutioning`, or domain skills depending on the task.
