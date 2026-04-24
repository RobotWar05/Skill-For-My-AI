# Contributing to the Canonical AI Agent Skills Repository

## Overview

This repository contains reusable, production-grade AI agent skills. Contributions must maintain the quality bar established in `docs/skill-authoring-rules.md`.

---

## How to Add a New Skill

1. **Check the catalog** (`skills/_catalog/README.md`) to confirm no existing skill covers the same task.
2. **Copy the template** from `templates/skill-template/` into `skills/<your-skill-name>/`.
3. **Fill in all 14 sections** of `SKILL.md`. No section may be left blank or filled with placeholder text.
4. **Write eval prompts** — at least 5 test prompts (mix of positive and negative triggers) in `evals/prompts/<your-skill-name>.md`.
5. **Update the catalog** — add your skill to `skills/_catalog/README.md` with all required fields.
6. **Run the trigger checklist** (`evals/trigger-checklist.md`) against your new skill.
7. **Submit a PR** with a clear description of:
   - What task the skill addresses.
   - Why no existing skill covers it.
   - How you verified trigger/anti-trigger accuracy.

---

## How to Modify an Existing Skill

1. **State the problem** — what is wrong with the current skill? Mis-triggering? Missing workflow step? Incorrect constraint?
2. **Make the change** in the skill's `SKILL.md`.
3. **Run regression** — follow `evals/regression-process.md`:
   - Re-run all existing eval prompts for the skill.
   - Test boundary prompts that could be affected.
   - Test prompts that should NOT trigger the skill.
4. **Update the catalog** if trigger keywords, anti-triggers, or maturity level changed.
5. **Update CHANGELOG.md** with a clear description of the change.

---

## How to Add Eval Prompts

1. Place new prompts in `evals/prompts/<skill-name>.md`.
2. Each prompt must include:
   - The test prompt text.
   - Whether it is a positive or negative trigger test.
   - Expected behavior (1–2 sentences).
   - Pass/fail criteria.
3. Ensure no duplicate prompts.

---

## Quality Standards

- **No generic descriptions.** Every skill description must be specific enough to distinguish it from all other skills.
- **No fabrication.** Do not invent APIs, tools, commands, or test results in skill workflows or examples.
- **No mega-skills.** If a skill tries to do more than one distinct workflow, split it.
- **No project-specific content** in canonical skills. Use project overlays instead.
- **All assumptions labeled.** Any assumed behavior must be tagged `ASSUMPTION`.

---

## Commit Message Format

```
<type>(<scope>): <description>

Types: feat, fix, refactor, docs, eval, chore
Scope: skill name, docs, evals, templates, root
```

Examples:
```
feat(embedded-automation-design): add RTOS task priority guidelines
fix(requirement-intake): clarify anti-trigger for simple Q&A
docs(skill-authoring-rules): add section on reference file management
eval(review-debug-deep-mode): add edge case prompts for performance bugs
```

---

## Versioning

- **PATCH** (0.1.x): Typo fixes, clarifications, new eval prompts.
- **MINOR** (0.x.0): New skills, significant skill rewrites, new documentation.
- **MAJOR** (x.0.0): Breaking changes to AGENTS.md rules, skill format changes, catalog schema changes.
