# When to Use: Skill vs AGENTS.md vs Project Overlay vs Docs

This document clarifies where different types of rules and information should live.

---

## Decision Matrix

| Type of Content | Where It Goes | Example |
|---|---|---|
| Rule that applies to EVERY task, always | `AGENTS.md` | "Never fabricate API endpoints" |
| Rule that applies to a SPECIFIC type of task | `skills/<name>/SKILL.md` | "When reviewing code, check for race conditions" |
| Rule that applies to a SPECIFIC project | Project overlay (in project repo) | "This project uses STM32F4; ISR latency budget is 5μs" |
| Explanation of WHY a rule exists | `docs/` | "Why we default to non-blocking design" |
| Reference material (datasheets, standards) | `skills/<name>/references/` or `docs/` | "MISRA C compliance checklist" |
| Template for creating new content | `templates/` | "Skill template with all 14 sections" |
| Test prompts for verifying skill behavior | `evals/prompts/` | "Test that review-debug triggers on code review requests" |

---

## Detailed Guidelines

### Put in `AGENTS.md` if:

- It applies to **every task** without exception.
- It's a **hard constraint** (must/must not), not a suggestion.
- It's **short enough** to include without bloating the file.
- Removing it would allow the agent to produce harmful output (fabrication, assumption masking, etc.).

**Examples of AGENTS.md content:**
- No fabrication rule.
- Assumption labeling requirement.
- Default response structure.
- Embedded/automation defaults.
- Catalog-first rule.

**Do NOT put in AGENTS.md:**
- Detailed workflows (→ skill).
- Step-by-step procedures (→ skill).
- Explanations and rationale (→ docs).
- Project-specific constraints (→ project overlay).

---

### Put in a Skill if:

- It's a **complete workflow** for a specific type of task.
- It has **clear trigger conditions** — you can define when it activates and when it doesn't.
- It's **reusable** across multiple projects.
- It has **enough substance** to warrant its own file (not just a one-line rule).

**Examples of skill content:**
- How to conduct a structured requirement intake.
- How to perform a deep code review with severity classification.
- How to analyze architecture before writing code.

**Do NOT make a skill for:**
- A single rule that fits in `AGENTS.md` (→ `AGENTS.md`).
- Project-specific procedures (→ project overlay or project-specific skill).
- Reference material without workflow (→ `docs/` or `references/`).

---

### Put in a Project Overlay if:

- It's **specific to one project** (hardware, toolchain, repo structure, team conventions).
- It **extends** canonical skills with project context.
- It would be **incorrect or misleading** if applied to a different project.

**Examples of project overlay content:**
- "This project targets ESP32-S3 with FreeRTOS. Stack size minimum: 4096 bytes."
- "Source code is in `src/`, tests in `test/`, CI uses GitHub Actions."
- "Use the `embedded-automation-design` skill with these additional constraints: [...]."
- "Pin mapping: IN1=GPIO8, IN2=GPIO9, IN3=GPIO10, IN4=GPIO11."

**The project overlay lives in the project repo, NOT in this canonical repo.**

---

### Put in Docs if:

- It **explains the reasoning** behind rules or design decisions.
- It's a **procedural guide** that supports multiple skills or repo-wide processes.
- It's **reference material** not tied to a specific skill's workflow.

**Examples of docs content:**
- Why this repo uses layered rules.
- How to name and trigger skills.
- Review and debug quality standards.
- Adaptation workflow for new projects.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---|---|---|
| Putting project pin mappings in a canonical skill | Wrong for every other project | Move to project overlay |
| Putting a full workflow in `AGENTS.md` | Makes AGENTS.md too long; not always relevant | Create a skill |
| Putting a one-line rule in a skill | Overhead of 14 sections for one rule | Add to `AGENTS.md` |
| Putting rationale in `AGENTS.md` | Makes it harder to read quickly | Move explanation to `docs/`; keep only the rule in `AGENTS.md` |
| Duplicating rules across skill and `AGENTS.md` | Maintenance burden; risk of divergence | Reference `AGENTS.md` from skill; don't repeat |
