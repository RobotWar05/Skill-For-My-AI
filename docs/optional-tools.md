# Optional Tools

This repository is plain Markdown and does not require external tools. The tools below may help some agents, but they are optional and must not become mandatory behavior for the canonical base repo.

## Rules for Optional Tools

- Optional tools are not required to use this repository.
- If a tool is unavailable, the agent should continue without failing.
- Tool output is evidence, not a substitute for reading important files.
- If compressed or summarized output hides important debug details, read the raw output.
- Do not add mandatory installation steps for optional tools to canonical skills.
- Project overlays may recommend tools for a specific project, but canonical skills should remain vendor-agnostic.

## Magika

Magika is an AI-powered file type detection tool from `google/magika`. It can help classify unknown, extensionless, or suspicious files before deeper analysis.

Potential use cases:

- Identifying file types when names or extensions are missing.
- Distinguishing text, code, document, and binary-like inputs before choosing an analysis path.
- Supporting safety review of unfamiliar files.

Boundaries:

- Magika output should be treated as supporting evidence.
- Important files still need direct inspection.
- Do not fail a workflow just because Magika is unavailable.
- Do not create a mandatory Magika-based skill unless a recurring file-intake workflow clearly needs it.

Source: https://github.com/google/magika

## RTK

RTK is a CLI proxy from `rtk-ai/rtk` that compresses and filters terminal output for common development commands. It can reduce noisy output from commands such as diffs, search results, logs, and test runners.

Potential use cases:

- Reducing very noisy terminal output.
- Grouping repeated errors.
- Condensing large diffs or test logs before first-pass triage.

Boundaries:

- RTK output may omit details needed for debugging.
- If a failure is unclear, inspect raw command output.
- Do not replace source-file reads with compressed summaries.
- Do not create a mandatory RTK-based skill unless a recurring terminal-output workflow clearly needs it.

Source: https://github.com/rtk-ai/rtk
