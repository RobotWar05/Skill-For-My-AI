# Regression Process

Follow this process after every skill modification to ensure the change doesn't break existing behavior.

---

## When to Run Regression

- After modifying any section of a SKILL.md.
- After modifying AGENTS.md rules that affect skill behavior.
- After modifying docs that skills reference (e.g., `review-debug-standards.md`).
- After adding a new skill that may overlap with existing ones.

---

## Regression Steps

### Step 1: Re-run Existing Eval Prompts

1. Open `evals/prompts/<modified-skill-name>.md`.
2. Feed EVERY prompt to the agent.
3. Verify each prompt still produces the expected behavior.
4. Record results: PASS / FAIL / CHANGED (behavior changed but may be acceptable).

### Step 2: Test Boundary Prompts

Create and test prompts that sit on the boundary between:
- Triggering the modified skill and NOT triggering it.
- Triggering the modified skill and triggering an adjacent skill.

For each boundary prompt:
- State which skill should trigger.
- Verify the correct skill triggers.
- If the wrong skill triggers, the modification introduced a regression.

### Step 3: Test Adjacent Skills

For each skill that is "adjacent" (similar triggers or related domain):
1. Run that skill's eval prompts.
2. Verify the modification didn't cause the adjacent skill to mis-trigger or stop triggering.

### Step 4: Check Catalog Consistency

1. Open `skills/_catalog/README.md`.
2. Verify the modified skill's catalog entry matches its current SKILL.md.
3. If triggers, anti-triggers, or description changed, update the catalog.

### Step 5: Document Results

Record in the PR or commit message:
- Number of prompts tested.
- Number of PASS / FAIL / CHANGED results.
- Any boundary issues discovered.
- Any catalog updates made.

---

## Regression Severity

| Result | Meaning | Action |
|---|---|---|
| All PASS | No regression detected | Proceed with the change |
| CHANGED (acceptable) | Behavior changed but is correct/improved | Document the change; update eval expectations |
| FAIL (false positive) | Skill triggers when it shouldn't | Fix the trigger/description; re-test |
| FAIL (false negative) | Skill doesn't trigger when it should | Fix the trigger/description; re-test |
| FAIL (output quality) | Skill triggers correctly but output is wrong | Fix the workflow/constraints; re-test |

---

## Quick Regression Checklist

- [ ] All existing eval prompts for the modified skill: PASS
- [ ] At least 2 boundary prompts tested: PASS
- [ ] Adjacent skills' eval prompts: PASS
- [ ] Catalog entry updated if needed
- [ ] CHANGELOG updated
- [ ] Results documented
