# Review and Debug Standards

This document defines the quality standards for code review, debugging, and optimization tasks.

---

## Severity Levels

When reporting issues found during review or debug, classify each finding:

| Level | Label | Definition | Action Required |
|---|---|---|---|
| S1 | **CRITICAL** | Data loss, security vulnerability, system crash, hardware damage risk | Must fix before any other work. Stop and address immediately. |
| S2 | **HIGH** | Incorrect behavior under normal conditions, race condition, resource leak | Must fix before release. |
| S3 | **MEDIUM** | Incorrect behavior under edge conditions, performance degradation, poor error handling | Should fix; schedule in current sprint. |
| S4 | **LOW** | Code style, naming, minor inefficiency, missing documentation | Fix when convenient; do not block release. |
| S5 | **INFO** | Observation, suggestion, or potential future concern | Record for awareness; no action required now. |

---

## Risk Analysis Framework

For each finding, assess:

### 1. Impact
- What breaks if this issue occurs?
- How many users/systems are affected?
- Is the failure recoverable or catastrophic?

### 2. Probability
- How likely is the trigger condition in normal operation?
- Does it require specific timing, input, or state to manifest?

### 3. Detectability
- Will the issue be caught by existing tests, logs, or monitoring?
- Is the failure silent or visible?

### Risk Priority

```
Risk = Impact × Probability × (1 / Detectability)
```

A high-impact, high-probability, low-detectability issue is the most dangerous.

---

## Regression Awareness

When fixing a bug or modifying code, always consider:

1. **What else uses this code path?** — Trace callers, dependencies, and shared state.
2. **What assumptions do other modules make about this behavior?** — A fix that changes return values, timing, or state transitions can break callers.
3. **What tests cover this code?** — If no tests exist, flag this as an additional risk.
4. **Does the fix introduce new resource usage?** — Memory, CPU, file handles, network connections.
5. **Does the fix change any timing characteristics?** — Especially critical in embedded/real-time systems.

### Regression Checklist

- [ ] Identified all callers of the modified function/module.
- [ ] Verified no caller depends on the old (buggy) behavior.
- [ ] Checked for shared state that might be affected.
- [ ] Verified resource cleanup paths are still correct.
- [ ] Confirmed timing/ordering assumptions still hold.
- [ ] Ran existing tests (or noted their absence).

---

## Evidence-Based Conclusions

### Rules

1. **Every conclusion must cite evidence.** Point to the specific code, log line, configuration, or measurement that supports your conclusion.
2. **Distinguish root cause from symptoms.** Fixing a symptom without identifying root cause leads to recurring issues.
3. **Label your confidence level:**
   - **CONFIRMED** — Reproduced and verified with evidence.
   - **LIKELY** — Strong evidence but not fully reproduced.
   - **SUSPECTED** — Consistent with symptoms but other causes are possible.
   - **SPECULATIVE** — Possible but insufficient evidence; needs investigation.

### Format

When presenting findings:

```
FINDING: [Description of the issue]
SEVERITY: [S1–S5]
EVIDENCE: [Specific file:line, log output, or measurement]
ROOT CAUSE: [Analysis] (confidence: CONFIRMED/LIKELY/SUSPECTED/SPECULATIVE)
FIX: [Proposed solution]
REGRESSION RISK: [What could break]
```

---

## Missing-Data Protocol

When you lack sufficient information to complete a review or debug task:

### Step 1: State What You Know
- List the facts you have from the provided context.

### Step 2: State What You Need
- Be specific: "I need the output of `dmesg | tail -20` after the crash" is better than "I need more logs."
- Prioritize: list the most useful missing data first.

### Step 3: State What You Can Conclude Without It
- Provide your best analysis with available data.
- Label all conclusions with appropriate confidence levels.
- Do NOT fabricate data to fill gaps.

### Step 4: Provide Conditional Recommendations
- "IF the log shows [X], THEN the root cause is likely [Y] and the fix is [Z]."
- "IF [assumption] is correct, THEN [recommendation]. Otherwise, [alternative]."

---

## Optimization Standards

When optimizing code or systems:

### 1. Measure First
- Do NOT optimize without baseline measurements.
- Specify what was measured, how, and with what tool.
- If measurements aren't available, state this and request them.

### 2. Identify the Bottleneck
- Optimization without profiling is guesswork.
- Focus on the critical path, not the easy fix.

### 3. Quantify the Improvement
- "Reduced latency from 12ms to 3ms (75% improvement)" is acceptable.
- "Made it faster" is NOT acceptable.

### 4. Document the Tradeoff
- Every optimization has a cost. State it.
- Common costs: code complexity, memory usage, portability, maintainability.

### 5. Verify No Regression
- Optimization changes must pass the regression checklist above.
- Performance gains that introduce correctness bugs are not gains.
