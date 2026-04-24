# Skill Authoring Rules

This document defines the mandatory standards for writing skills in this repository. Every skill must comply with these rules before being added to the catalog.

---

## 1. Skill File Structure

Every skill must live in its own directory:

```text
skills/<skill-name>/SKILL.md
```

Every `SKILL.md` must start with YAML frontmatter at the very top of the file:

```yaml
---
name: skill-name
description: Use when the agent must perform a specific reusable workflow in a specific context and produce specific behavior.
---
```

Frontmatter requirements:

- `name` is mandatory and must exactly match the skill folder name.
- `description` is mandatory and must be a precise trigger signal for agent loaders.
- The opening `---` must be the first line of the file.
- The closing `---` must appear before the visible skill body.
- Do not put comments, headings, or blank lines before the frontmatter.

The description in frontmatter should match the intent of the DESCRIPTION section. Many agent loaders use it as the primary trigger signal.

---

## 2. Single Responsibility

Each skill must address **exactly one workflow or task type**. If you find yourself writing "and also handles..." — stop. Split it into two skills.

**Test:** Can you describe the skill's purpose in one sentence without using "and"? If not, it's too broad.

---

## 3. Required Sections

After the YAML frontmatter, every `SKILL.md` must contain all 14 sections below, in this order:

| # | Section | Purpose |
|---|---|---|
| 1 | NAME | Canonical skill name (lowercase, hyphenated) |
| 2 | DESCRIPTION | Specific description distinguishing this skill from all others |
| 3 | PURPOSE | Why this skill exists; what problem it solves |
| 4 | USE WHEN | Conditions that should trigger this skill |
| 5 | DO NOT USE WHEN | Conditions that should NOT trigger this skill |
| 6 | EXPECTED INPUTS | What the agent receives when this skill activates |
| 7 | EXPECTED OUTPUTS | What the agent must produce |
| 8 | WORKFLOW | Step-by-step process to follow |
| 9 | CONSTRAINTS | Hard rules the agent must not violate |
| 10 | ANTI-HALLUCINATION RULES | Specific fabrication risks for this skill |
| 11 | POSITIVE TRIGGER EXAMPLES | Prompts/scenarios that SHOULD trigger this skill |
| 12 | NEGATIVE / NON-TRIGGER EXAMPLES | Prompts/scenarios that MUST NOT trigger this skill |
| 13 | ADAPTATION NOTES | How to customize this skill for a specific project |
| 14 | OPTIONAL: REFERENCES / SCRIPTS / ASSETS | Pointers to supporting materials |

**No section may be left blank.** If a section genuinely does not apply, write "Not applicable for this skill — [reason]."

---

## 4. Description Quality

The frontmatter `description` and Section 2 DESCRIPTION are the most important signals for trigger accuracy.

### Must:
- Be specific enough that an agent can distinguish this skill from every other skill in the catalog.
- State the **type of task**, the **context**, and the **expected agent behavior**.
- Use concrete nouns and verbs, not abstract qualifiers.

### Must NOT:
- Use generic wording like "helps with technical tasks" or "improves response quality."
- Use superlatives like "comprehensive" or "advanced" without specifying what that means.
- Overlap significantly with another skill's description.

### Example — Bad:
> "A skill for handling complex engineering problems."

### Example — Good:
> "Enforces a structured intake process for medium-to-large technical requirements: summarizes the request, identifies constraints, lists missing information, and defines the true technical objective before any solution work begins."

---

## 5. Workflow Clarity

The WORKFLOW section must be a numbered list of concrete steps. Each step should be actionable — an agent should be able to follow the workflow mechanically without needing to "interpret" the intent.

### Must:
- Use imperative verbs: "Identify...", "List...", "Verify...", "Output..."
- Define decision points explicitly: "IF [condition] THEN [action] ELSE [action]."
- Specify what to do when information is missing.

### Must NOT:
- Use vague directives like "Consider the implications" or "Think carefully about."
- Leave implicit steps that require domain intuition to fill in.
- Include more than 12 steps. If you need more, the skill is too broad — split it.

---

## 6. Trigger and Anti-Trigger Precision

### Triggers (USE WHEN):
- List specific, observable conditions — not "when appropriate."
- Include keyword patterns the agent can match against.
- Be concrete: "User provides a multi-paragraph problem statement with technical constraints" is better than "user has a complex request."
- Include positive trigger examples in Section 11 for stable behavior.

### Anti-Triggers (DO NOT USE WHEN):
- List conditions where the skill looks like it might apply but should NOT.
- This is the most common source of mis-triggers — invest effort here.
- Include examples of confusable tasks and which skill should handle them instead.
- Include negative trigger examples in Section 12 for stable behavior.

---

## 7. Examples Quality

### Positive Examples:
- Minimum 3 examples.
- Each must be a realistic prompt or scenario, not a contrived toy case.
- Show variation in phrasing and context.

### Negative Examples:
- Minimum 3 examples.
- Each must be a prompt that LOOKS like it could trigger this skill but should NOT.
- State which skill (if any) should handle it instead.

---

## 8. Constraints and Anti-Hallucination

### Constraints:
- Hard rules that override general behavior.
- State them as "MUST" / "MUST NOT" rules.
- Keep them testable: an evaluator should be able to check compliance.

### Anti-Hallucination Rules:
- Identify the specific fabrication risks for this skill's domain.
- For example, a code review skill might say: "Do NOT invent function names that don't exist in the provided code."
- Be specific to the skill — don't just repeat the repo-wide no-fabrication rule.

---

## 9. References and Supporting Materials

- If a skill needs reference material (API docs, standards, checklists), place them in the skill's `references/` subdirectory.
- If a skill uses helper scripts, place them in `scripts/`.
- Keep references as separate files — do NOT inline long reference material into `SKILL.md`.
- References should be factual, sourced, and dated where possible.

---

## 10. Adaptation Notes

Every skill must include notes on how to adapt it for a project-specific context:

- What parts of the workflow might change per project?
- What project-specific constraints typically need to be added?
- What should go in a project overlay vs modifying the skill?

**Rule:** The canonical skill in this repo must NEVER be modified for one project's needs. Adaptations go in project overlays or project-specific skill forks.

---

## 11. Naming

See `docs/naming-and-triggering-guidelines.md` for full naming rules. Summary:

- Lowercase, hyphenated.
- Verb-noun or adjective-noun pattern.
- Maximum 4 words.
- Must be unique across the catalog.
- Must not use generic terms that could apply to multiple skills.
