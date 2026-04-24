# Canonical AI Agent Skills Repository

A production-grade, vendor-agnostic repository of reusable AI agent skills, principles, templates, and evaluation tools. Designed as the single source of truth for how AI agents should work across all projects and workflows.

---

## Repository Purpose

This repo serves as:

- **Source of truth** for working style, technical principles, and quality standards when collaborating with AI agents.
- **Skill library** — a curated set of reusable, well-tested skills that agents can select and execute.
- **Scaffolding system** — templates and workflows to create new skills without ambiguity.
- **Evaluation framework** — test prompts and checklists to verify skill trigger accuracy and output quality.
- **Adaptation base** — a stable foundation that can be extended for any new project without modifying canonical skills.

**This is NOT a project-specific repository.** It contains no board pinouts, no project file paths, no vendor-locked commands. Project specifics belong in project overlays (see `templates/project-overlay-template.md`).

---

## Quick Start

### For an AI Agent

1. **Read `AGENTS.md`** — contains the repo-wide rules that are always active.
2. **Read `skills/_catalog/README.md`** — browse available skills and their trigger conditions.
3. **Match the current task** to a skill. Follow its `SKILL.md` workflow.
4. **If no skill matches**, use `skills/skill-scaffolder/SKILL.md` + `templates/skill-template/SKILL.md` to create one.

### For a Human

1. Read this README for orientation.
2. Read `docs/repo-philosophy.md` to understand design decisions.
3. Browse `skills/_catalog/README.md` to see what's available.
4. See `docs/adaptation-workflow.md` for how to use this repo in a new project.

---

## High-Level Structure

```
repo-root/
├─ README.md                  # This file — orientation and quick start
├─ AGENTS.md                  # Repo-wide rules (agent reads FIRST)
├─ LICENSE                    # MIT License
├─ CONTRIBUTING.md            # How to add/modify skills
├─ CHANGELOG.md               # Version history
├─ .gitignore
│
├─ docs/                      # Deep documentation
│  ├─ repo-philosophy.md          # Why this repo exists, design rationale
│  ├─ skill-authoring-rules.md    # Rules for writing high-quality skills
│  ├─ when-to-use-skill-vs-agents.md  # What goes where
│  ├─ adaptation-workflow.md      # How to adapt repo for a new project
│  ├─ naming-and-triggering-guidelines.md  # Naming, triggers, anti-triggers
│  ├─ review-debug-standards.md   # Review/debug quality standards
│  ├─ public-release-checklist.md # Public GitHub readiness checks
│  ├─ attribution-policy.md       # External inspiration and license guidance
│  └─ optional-tools.md           # Optional Magika/RTK tooling guidance
│
├─ skills/                    # Reusable skill definitions
│  ├─ _catalog/README.md         # Index of all skills
│  ├─ requirement-intake/         # Intake and clarify requirements
│  ├─ structured-technical-response/  # Format technical responses
│  ├─ source-first-citation/      # Prioritize user-provided sources
│  ├─ architecture-first-solutioning/ # Architecture before code
│  ├─ review-debug-deep-mode/     # Deep review/debug/optimize
│  ├─ embedded-automation-design/ # Embedded/automation best practices
│  ├─ skill-scaffolder/           # Create new skills from template
│  ├─ data-driven-tradeoff-analysis/ # Compare solutions with evidence
│  └─ coding-agent-discipline/    # Keep code changes focused and verifiable
│
├─ templates/                 # Scaffolding templates
│  ├─ skill-template/            # Template for new skills
│  └─ project-overlay-template.md # Template for project-specific config
│
├─ evals/                     # Skill testing and quality assurance
│  ├─ README.md                  # Eval system overview
│  ├─ trigger-checklist.md       # Description quality checklist
│  ├─ regression-process.md      # Post-modification testing process
│  ├─ eval-result-template.md     # Manual eval result record template
│  └─ prompts/                   # Test prompts per skill
│
└─ examples/                  # Worked examples
   ├─ example-project-adaptation.md   # Adapting repo for a project
   └─ example-skill-extension.md      # Creating a new skill
```

