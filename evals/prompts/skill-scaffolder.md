# Eval Prompts: skill-scaffolder

---

## Prompt 1 — POSITIVE

**Prompt:**
> "I keep having to review database schema designs and there's no skill for it. Create one."

**Expected Behavior:** Agent activates `skill-scaffolder`. Checks catalog (no match). Creates a new `database-schema-review` skill with all 14 sections. Generates catalog entry and eval prompts.

**Pass Criteria:** Complete SKILL.md with all 14 sections filled (no TBD). Catalog entry created. At least 5 eval prompts. Description is specific to database schema review (not generic "database tasks").

---

## Prompt 2 — POSITIVE

**Prompt:**
> "We need a skill for technical documentation writing — structuring READMEs, API docs, and architecture decision records."

**Expected Behavior:** Agent scaffolds a `technical-documentation-authoring` skill. Classifies content correctly: the skill covers the *process* of writing docs (workflow), not the docs themselves.

**Pass Criteria:** Skill name follows naming conventions. USE WHEN and DO NOT USE WHEN are specific. Anti-triggers include "write code" and "review code" with skill references.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "No existing skill covers CI/CD pipeline design for embedded firmware. Scaffold one."

**Expected Behavior:** Agent creates `ci-cd-pipeline-design` skill. Recognizes this is domain-specific (embedded CI/CD is different from web CI/CD) and makes the description specific.

**Pass Criteria:** Description distinguishes embedded CI/CD from web CI/CD. Workflow includes embedded-specific steps (cross-compilation, hardware-in-loop testing).

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "Use the review-debug skill to check this code."

**Expected Behavior:** User is requesting an existing skill. Do NOT scaffold a new one.

**Pass Criteria:** No new skill created. Agent activates `review-debug-deep-mode`.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Add a rule: always use semicolons at end of lines."

**Expected Behavior:** Single rule. Goes in `AGENTS.md` or project overlay. Not a skill.

**Pass Criteria:** No new skill created. Agent recommends adding to `AGENTS.md` or project overlay.

---

## Prompt 6 — NEGATIVE (Boundary)

**Prompt:**
> "The requirement-intake skill doesn't cover hardware procurement specs. Can you fix it?"

**Expected Behavior:** This is a skill modification, not scaffolding. Agent should modify the existing skill or suggest adding adaptation notes.

**Pass Criteria:** No new skill created. Agent proposes extending the existing skill's adaptation notes or creating a project overlay.
