# Trigger Checklist

Use this checklist to validate a skill's description and trigger/anti-trigger definitions. Run this after creating a new skill or modifying an existing one.

---

## Description Quality

- [ ] **Specificity:** Does the description specify the exact task type? (not "technical tasks")
- [ ] **Context:** Does the description specify when this task arises?
- [ ] **Behaviors:** Does the description list what the agent concretely does?
- [ ] **Distinguishability:** Can you tell this skill apart from EVERY other skill by description alone?
- [ ] **Length:** Is the description under 3 sentences?
- [ ] **No generic wording:** Does it avoid phrases like "helps with", "improves", "comprehensive"?

## Trigger Accuracy

- [ ] **Observable conditions:** Are USE WHEN triggers based on observable facts (not subjective assessments)?
- [ ] **Keyword coverage:** Are 5–10 trigger keywords listed?
- [ ] **No subjective triggers:** No triggers like "when the problem is complex" (replace with observable criteria)?
- [ ] **Testable:** Can you write a prompt that definitively triggers or doesn't trigger this skill?

## Anti-Trigger Accuracy

- [ ] **Coverage:** Are DO NOT USE WHEN conditions listed for all confusable task types?
- [ ] **Cross-references:** Does each anti-trigger specify which skill should handle the task instead?
- [ ] **Boundary cases:** Are the boundaries between this skill and adjacent skills explicitly defined?
- [ ] **Keyword exclusions:** Are anti-trigger keywords listed?

## Overlap Check

- [ ] **Catalog review:** Compared this skill's triggers against ALL other skills in the catalog?
- [ ] **No overlapping triggers:** No other skill has the same USE WHEN conditions?
- [ ] **Clear boundaries:** If two skills have related triggers, are the boundaries documented in both skills' anti-triggers?
- [ ] **Boundary prompts:** Created eval prompts that test the boundary between this skill and its closest neighbors?

## Examples Quality

- [ ] **Positive examples:** At least 3 realistic positive trigger examples?
- [ ] **Negative examples:** At least 3 realistic negative trigger examples?
- [ ] **Variation:** Examples show different phrasings and contexts (not just rephrased versions of the same prompt)?
- [ ] **Negative examples reference alternatives:** Each negative example states which skill should handle it?

## Overall

- [ ] **Would a new agent correctly trigger this skill** given only the catalog entry?
- [ ] **Would a new agent correctly NOT trigger this skill** for confusable tasks?
- [ ] **Has the catalog been updated** with this skill's current trigger/anti-trigger info?
