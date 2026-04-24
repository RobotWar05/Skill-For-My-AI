# AGENTS.md — Repo-Wide Rules for All AI Agents

> **Read this file FIRST before doing any work in this repository.**
> These rules are always active, regardless of which skill or task you are executing.

---

## 1. CATALOG FIRST

Before inventing a new workflow, writing ad-hoc logic, or generating a response from scratch:

1. Read `skills/_catalog/README.md`.
2. Check if an existing skill matches the current task.
3. If a match exists, follow that skill's `SKILL.md` workflow exactly.
4. If no match exists, proceed to Rule 2.

**Do NOT skip this step. Do NOT assume no skill applies without checking the catalog.**

---

## 2. SCAFFOLD, DON'T IMPROVISE

If no existing skill fits the task:

1. Use the `skill-scaffolder` skill (see `skills/skill-scaffolder/SKILL.md`).
2. Use the template at `templates/skill-template/SKILL.md` as the structural base.
3. Generate a new skill with all 14 required sections (see `docs/skill-authoring-rules.md`).
4. Place the new skill in `skills/<skill-name>/SKILL.md`.
5. Update `skills/_catalog/README.md` with the new entry.

**Do NOT create partial or "placeholder" skills. Every skill must be immediately usable.**

---

## 3. ASSUMPTION TRACKING

Every assumption you make must be:

- Explicitly labeled as `ASSUMPTION` in your output.
- Accompanied by the reasoning behind the assumption.
- Flagged for user confirmation when the assumption affects architecture, safety, or correctness.

**Distinguish clearly between:**
- **FACT**: Verified from provided sources, documentation, or code.
- **INFERENCE**: Logically derived from available facts.
- **ASSUMPTION**: Not verified; requires confirmation.

---

## 4. NO FABRICATION

You must NEVER fabricate:

- API endpoints, function signatures, or library behavior
- CLI commands or tool capabilities
- File paths, directory structures, or configuration formats
- Test results, benchmarks, or performance data
- Hardware specifications or register maps
- Dependencies or version compatibility claims

If you lack information:
- State what you don't know.
- State what you would need to verify.
- Provide your best inference clearly labeled as such.

---

## 5. CONTEXT FIRST

When the user provides files, code, logs, documentation, or system descriptions:

- Use those sources as primary evidence before external knowledge.
- Cite specific files, modules, functions, and line numbers when possible.
- Use external references only when user-provided context is insufficient.

---

## 6. RESPONSE STRUCTURE

For non-trivial technical responses, default to this structure:

1. **SUMMARY OF REQUEST** — What was asked.
2. **ANALYSIS / ARCHITECTURE** — Technical breakdown.
3. **RESULT / SOLUTION** — Concrete answer or implementation.
4. **ADDITIONAL RECOMMENDATIONS** — What else to consider.

Skip sections only when the task is genuinely trivial (e.g., a single-line fix).

---

## 7. EMBEDDED / AUTOMATION DEFAULTS

When working on embedded systems, automation, or real-time contexts, default to:

- Non-blocking design patterns
- Explicit state machines
- Defined timeouts on all waits
- Watchdog-safe operation
- Short ISR handlers (defer work to main loop / task)
- Clear separation: hardware → driver → transport → logic → application

Default AGAINST:
- `delay()` blocking calls
- Infinite `while` loops without exit conditions
- Heavy processing inside ISRs
- Unconstrained dynamic memory allocation
- Hidden inter-module dependencies

---

## 8. HONEST TECHNICAL FEEDBACK

- If the user's approach has flaws, state them directly.
- Explain why it's a problem in concrete terms.
- Suggest a better approach.
- Do not soften technical feedback for politeness.
- The goal is technical progress, not comfort.

---

## 9. REPO INTEGRITY

- Do NOT modify existing skills to fit a single project's needs. Create project overlays or project-specific skills instead.
- Do NOT add project-specific file paths, board pinouts, vendor commands, or hardware details to the canonical skills.
- Treat this repo as a **shared base**. Project specifics live outside or in clearly marked overlays.

---

## 10. FILE REFERENCE QUICK MAP

| What you need | Where to find it |
|---|---|
| Skill catalog | `skills/_catalog/README.md` |
| Skill authoring rules | `docs/skill-authoring-rules.md` |
| New skill template | `templates/skill-template/SKILL.md` |
| Scaffolding workflow | `skills/skill-scaffolder/SKILL.md` |
| Project overlay template | `templates/project-overlay-template.md` |
| Adaptation workflow | `docs/adaptation-workflow.md` |
| Evaluation prompts | `evals/prompts/` |
| Repo philosophy | `docs/repo-philosophy.md` |
