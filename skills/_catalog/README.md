# Skill Catalog

> **Agents: Read this file to find the right skill for your current task.**
> If no skill matches, use `skill-scaffolder` to create a new one.

---

## Catalog Index

| # | Skill Name | Purpose | Maturity |
|---|---|---|---|
| 1 | [requirement-intake](#1-requirement-intake) | Structured intake for medium-to-large requirements | Stable |
| 2 | [structured-technical-response](#2-structured-technical-response) | Enforce structured format for technical responses | Stable |
| 3 | [source-first-citation](#3-source-first-citation) | Prioritize user-provided sources over external knowledge | Stable |
| 4 | [architecture-first-solutioning](#4-architecture-first-solutioning) | Architecture analysis before implementation | Stable |
| 5 | [review-debug-deep-mode](#5-review-debug-deep-mode) | Deep analysis for review, debug, and optimization tasks | Stable |
| 6 | [embedded-automation-design](#6-embedded-automation-design) | Embedded/automation design with production constraints | Stable |
| 7 | [skill-scaffolder](#7-skill-scaffolder) | Create new skills from template | Stable |
| 8 | [data-driven-tradeoff-analysis](#8-data-driven-tradeoff-analysis) | Evidence-based comparison of technical alternatives | Stable |

---

## Skill Details

### 1. requirement-intake

- **Path:** `skills/requirement-intake/SKILL.md`
- **Purpose:** Conducts a structured intake of medium-to-large technical requirements before any solution work begins. Summarizes the request, identifies constraints, lists missing information, defines the true technical objective.
- **Use when:** User provides a multi-paragraph problem statement, a feature request with multiple parts, or a system design brief that needs decomposition.
- **Do NOT use when:** User asks a direct factual question, requests a single-line code fix, or the requirement is already clear and atomic.
- **Trigger keywords:** "requirement", "specification", "feature request", "build me", "design a system", "project brief", "I need a system that..."
- **Anti-trigger keywords:** "fix this line", "what does X mean", "quick question"
- **Input:** Problem statement, feature description, or system brief from user.
- **Output:** Structured intake summary with: request summary, constraints, missing information, true technical objective.
- **Dependencies:** None.

---

### 2. structured-technical-response

- **Path:** `skills/structured-technical-response/SKILL.md`
- **Purpose:** Enforces a four-section format (Summary → Analysis → Solution → Recommendations) for non-trivial technical responses to ensure clarity and completeness.
- **Use when:** Agent produces a technical response longer than a short paragraph. Applies to architecture discussions, implementation plans, technical explanations, and solution proposals.
- **Do NOT use when:** Response is trivially short (one-liner, yes/no, single code snippet with obvious context). When `requirement-intake` is active (it has its own output format).
- **Trigger keywords:** "explain how", "how should I implement", "what's the best approach", "design this", "propose a solution"
- **Anti-trigger keywords:** "what is", "define", "one-liner", "quick answer"
- **Input:** A technical question, problem, or discussion topic.
- **Output:** Four-section structured response.
- **Dependencies:** None. Can be combined with other skills.

---

### 3. source-first-citation

- **Path:** `skills/source-first-citation/SKILL.md`
- **Purpose:** When the user has provided source materials (code files, logs, documentation, system descriptions), ensures the agent prioritizes those materials as primary evidence and cites specific locations rather than relying on general knowledge.
- **Use when:** User has attached or referenced files, code snippets, log output, documentation, or system descriptions as part of their request.
- **Do NOT use when:** User asks a general knowledge question without providing any source material. User asks about an external API or tool they haven't provided docs for.
- **Trigger keywords:** "here is my code", "look at this file", "this log shows", "in my system", "attached documentation", "based on this"
- **Anti-trigger keywords:** "how does X generally work", "what is the standard for", "best practice for"
- **Input:** User-provided source material + a question or task.
- **Output:** Response that cites specific files, modules, functions, line numbers from the provided sources.
- **Dependencies:** None. Typically active alongside other skills.

---

### 4. architecture-first-solutioning

- **Path:** `skills/architecture-first-solutioning/SKILL.md`
- **Purpose:** For medium-to-large tasks, forces architecture analysis (data flow, control flow, state, timing, constraints, maintainability) before any code is written or solution is committed.
- **Use when:** Task involves designing a new system, adding a significant feature, refactoring a major component, or making a decision that affects multiple modules.
- **Do NOT use when:** Task is a localized bug fix, a single-function implementation, or a configuration change. When the architecture is already established and the task is "implement this known design."
- **Trigger keywords:** "design a system", "architect", "how should I structure", "refactor this module", "add a major feature", "system design"
- **Anti-trigger keywords:** "fix this bug", "implement this function", "change this config", "the design is already decided"
- **Input:** Problem statement or feature request requiring multi-component design.
- **Output:** Architecture analysis document covering data flow, control flow, state management, timing, constraints, and recommendations.
- **Dependencies:** Often preceded by `requirement-intake`.

---

### 5. review-debug-deep-mode

- **Path:** `skills/review-debug-deep-mode/SKILL.md`
- **Purpose:** Activates deep analysis mode for code review, debugging, and optimization tasks. Searches for both surface-level and latent bugs, assesses risk and regression potential, and prioritizes root cause analysis.
- **Use when:** User asks to review code, debug an issue, optimize performance, or analyze a failure. User provides code or logs and asks "what's wrong" or "why does this fail."
- **Do NOT use when:** User asks to write new code from scratch (use `architecture-first-solutioning`). User asks to explain how something works in general (use `structured-technical-response`).
- **Trigger keywords:** "review this", "debug", "what's wrong", "why does this fail", "optimize", "find bugs", "code review", "root cause"
- **Anti-trigger keywords:** "write new code", "implement from scratch", "explain how X works in general"
- **Input:** Code, logs, error messages, or system description with a review/debug/optimization request.
- **Output:** Findings with severity classification, root cause analysis, fix proposals, regression assessment.
- **Dependencies:** Follows `docs/review-debug-standards.md` for severity levels and evidence standards.

---

### 6. embedded-automation-design

- **Path:** `skills/embedded-automation-design/SKILL.md`
- **Purpose:** Applies production-grade embedded and automation design principles: non-blocking architecture, state machines, explicit timeouts, watchdog safety, clean layer separation (hardware/driver/transport/logic/app), and ISR discipline.
- **Use when:** Task involves firmware development, RTOS tasks, interrupt handling, hardware abstraction, real-time control, communication protocol implementation, or any embedded system design.
- **Do NOT use when:** Task is pure software with no embedded/hardware/real-time constraints. Task is web development, data science, or desktop application development.
- **Trigger keywords:** "firmware", "embedded", "RTOS", "ISR", "interrupt", "GPIO", "SPI", "I2C", "UART", "timer", "watchdog", "state machine", "non-blocking", "ESP32", "STM32", "PIC", "Arduino", "driver"
- **Anti-trigger keywords:** "web app", "REST API", "database", "frontend", "machine learning model", "cloud service"
- **Input:** Embedded system design task, firmware implementation request, or hardware abstraction design.
- **Output:** Design or implementation following embedded best practices with explicit rationale for each pattern used.
- **Dependencies:** None. Often combined with `architecture-first-solutioning` for larger designs.

---

### 7. skill-scaffolder

- **Path:** `skills/skill-scaffolder/SKILL.md`
- **Purpose:** Creates new skills from the canonical template when no existing skill matches the current task. Ensures the new skill follows all authoring rules, has proper trigger/anti-trigger definitions, and is added to the catalog.
- **Use when:** The agent has checked the catalog, found no matching skill, and needs to create a new one. When explicitly asked to create a new skill.
- **Do NOT use when:** An existing skill already covers the task (even partially — extend it instead). When the need is a one-time rule that fits in `AGENTS.md` or a project overlay.
- **Trigger keywords:** "create a new skill", "no skill matches", "scaffold a skill", "I need a skill for"
- **Anti-trigger keywords:** "use existing skill", "run the review skill", "follow the template"
- **Input:** Description of the task type that needs a new skill.
- **Output:** Complete SKILL.md with all 14 sections, catalog entry, and eval prompts.
- **Dependencies:** `templates/skill-template/SKILL.md`, `docs/skill-authoring-rules.md`.

---

### 8. data-driven-tradeoff-analysis

- **Path:** `skills/data-driven-tradeoff-analysis/SKILL.md`
- **Purpose:** Conducts evidence-based comparison of two or more technical alternatives. For each option, documents rationale, advantages, disadvantages, and conditions where it should not be used. Produces a recommendation with explicit reasoning.
- **Use when:** User asks to compare technologies, frameworks, approaches, or design options. When a technical decision has multiple viable paths and the tradeoffs need structured analysis.
- **Do NOT use when:** The decision is already made and the task is implementation. When comparing non-technical options (business, organizational). When only one option exists.
- **Trigger keywords:** "compare", "which should I use", "tradeoff", "pros and cons", "A vs B", "evaluate options", "which is better"
- **Anti-trigger keywords:** "implement this", "I've already decided", "just use X", "how do I use X"
- **Input:** Two or more technical alternatives to compare, with context about the use case.
- **Output:** Structured comparison matrix with evidence, recommendation, and conditions for each option.
- **Dependencies:** None. May follow `requirement-intake` if the comparison criteria need clarification.
