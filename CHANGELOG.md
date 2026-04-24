# Changelog

All notable changes to this repository will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Added
- `coding-agent-discipline` skill for focused, verifiable AI coding changes.
- Eval prompts for `coding-agent-discipline`, bringing total skill prompt files to 9.
- `evals/eval-result-template.md` for recording manual eval results.
- `docs/public-release-checklist.md` for public GitHub readiness checks.
- `docs/attribution-policy.md` for external inspiration and license-aware adaptation.
- `docs/optional-tools.md` for optional Magika and RTK guidance.

### Changed
- Added mandatory YAML frontmatter to every existing skill and the skill template.
- Clarified canonical base repository scope, data-driven technical recommendation rules, and project-specific content boundaries in `AGENTS.md`.
- Added scope classifications and overlap boundary notes to the skill catalog.
- Tightened `structured-technical-response` so it formats answers without replacing domain workflows.
- Fixed `data-driven-tradeoff-analysis` to reference the stable AGENTS.md data-driven decision rule instead of a section number.
- Updated authoring, contributing, template, eval, and README documentation for mandatory skill frontmatter and trigger examples.

---

## [0.1.0] — 2026-04-23

### Added
- Repository structure and root configuration files.
- `AGENTS.md` with 10 repo-wide rules for AI agents.
- 8 canonical skills:
  - `requirement-intake`
  - `structured-technical-response`
  - `source-first-citation`
  - `architecture-first-solutioning`
  - `review-debug-deep-mode`
  - `embedded-automation-design`
  - `skill-scaffolder`
  - `data-driven-tradeoff-analysis`
- Skill catalog at `skills/_catalog/README.md`.
- Skill template at `templates/skill-template/`.
- Project overlay template at `templates/project-overlay-template.md`.
- Documentation:
  - `docs/repo-philosophy.md`
  - `docs/skill-authoring-rules.md`
  - `docs/when-to-use-skill-vs-agents.md`
  - `docs/adaptation-workflow.md`
  - `docs/naming-and-triggering-guidelines.md`
  - `docs/review-debug-standards.md`
- Evaluation system:
  - `evals/README.md`
  - `evals/trigger-checklist.md`
  - `evals/regression-process.md`
  - 8 eval prompt files in `evals/prompts/`.
- Examples:
  - `examples/example-project-adaptation.md`
  - `examples/example-skill-extension.md`
