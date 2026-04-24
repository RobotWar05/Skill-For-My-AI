# Skill Template — Usage Guide

## Purpose

This directory contains the canonical template for creating new skills. It is used by the `skill-scaffolder` skill and can also be used manually.

## Contents

```
skill-template/
├─ SKILL.md        # Template with mandatory YAML frontmatter and all 14 required sections
├─ README.md        # This file
├─ references/      # Place for reference material (datasheets, standards, etc.)
│  └─ .gitkeep
├─ scripts/         # Place for helper scripts (linters, generators, etc.)
│  └─ .gitkeep
└─ assets/          # Place for diagrams, images, etc.
   └─ .gitkeep
```

## How to Use

1. Copy this entire directory to `skills/<your-skill-name>/`.
2. Rename nothing — the `SKILL.md` file must keep its name.
3. Open `SKILL.md` and keep the YAML frontmatter at the very top of the file.
4. Set frontmatter `name` to the exact folder name.
5. Replace frontmatter `description` with a precise trigger description. Many agent loaders use this as the primary trigger signal.
6. Follow the instructions in each section.
7. Delete the instructional comments (in brackets) after filling in real content.
8. Fill ALL 14 sections. No section may be blank or contain placeholder text.
9. After completing:
   - Add a catalog entry to `skills/_catalog/README.md`.
   - Create eval prompts in `evals/prompts/<skill-name>.md`.
   - Run `evals/trigger-checklist.md` against the new skill.

## Quality Checklist

Before considering the skill done:

- [ ] All 14 sections filled with real content (no brackets, no "TBD").
- [ ] `SKILL.md` starts with YAML frontmatter.
- [ ] Frontmatter includes `name` and `description`.
- [ ] Frontmatter `name` exactly matches the skill folder name.
- [ ] Description is specific and distinguishable from all catalog skills.
- [ ] At least 3 positive trigger examples.
- [ ] At least 3 negative trigger examples with alternative skill references.
- [ ] Workflow has ≤ 12 concrete steps.
- [ ] Constraints are MUST/MUST NOT and testable.
- [ ] Anti-hallucination rules are specific to this skill's domain.
- [ ] Adaptation notes explain how to extend without modifying.
- [ ] Catalog entry created.
- [ ] Eval prompts created (≥ 5).
- [ ] Trigger checklist passed.

## References

- `docs/skill-authoring-rules.md` — Quality standards for all sections.
- `docs/naming-and-triggering-guidelines.md` — Naming and trigger design.
- `evals/trigger-checklist.md` — Post-creation validation.
