---
name: coding-agent-discipline
description: Use when an AI coding agent is about to modify code, refactor files, or implement a change and must first define success criteria, keep changes surgical, avoid over-engineering, preserve unrelated code, and state assumptions explicitly.
---

# SKILL: coding-agent-discipline

---

## 1. NAME

`coding-agent-discipline`

---

## 2. DESCRIPTION

Enforces disciplined behavior before and during AI-assisted code changes: define success criteria, keep edits focused, avoid speculative abstractions, preserve unrelated code, state assumptions, and verify the result. This skill prevents over-engineered rewrites, drive-by refactors, and hidden assumptions during implementation work.

---

## 3. PURPOSE

AI coding agents often fail by making silent assumptions, touching unrelated files, adding unnecessary abstractions, or declaring completion without verification. This skill exists to:

- Convert implementation requests into verifiable goals.
- Keep changes limited to what the user asked for.
- Prevent broad rewrites when a surgical patch is enough.
- Surface assumptions before they affect correctness.
- Require a verification path before considering the work complete.

---

## 4. USE WHEN

- User asks the agent to implement, patch, refactor, or modify code.
- User asks for a bug fix that will require editing code.
- User asks to add a feature, update behavior, or change existing implementation.
- The task involves touching files in a codebase.
- The agent is about to make code changes after using another skill such as `architecture-first-solutioning` or `review-debug-deep-mode`.

---

## 5. DO NOT USE WHEN

- User asks only for an explanation with no code changes.
- User asks only for a code review and does not want edits; use `review-debug-deep-mode`.
- User asks to compare technical options; use `data-driven-tradeoff-analysis`.
- User asks for requirements clarification before implementation; use `requirement-intake`.
- User asks to create a new skill; use `skill-scaffolder`.

---

## 6. EXPECTED INPUTS

- User request describing a desired code change.
- Existing files, code snippets, tests, logs, or repository context.
- Optional constraints such as "minimal change", "no refactor", "preserve API", or "do not touch unrelated files."

---

## 7. EXPECTED OUTPUTS

The agent must produce or internally apply:

1. **Success criteria**: what must be true when the change is complete.
2. **Assumptions**: explicit `ASSUMPTION` labels for unverified conditions that affect correctness.
3. **Surgical plan**: the smallest reasonable file and behavior scope.
4. **Implementation**: focused edits that trace directly to the request.
5. **Verification**: tests, static checks, manual inspection, or a clear statement when verification could not be run.

---

## 8. WORKFLOW

1. **Restate the coding goal.** Convert the request into a concrete outcome.
2. **Define success criteria.** State how completion will be verified.
3. **Inspect before editing.** Read relevant files and existing patterns before proposing changes.
4. **State assumptions.** Label every unverified condition that affects correctness as `ASSUMPTION`.
5. **Choose the smallest change.** Prefer the least invasive patch that satisfies the success criteria.
6. **Avoid speculative design.** Do not add abstractions, configuration, dependencies, or features not required by the task.
7. **Preserve unrelated code.** Do not refactor, reformat, rename, or delete unrelated code.
8. **Edit surgically.** Every changed line must connect to the requested outcome or cleanup caused by the change.
9. **Verify.** Run the relevant available check or explain why verification could not be performed.
10. **Report honestly.** Summarize changed behavior, verification result, assumptions, and remaining risk.

---

## 9. CONSTRAINTS

- MUST define success criteria before substantial edits.
- MUST inspect relevant existing code before modifying it.
- MUST keep changes scoped to the user's request.
- MUST NOT rewrite working systems without a concrete reason tied to the task.
- MUST NOT add speculative abstractions, dependencies, configuration, or features.
- MUST NOT modify unrelated files for cleanup, style, or preference.
- MUST state verification performed or explicitly state that verification was not run.
- MUST label assumptions as `ASSUMPTION` when they affect correctness.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT claim tests passed unless they were actually run.
- Do NOT invent repository conventions; verify them from existing files.
- Do NOT assume an API, framework behavior, or command exists without local evidence or documentation.
- Do NOT describe unrelated files as changed if they were not modified.
- Do NOT claim a broad refactor is necessary unless the inspected code proves the smaller change cannot work.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Implement the new validation behavior in this module, but keep the diff small."
2. "Refactor this function without changing behavior and make sure the tests still pass."
3. "Fix this bug in the parser. Do not touch unrelated code."
4. "Add support for this flag in the CLI and update only the necessary files."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "Explain how this parser works." -> Use `structured-technical-response` or answer directly.
2. "Review this code for bugs, but do not edit anything." -> Use `review-debug-deep-mode`.
3. "Should we use Rust or Go for this tool?" -> Use `data-driven-tradeoff-analysis`.
4. "I need a skill for database migration reviews." -> Use `skill-scaffolder`.

---

## 13. ADAPTATION NOTES

- Project overlays may add project-specific success criteria such as required test commands, lint commands, API compatibility rules, or branch policies.
- Canonical skill content must stay vendor-agnostic and must not include app-specific build commands or project-specific file paths.
- For high-risk projects, overlays may require tests before and after refactors, approval before touching generated files, or stronger rollback plans.
- If a project has generated code, vendored code, or migration files, define those edit boundaries in the project overlay rather than modifying this canonical skill.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `AGENTS.md` repo integrity, no-fabrication, context-first, and data-driven recommendation rules.
- Reference: `docs/attribution-policy.md` for external inspiration and adaptation guidance.
- No scripts or assets required for this skill.
