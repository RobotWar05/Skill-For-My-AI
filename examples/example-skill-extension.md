# Example: Skill Extension — Creating a `test-strategy-design` Skill

This example demonstrates how to use the `skill-scaffolder` to create a new canonical skill.

---

## Context

During multiple projects, a recurring pattern emerged: when asked to "write tests" for embedded firmware, the agent would jump straight to writing unit tests without considering the test strategy: what SHOULD be tested, at what level (unit, integration, hardware-in-loop), with what tools, and what coverage targets.

A new skill is needed to enforce test strategy thinking before test implementation.

---

## Step 1: Verify No Existing Skill Covers This

Checked `skills/_catalog/README.md`:
- `review-debug-deep-mode` — reviews existing code for bugs, but doesn't design test strategies.
- `architecture-first-solutioning` — designs system architecture, but testing is a footnote, not the focus.
- `requirement-intake` — intakes requirements, but doesn't cover test planning specifically.

**Conclusion:** No existing skill covers test strategy design. Proceed with scaffolding.

---

## Step 2: Classify the Content

| Question | Answer |
|---|---|
| Is this a single rule for AGENTS.md? | No — it's a multi-step workflow. |
| Is this project-specific? | No — test strategy is needed across all projects. |
| Is this a docs page? | No — it's an actionable workflow, not an explanation. |
| Does it have clear triggers? | Yes — "write tests", "test plan", "test strategy", "how to test this." |

**Decision:** Create a canonical skill.

---

## Step 3: Choose a Name

Following `docs/naming-and-triggering-guidelines.md`:
- Pattern: verb-noun → `test-strategy-design`
- Unique in catalog? ✅
- Under 4 words? ✅
- Not generic? ✅ (not just "testing")

---

## Step 4: Copy Template and Fill

Copied `templates/skill-template/` to `skills/test-strategy-design/`.

### Filled SKILL.md (key sections shown):

**DESCRIPTION:**
> "Designs a test strategy before test implementation begins: identifies what to test, at what level (unit, integration, system, hardware-in-loop), with what tools, and with what coverage targets. Prevents the common pattern of writing random unit tests without a coherent testing plan."

**USE WHEN:**
- User asks to "write tests" for a module or system.
- User asks for a "test plan" or "test strategy."
- User asks "how should I test this?"
- A new module/feature is being designed and test coverage needs planning.

**DO NOT USE WHEN:**
- User asks to run existing tests → direct command execution.
- User asks to debug a failing test → use `review-debug-deep-mode`.
- User asks to review test code quality → use `review-debug-deep-mode`.

**WORKFLOW:**
1. Identify the system/module under test.
2. List all behaviors that need testing (functional requirements → test cases).
3. Classify each test by level: unit / integration / system / HIL.
4. For each level, identify the testing tool/framework (Unity, CMock, pytest, hardware fixture).
5. Define coverage targets (line coverage, branch coverage, requirement coverage).
6. Identify what CANNOT be tested automatically (manual test procedures).
7. Produce the test strategy document.

---

## Step 5: Check for Trigger Overlap

Compared with adjacent skills:
- `review-debug-deep-mode`: Reviews existing code/tests. Does NOT design test strategies. Anti-trigger added to both skills.
- `architecture-first-solutioning`: May mention testing in recommendations. Added cross-reference: "For detailed test planning, use `test-strategy-design`."

---

## Step 6: Generate Eval Prompts

Created `evals/prompts/test-strategy-design.md`:

**Prompt 1 — POSITIVE:** "Write unit tests for my motor controller module."
→ Should trigger. Agent designs strategy first, then implements.

**Prompt 2 — POSITIVE:** "How should I test this communication protocol?"
→ Should trigger. Strategy includes unit tests for packet parser, integration test for protocol flow, HIL test for actual hardware.

**Prompt 3 — NEGATIVE:** "Run `pytest test_sensor.py`."
→ Should NOT trigger. Direct command execution.

**Prompt 4 — NEGATIVE:** "This test is failing: `test_motor_speed`. Debug it."
→ Should NOT trigger. Use `review-debug-deep-mode`.

**Prompt 5 — NEGATIVE:** "Review the quality of my existing test suite."
→ Should NOT trigger. Use `review-debug-deep-mode`.

---

## Step 7: Update Catalog

Added to `skills/_catalog/README.md`:

```markdown
### 9. test-strategy-design

- **Path:** `skills/test-strategy-design/SKILL.md`
- **Purpose:** Designs test strategies before implementation...
- **Use when:** User asks to write tests, create test plans...
- **Do NOT use when:** Running existing tests, debugging test failures...
- **Trigger keywords:** "write tests", "test plan", "test strategy", "how to test"
- **Anti-trigger keywords:** "run tests", "debug test", "review test code"
- **Maturity:** Draft
```

---

## Step 8: Run Trigger Checklist

Ran `evals/trigger-checklist.md`:
- [x] Description specifies task type (test strategy design)
- [x] Context specified (before test implementation)
- [x] Behaviors listed (identify, classify, select tools, define coverage)
- [x] Distinguishable from all other skills
- [x] Under 3 sentences
- [x] All anti-triggers have cross-references
- [x] At least 3 positive examples, 3 negative examples
- [x] Catalog updated

**Result:** All checks pass. Skill is ready for use.
