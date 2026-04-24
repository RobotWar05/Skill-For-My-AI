# Adaptation Workflow

This document describes the complete process for adapting this canonical skill repository to a new project or workflow.

---

## Overview

When starting a new project, the agent should NOT invent workflows from scratch. Instead, it follows this process:

```
Read AGENTS.md → Read Catalog → Select Skills → Create Project Overlay → Work
```

If the catalog lacks a needed skill:

```
Read AGENTS.md → Read Catalog → No Match → Use Skill Scaffolder → Create Skill → Update Catalog → Create Project Overlay → Work
```

---

## Step-by-Step Process

### Step 1: Read `AGENTS.md`

- Internalize the repo-wide rules.
- These rules are ALWAYS active, regardless of the project.
- Pay special attention to: no-fabrication, assumption tracking, context-first, response structure.

### Step 2: Read the Skill Catalog

- Open `skills/_catalog/README.md`.
- For each skill, check:
  - Does the skill's "USE WHEN" match tasks I expect in this project?
  - Does the skill's "DO NOT USE WHEN" exclude this project's context?
- Make a list of relevant skills.

### Step 3: Identify Gaps

- List the types of tasks expected in the project.
- For each task type, confirm a skill exists.
- If no skill matches, flag it as a gap.

### Step 4: Fill Gaps (If Needed)

For each gap:

1. Read `skills/skill-scaffolder/SKILL.md`.
2. Copy `templates/skill-template/` to `skills/<new-skill-name>/`.
3. Fill all 14 sections following `docs/skill-authoring-rules.md`.
4. Create eval prompts in `evals/prompts/<new-skill-name>.md`.
5. Add the new skill to `skills/_catalog/README.md`.

**Decision point:** Is the new skill project-specific or reusable?
- If **reusable** across projects → add to this canonical repo.
- If **project-specific** → create it in the project repo, not here.

### Step 5: Create a Project Overlay

Use `templates/project-overlay-template.md` as the base. The overlay must contain:

1. **Project Identity** — name, platform, toolchain, repository location.
2. **Active Skills** — list of canonical skills to use, with any project-specific adjustments.
3. **Project Constraints** — hardware specs, timing budgets, memory limits, API contracts.
4. **Project-Specific Skills** — skills created only for this project (if any).
5. **File Map** — where source code, tests, docs, and configs live in the project repo.
6. **Assumptions** — all assumptions about the project, labeled as such.

**Place the overlay in the project repo, NOT in this canonical repo.**

### Step 6: Record Assumptions

Every assumption made during adaptation must be:

- Labeled `ASSUMPTION` explicitly.
- Accompanied by reasoning.
- Flagged for user confirmation if it affects architecture or safety.

### Step 7: Begin Work

The agent now operates with:

- `AGENTS.md` as the always-on rule layer.
- Selected canonical skills as the workflow layer.
- Project overlay as the context layer.

---

## Rules for Adaptation

### DO:
- Reference canonical skills by name in the project overlay.
- Add project-specific constraints as extensions, not modifications.
- Create project-specific skills when the canonical set doesn't cover a project-unique workflow.
- Keep the project overlay up to date as the project evolves.

### DO NOT:
- Modify canonical skills to fit one project.
- Copy canonical skills into the project repo and edit them (this breaks the single-source-of-truth principle).
- Add project-specific file paths, hardware details, or vendor commands to canonical skills.
- Skip reading the catalog and invent workflows ad-hoc.

---

## Example Adaptation Flow

See `examples/example-project-adaptation.md` for a complete worked example using an ESP32-based IoT project.
