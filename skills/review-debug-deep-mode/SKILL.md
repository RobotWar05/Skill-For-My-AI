# SKILL: review-debug-deep-mode

---

## 1. NAME

`review-debug-deep-mode`

---

## 2. DESCRIPTION

Activates a deep analysis mode for code review, debugging, and optimization tasks. Systematically searches for both surface-level and latent bugs, classifies findings by severity, assesses regression risk, identifies side effects, and prioritizes root cause analysis over symptom patching. Follows evidence-based standards from `docs/review-debug-standards.md`.

---

## 3. PURPOSE

Superficial reviews catch only obvious bugs. This skill exists to:

- Enforce a systematic, multi-pass analysis (surface → latent → risk → root cause).
- Classify every finding by severity (S1–S5).
- Assess regression risk for each proposed fix.
- Prevent "fix the symptom, ignore the disease" patterns.
- Ensure conclusions are backed by evidence, not guesses.

---

## 4. USE WHEN

- User asks to review code for correctness, quality, or security.
- User asks to debug a specific issue (crash, incorrect behavior, performance).
- User asks to optimize existing code for performance, size, or reliability.
- User provides code or logs and asks "what's wrong" or "why does this fail."
- User asks for a code audit or technical assessment of existing implementation.

---

## 5. DO NOT USE WHEN

- User asks to write new code from scratch (use `architecture-first-solutioning`).
- User asks to explain how something works in general (use `structured-technical-response`).
- User asks to compare options (use `data-driven-tradeoff-analysis`).
- User asks to intake requirements (use `requirement-intake`).
- No code or system output is provided for review.

---

## 6. EXPECTED INPUTS

- Code files, snippets, or modules to review.
- Optionally: error logs, stack traces, test results, expected vs actual behavior.
- Optionally: specific concern areas ("focus on thread safety" or "check memory management").

---

## 7. EXPECTED OUTPUTS

A review/debug report containing:

1. **FINDINGS LIST** — Each finding in this format:
   ```
   FINDING: [Description]
   SEVERITY: [S1-S5]
   LOCATION: [file:function:line]
   EVIDENCE: [What you observed]
   ROOT CAUSE: [Analysis] (confidence: CONFIRMED/LIKELY/SUSPECTED/SPECULATIVE)
   FIX: [Proposed solution]
   REGRESSION RISK: [What could break]
   ```

2. **SUMMARY** — Total counts by severity level.
3. **PRIORITY ORDER** — Which findings to address first and why.
4. **MISSING DATA** — What additional information would improve the analysis.

---

## 8. WORKFLOW

1. **Read all provided code/logs completely** before starting analysis.
2. **Pass 1 — Surface bugs.** Scan for obvious issues: syntax errors, null dereferences, off-by-one, resource leaks, unhandled errors.
3. **Pass 2 — Logic bugs.** Trace execution paths. Check boundary conditions, state transitions, error paths, concurrent access.
4. **Pass 3 — Latent bugs.** Look for: race conditions, timing dependencies, silent failures, integer overflow, buffer overflow, use-after-free.
5. **Pass 4 — Design issues.** Assess: tight coupling, hidden dependencies, poor separation of concerns, scalability limits.
6. **Classify each finding** by severity (S1–S5) using `docs/review-debug-standards.md`.
7. **Assess regression risk** for each proposed fix.
8. **Identify root cause** where possible. Distinguish root cause from symptoms.
9. **Label confidence levels** for all conclusions (CONFIRMED/LIKELY/SUSPECTED/SPECULATIVE).
10. **Present findings** in priority order with the format above.

---

## 9. CONSTRAINTS

- MUST perform multi-pass analysis (not just one scan).
- MUST classify every finding with a severity level.
- MUST assess regression risk for every proposed fix.
- MUST label confidence level on every root cause analysis.
- MUST NOT skip latent bug analysis even if surface bugs are found.
- MUST cite evidence (file, function, line, specific code pattern) for every finding.
- MUST NOT fabricate findings to pad the report. If the code is clean, say so.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT invent bugs that aren't evidenced in the code.
- Do NOT fabricate line numbers or function names.
- Do NOT assume standard library behavior without checking the actual implementation context.
- Do NOT claim a race condition exists without identifying the concurrent access paths.
- Do NOT fabricate test results or reproduction steps.
- If you can't determine the root cause, say so and list what data you'd need.

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "Review this ISR handler for correctness." [code attached]
2. "My UART communication drops packets every 30 seconds. Here's the code."
3. "Optimize this sensor reading loop — it's too slow."
4. "Find bugs in this state machine implementation."
5. "Why does this code crash when I press button B during a WiFi scan?"

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "Write a new UART driver from scratch." → Use `architecture-first-solutioning`.
2. "Explain how DMA works." → Use `structured-technical-response`.
3. "Should I use interrupts or polling?" → Use `data-driven-tradeoff-analysis`.
4. "Build me a monitoring system." → Use `requirement-intake`.

---

## 13. ADAPTATION NOTES

- **For embedded projects:** Add hardware-specific checks: ISR safety, watchdog feeding, stack overflow, DMA buffer alignment.
- **For web projects:** Add checks for: SQL injection, XSS, CSRF, N+1 queries, connection pool exhaustion.
- **For RTOS projects:** Add checks for: priority inversion, deadlock, stack sizing, task starvation.
- These adaptations go in a **project overlay**.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Reference: `docs/review-debug-standards.md` — severity levels, evidence standards, regression checklist.
- No scripts or assets required.