---

## How to Use with a New Agent

Any AI agent (OpenAI Codex, Claude Code, Antigravity, or any filesystem-based agent) can use this repo:

1. **Point the agent to the repo root.**
2. **Instruct it to read `AGENTS.md` first.** This file contains the non-negotiable rules.
3. **For task execution**, the agent should consult `skills/_catalog/README.md` and select the appropriate skill.
4. **For project-specific work**, create a project overlay from `templates/project-overlay-template.md` and place it in the project repo (not here).

No vendor-specific configuration is required. The entire system runs on plain Markdown files.

---

## How to Use with a New Project / Workflow

See `docs/adaptation-workflow.md` for the complete process. Summary:

1. Read `AGENTS.md` and `skills/_catalog/README.md`.
2. Identify which canonical skills apply to the project.
3. Create a **project overlay** (from `templates/project-overlay-template.md`) containing:
   - Project-specific constraints (board, toolchain, repo structure).
   - Which canonical skills to activate.
   - Any project-specific skills needed.
4. Place the overlay in the **project repo**, not in this canonical repo.
5. The agent reads the overlay → reads referenced canonical skills → works.

---

## How to Add a New Skill

See `CONTRIBUTING.md` for detailed steps. Summary:

1. Verify no existing skill covers the same task (check catalog).
2. Copy `templates/skill-template/` to `skills/<skill-name>/`.
3. Keep `SKILL.md` at the root of that skill directory.
4. Start `SKILL.md` with YAML frontmatter containing `name` and `description`.
5. Ensure `name` exactly matches the folder name.
6. Write a specific `description`; this is the primary trigger signal for many agent loaders.
7. Fill all 14 required sections in `SKILL.md`.
8. Include positive and negative trigger examples for stable behavior.
9. Write eval prompts in `evals/prompts/<skill-name>.md` (minimum 5).
10. Update `skills/_catalog/README.md`.
11. Run `evals/trigger-checklist.md` against the new skill.

---

## How to Test a Skill

1. Open `evals/prompts/<skill-name>.md`.
2. Feed each test prompt to the agent with access to this repo.
3. Verify:
   - Positive triggers activate the skill.
   - Negative triggers do NOT activate the skill.
   - Output follows the skill's expected format and constraints.
4. After modifying a skill, follow `evals/regression-process.md`.

---

## Conventions

| Convention | Rule |
|---|---|
| Skill names | Lowercase, hyphenated, verb-noun or adjective-noun (e.g., `requirement-intake`) |
| Skill files | Always `SKILL.md` inside a named directory |
| Skill frontmatter | Mandatory YAML frontmatter at the top of every `SKILL.md` with `name` and `description` |
| Descriptions | Specific enough to distinguish from all other skills; no generic wording |
| Trigger examples | Positive and negative examples required for every skill |
| Assumptions | Always labeled `ASSUMPTION` |
| Facts vs Inferences | Always distinguished; never present inference as fact |
| Project specifics | Never in canonical skills; use project overlays |
| Language | English for all skill/doc content (international agent compatibility) |

---

## Versioning Strategy

This repo uses [Semantic Versioning](https://semver.org/):

- **PATCH** (0.1.x): Typo fixes, clarifications, additional eval prompts.
- **MINOR** (0.x.0): New skills, significant rewrites, new documentation sections.
- **MAJOR** (x.0.0): Breaking changes to `AGENTS.md`, skill format changes, catalog schema changes.

Current version: **0.1.0**

---

## Maintenance Strategy

1. **Quarterly review**: Audit all skills for trigger overlap, description quality, and relevance.
2. **Post-incident updates**: If a skill mis-triggers or produces poor output, update the skill and run regression.
3. **Catalog hygiene**: Remove deprecated skills, update maturity levels, flag experimental skills.
4. **Eval expansion**: Continuously add test prompts based on real-world usage patterns.
5. **No silent changes**: Every modification gets a CHANGELOG entry and, for skills, a regression pass.
