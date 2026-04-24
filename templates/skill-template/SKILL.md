---
name: skill-name-here
description: Use when the agent must perform a specific reusable workflow. Replace this with a precise trigger description that states the task type, context, and expected behavior.
---

# SKILL: [skill-name-here]

> **Instructions:** Copy this template to `skills/<your-skill-name>/SKILL.md`.
> Fill every section. Do not leave placeholders. Do not write "TBD."
> The YAML frontmatter above is mandatory and must remain at the very top of every skill.
> Refer to `docs/skill-authoring-rules.md` for quality standards.
> After completing, run `evals/trigger-checklist.md` against this skill.

---

## 1. NAME

`[lowercase-hyphenated-name]`

---

## 2. DESCRIPTION

[Write a specific description that distinguishes this skill from all others in the catalog.
Follow the formula: "[Action verb] a [specific process] for [specific context]: [list of concrete behaviors]."
Must be under 3 sentences. Must specify task type, context, and expected agent behavior.
Do NOT use generic wording like "helps with technical tasks."]

---

## 3. PURPOSE

[Explain why this skill exists. What problem does it solve? What happens without it?
Be concrete — "prevents X" is better than "improves quality."]

---

## 4. USE WHEN

[List specific, observable conditions that should trigger this skill.
- Each condition must be concrete and testable.
- Include keyword patterns agents can match against.
- Example: "User provides a multi-paragraph problem statement with technical constraints."]

---

## 5. DO NOT USE WHEN

[List conditions where this skill looks like it might apply but should NOT.
- For each anti-trigger, state which skill should handle it instead.
- This section prevents mis-triggers — invest serious effort here.
- Example: "User asks a quick factual question → answer directly, no skill needed."]

---

## 6. EXPECTED INPUTS

[What does the agent receive when this skill activates?
- User-provided materials (code, logs, docs)?
- A specific type of question or request?
- Optional additional context?]

---

## 7. EXPECTED OUTPUTS

[What must the agent produce?
- Specific sections or format?
- Structured document or inline response?
- Code, configuration, or analysis?
Be precise — an evaluator should be able to check compliance.]

---

## 8. WORKFLOW

[Numbered list of concrete steps. Each step must be actionable with imperative verbs.
- Maximum 12 steps. If you need more, the skill is too broad — split it.
- Define decision points: "IF [condition] THEN [action] ELSE [action]."
- Specify what to do when information is missing.
Do NOT use vague directives like "consider" or "think about."]

1. **[Step name].** [Action description.]
2. **[Step name].** [Action description.]
3. ...

---

## 9. CONSTRAINTS

[Hard rules the agent must not violate during this skill's execution.
- State as MUST / MUST NOT rules.
- Each must be testable — an evaluator should be able to check compliance.
- Example: "MUST NOT propose solutions during intake."]

---

## 10. ANTI-HALLUCINATION RULES

[Specific fabrication risks for THIS skill's domain.
- Do NOT just repeat the repo-wide no-fabrication rule.
- Identify what an agent is most likely to fabricate when executing this skill.
- Example for a code review skill: "Do NOT invent function names that don't exist in the provided code."]

---

## 11. POSITIVE TRIGGER EXAMPLES

[Minimum 3 realistic prompts or scenarios that SHOULD trigger this skill.
Show variation in phrasing and context.]

1. "[Example prompt 1]"
2. "[Example prompt 2]"
3. "[Example prompt 3]"

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

[Minimum 3 prompts that LOOK like they could trigger this skill but MUST NOT.
State which skill should handle each instead.]

1. "[Example prompt]" → [Which skill instead, or "answer directly"]
2. "[Example prompt]" → [Which skill instead]
3. "[Example prompt]" → [Which skill instead]

---

## 13. ADAPTATION NOTES

[How to customize this skill for a specific project.
- What parts of the workflow might change?
- What project-specific constraints typically need to be added?
- What should go in a project overlay vs modifying the skill?
- Rule: canonical skill must NEVER be modified for one project. Use overlays.]

---

## 14. REFERENCES / SCRIPTS / ASSETS

[Pointers to supporting materials, if any.
- References: documentation, standards, checklists in `references/` subdirectory.
- Scripts: helper scripts in `scripts/` subdirectory.
- Assets: diagrams, images in `assets/` subdirectory.
- If none: "No references, scripts, or assets required for this skill."]
