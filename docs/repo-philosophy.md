# Repository Philosophy

## Why This Repo Exists

This repository is the **canonical source of truth** for how AI agents should work with us. It exists to solve three problems:

1. **Inconsistency** — Without a shared rule base, every conversation with an AI agent starts from zero. The agent has no memory of our standards, preferences, or quality expectations.
2. **Prompt fragmentation** — Rules scattered across individual prompts lead to contradictions, gaps, and "vibe coding" where quality depends on how well the prompt was written that day.
3. **Non-reusability** — Without structured skills, good workflows discovered in one project die with that project's conversation history.

This repo replaces ad-hoc prompts with a **structured, versioned, testable** system.

---

## Repo-Wide Rules vs Skill-Level Rules

The repository uses a layered architecture for rules:

### Layer 1: `AGENTS.md` (Repo-Wide Rules)

- **Always active**, regardless of the current task.
- Contains principles that apply universally: no fabrication, assumption tracking, context-first, response structure, embedded defaults.
- **Short and hard.** An agent should be able to internalize these in one read.
- Think of this as the "constitution" — it doesn't change often, and everything else must be compatible with it.

### Layer 2: `docs/` (Deep Documentation)

- Contains the **reasoning behind** the rules.
- Agents read these when they need to understand *why* a rule exists, not just *what* it says.
- Also contains procedural guides (how to adapt, how to author, how to review).
- Think of this as the "legislative history" — it informs interpretation but isn't read on every task.

### Layer 3: `skills/` (Skill-Level Rules)

- Each skill is a **self-contained workflow** for a specific type of task.
- Skill rules only activate when the skill is triggered.
- Skills contain their own constraints, anti-hallucination rules, and examples.
- Think of these as "specialized procedures" — you follow the one that matches your situation.

### Layer 4: Project Overlays (External)

- **Not stored in this repo.** Stored in the project's own repo.
- Contains project-specific board details, file paths, toolchains, vendor constraints.
- References canonical skills by name and adds project context.
- Think of these as "local ordinances" — they extend the base rules for a specific jurisdiction.

---

## Why Not One Long Prompt?

A single monolithic prompt fails in multiple ways:

| Problem | Monolithic Prompt | This Repo |
|---|---|---|
| **Context window** | Hits token limits; forces truncation | Agent reads only what's needed for the current task |
| **Maintenance** | Editing one section risks breaking others | Each skill is independently editable and testable |
| **Testing** | No way to verify which rule triggered | Each skill has dedicated eval prompts |
| **Reuse** | Copy-paste across projects; diverges quickly | Single source of truth; projects reference, not copy |
| **Onboarding** | New agent must parse everything at once | Agent reads `AGENTS.md` → catalog → relevant skill |
| **Evolution** | Hard to version; hard to diff | Standard versioning with CHANGELOG |

---

## Design Principles Summary

1. **Accuracy over speed.** Never fabricate to fill gaps. Say what you don't know.
2. **Structure over intuition.** Follow defined workflows, not "feels right."
3. **Specificity over generality.** Vague descriptions cause mis-triggers. Be precise.
4. **Separation of concerns.** Repo-wide rules ≠ skill rules ≠ project rules.
5. **Testability.** If you can't test whether a skill triggers correctly, it's not well-defined.
6. **Stability.** Canonical skills don't change for one project. Extend, don't modify.
