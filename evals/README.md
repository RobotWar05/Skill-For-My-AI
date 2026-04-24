# Evaluation System

## Purpose

This directory contains tools for testing skill trigger accuracy, output quality, and regression after modifications.

## Structure

```
evals/
├─ README.md                # This file
├─ trigger-checklist.md     # Checklist for validating skill descriptions/triggers
├─ regression-process.md    # Process for testing after skill modifications
└─ prompts/                 # Test prompts per skill
   ├─ requirement-intake.md
   ├─ structured-technical-response.md
   ├─ source-first-citation.md
   ├─ architecture-first-solutioning.md
   ├─ review-debug-deep-mode.md
   ├─ embedded-automation-design.md
   └─ skill-scaffolder.md
```

## How to Run Evals

### Manual Evaluation

1. Open the prompt file for the skill you want to test (e.g., `evals/prompts/requirement-intake.md`).
2. Feed each test prompt to the agent with access to the skill repo.
3. For each prompt, verify:
   - **Positive triggers:** The skill activates and the output matches expected behavior.
   - **Negative triggers:** The skill does NOT activate (a different skill or direct answer is used).
4. Record results: PASS / FAIL / PARTIAL with notes.

### After Modifying a Skill

Follow `evals/regression-process.md`:
1. Re-run all existing eval prompts for the modified skill.
2. Test boundary prompts (prompts that are close to the trigger/anti-trigger line).
3. Test prompts from adjacent skills to ensure no new false positives.

## Evaluation Criteria

| Criterion | Definition |
|---|---|
| **Trigger Accuracy** | Skill triggers when it should (true positive) and doesn't when it shouldn't (true negative). |
| **Output Completeness** | All expected output sections are present and filled. |
| **Output Quality** | Content is specific, evidence-based, and actionable — not generic filler. |
| **Constraint Compliance** | All CONSTRAINTS and ANTI-HALLUCINATION RULES are followed. |
| **Format Compliance** | Output follows the skill's defined format/structure. |

## Adding New Eval Prompts

1. Place prompts in `evals/prompts/<skill-name>.md`.
2. Each prompt must include:
   - **Prompt text** — the exact text to feed the agent.
   - **Type** — POSITIVE (should trigger) or NEGATIVE (should not trigger).
   - **Expected behavior** — 1–2 sentences describing what should happen.
   - **Pass/Fail criteria** — how to determine if the test passed.
3. Aim for at least 5 prompts per skill (3 positive, 2 negative minimum).
