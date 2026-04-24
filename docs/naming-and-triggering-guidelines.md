# Naming and Triggering Guidelines

This document defines how to name skills, write descriptions, design triggers, and avoid trigger conflicts.

---

## Skill Naming Rules

### Format
- **Lowercase, hyphenated.**
- **Verb-noun** or **adjective-noun** pattern.
- **Maximum 4 words.**

### Examples

| Good | Bad | Why Bad |
|---|---|---|
| `requirement-intake` | `requirements` | Too vague; noun-only |
| `review-debug-deep-mode` | `code-helper` | Too generic |
| `embedded-automation-design` | `embedded` | Doesn't specify the action |
| `source-first-citation` | `citation-and-source-management-tool` | Too long |
| `data-driven-tradeoff-analysis` | `analysis` | Could mean anything |

### Uniqueness
- Every skill name must be unique across the entire catalog.
- Before naming a new skill, check `skills/_catalog/README.md` for conflicts.
- If two names feel too similar, that's a signal the skills might overlap — investigate before proceeding.

---

## Description Writing

The DESCRIPTION field in `SKILL.md` is the primary text agents use to decide whether to trigger a skill. It must be written with precision.

### Formula

A good description follows this pattern:

> "[Action verb] a [specific process] for [specific context]: [list of concrete behaviors]."

### Checklist

- [ ] Does the description specify the **type of task**? (not just "technical tasks")
- [ ] Does the description specify the **context**? (when does this task arise?)
- [ ] Does the description list **concrete behaviors**? (what the agent actually does)
- [ ] Is the description **distinguishable** from every other skill's description?
- [ ] Is the description **under 3 sentences**?

### Examples

**Bad:**
> "Helps with software engineering problems."

- No task type specified.
- No context specified.
- No behaviors listed.
- Matches half the catalog.

**Good:**
> "Enforces a structured intake process for medium-to-large technical requirements: summarizes the request, identifies constraints, lists missing information, and defines the true technical objective before any solution work begins."

- Task type: requirement intake.
- Context: medium-to-large requirements.
- Behaviors: summarize, identify, list, define.
- Distinguishable: no other skill does intake-before-solution.

---

## Trigger Design

### USE WHEN (Positive Triggers)

Write triggers as **observable conditions**, not subjective assessments.

| Good Trigger | Bad Trigger |
|---|---|
| "User provides a multi-paragraph problem statement" | "User has a complex problem" |
| "User asks to review or debug existing code" | "Code needs improvement" |
| "User asks to compare two or more technical approaches" | "User needs help deciding" |
| "Task involves embedded firmware with real-time constraints" | "Embedded project" |

### Keywords
- List 5–10 keywords or phrases that commonly appear in prompts that should trigger this skill.
- Be specific: "review this code" is better than "code."

---

## Anti-Trigger Design

### DO NOT USE WHEN (Negative Triggers)

Anti-triggers prevent false activations. They are the most important defense against mis-triggers.

### Strategy

For each skill, ask:
1. What tasks **look similar** but are actually different?
2. Which **other skill** should handle those tasks?
3. What **keywords might overlap** with another skill?

### Format

Each anti-trigger should specify:
- The condition that should NOT trigger this skill.
- Which skill (if any) should handle it instead.

Example:
> "User asks a quick factual question with no ambiguity or missing requirements → this is a direct answer, not a requirement intake. Do not trigger."

---

## Resolving Trigger Overlap

When two skills have overlapping triggers, follow this resolution process:

### Step 1: Identify the Overlap
- Which prompts trigger both skills?
- Are the overlapping prompts genuinely ambiguous, or is one skill clearly more appropriate?

### Step 2: Sharpen Descriptions
- Revise both skills' DESCRIPTION sections to be more specific.
- Add distinguishing keywords.

### Step 3: Add Cross-References in Anti-Triggers
- In Skill A's anti-trigger: "If the task is [specific condition], use Skill B instead."
- In Skill B's anti-trigger: "If the task is [specific condition], use Skill A instead."

### Step 4: Add Eval Prompts
- Create test prompts specifically designed to test the boundary between the two skills.
- Add these to both skills' eval prompt files.

### Step 5: Update Catalog
- Ensure the catalog's trigger/anti-trigger keywords reflect the changes.

---

## Common Trigger Pitfalls

| Pitfall | Example | Fix |
|---|---|---|
| Trigger too broad | "Use when user has a technical question" | Specify the task type and context |
| No anti-triggers | Skill has USE WHEN but no DO NOT USE WHEN | Add anti-triggers for confusable tasks |
| Keyword overlap | Two skills both trigger on "architecture" | Add qualifiers: "architecture analysis before implementation" vs "architecture review of existing system" |
| Subjective trigger | "Use when the problem is complex" | Replace with observable: "Use when the problem involves 3+ interacting components" |
| Missing cross-reference | Anti-trigger says "don't use here" but doesn't say what to use instead | Always point to the alternative skill |
