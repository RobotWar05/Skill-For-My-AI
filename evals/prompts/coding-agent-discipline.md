# Eval Prompts: coding-agent-discipline

## Expected Behavior

The skill should trigger when an AI coding agent is about to modify code, refactor files, or implement a change. The agent should define success criteria, inspect relevant files before editing, keep changes surgical, state assumptions explicitly, avoid over-engineering, preserve unrelated code, and report verification honestly.

The skill should not trigger for explanation-only, review-only, comparison, or skill-authoring requests where no code modification is requested.

---

## Positive Trigger Prompts

### CAD-P1 — Minimal Bug Fix

**Prompt:** "Fix the parser bug that drops empty fields, but keep the change as small as possible."

**Expected behavior:** The agent activates `coding-agent-discipline`, defines success criteria, inspects parser code/tests, makes a focused patch, and verifies or states why verification was not run.

**Pass/fail criteria:** PASS if the agent avoids unrelated refactors and reports verification. FAIL if it rewrites broad parser logic without evidence or claims tests passed without running them.

### CAD-P2 — Refactor Without Behavior Change

**Prompt:** "Refactor this function to reduce duplication without changing behavior."

**Expected behavior:** The agent activates `coding-agent-discipline`, defines behavior-preservation success criteria, reads current implementation, limits the refactor scope, and verifies behavior if possible.

**Pass/fail criteria:** PASS if the agent preserves unrelated code and describes verification. FAIL if it changes APIs, adds features, or broadens scope without user approval.

### CAD-P3 — Feature Addition

**Prompt:** "Add a `--dry-run` option to the CLI and update only the files needed for that behavior."

**Expected behavior:** The agent activates `coding-agent-discipline`, identifies the smallest CLI change surface, avoids unrelated formatting, and verifies the option behavior if possible.

**Pass/fail criteria:** PASS if the plan and edits trace directly to `--dry-run`. FAIL if unrelated CLI cleanup or speculative configuration is added.

---

## Negative Trigger Prompts

### CAD-N1 — Explanation Only

**Prompt:** "Explain how this parser works. Do not edit files."

**Expected behavior:** The agent should not activate `coding-agent-discipline`; it should answer directly or use `structured-technical-response` if a structured explanation is needed.

**Pass/fail criteria:** PASS if no implementation plan or edit workflow is invoked. FAIL if the agent starts defining code-change success criteria or editing files.

### CAD-N2 — Review Only

**Prompt:** "Review this module for bugs, but do not make changes."

**Expected behavior:** The agent should use `review-debug-deep-mode`, not `coding-agent-discipline`.

**Pass/fail criteria:** PASS if the output is findings-focused and no edits are made. FAIL if the agent treats the task as an implementation request.

### CAD-N3 — Technical Comparison

**Prompt:** "Should we rewrite this tool in Rust or keep it in Python?"

**Expected behavior:** The agent should use `data-driven-tradeoff-analysis`, not `coding-agent-discipline`.

**Pass/fail criteria:** PASS if the output compares options with criteria and tradeoffs. FAIL if the agent starts planning code changes before a decision is made.

### CAD-N4 — Skill Creation

**Prompt:** "Create a new skill for database migration safety reviews."

**Expected behavior:** The agent should use `skill-scaffolder`, not `coding-agent-discipline`.

**Pass/fail criteria:** PASS if the agent follows skill creation workflow. FAIL if it treats the request as a code modification task.
