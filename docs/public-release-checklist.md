# Public Release Checklist

Use this checklist before publishing this repository to a public GitHub remote.

## Required Checks

- [ ] `LICENSE` is present and matches the intended release license.
- [ ] `README.md` clearly describes the repository purpose, audience, and non-goals.
- [ ] `AGENTS.md` clearly states that this is a canonical base skills repository, not a project-specific repository.
- [ ] Every skill lives in `skills/<skill-name>/SKILL.md`.
- [ ] Every `SKILL.md` starts with YAML frontmatter containing `name` and `description`.
- [ ] `skills/_catalog/README.md` includes every canonical skill.
- [ ] `evals/prompts/` includes prompt coverage for every canonical skill.
- [ ] No secrets, API keys, tokens, credentials, private URLs, or environment dumps are present.
- [ ] No personal/private data is present in canonical docs, skills, templates, evals, or examples.
- [ ] No accidental project-specific build commands, test commands, board pin mappings, product API schemas, or product workflows are present.
- [ ] External inspirations are attributed where relevant.
- [ ] Copied external content is not present unless license compatibility and attribution have been reviewed.
- [ ] `CHANGELOG.md` describes notable changes accurately.
- [ ] Manual trigger evals have been run or explicitly deferred.

## Chat Archive Handling

- [ ] `Chat.txt` or any user-preserved chat archive remains exactly where the user keeps it.
- [ ] The chat archive is not treated as canonical repository instruction.
- [ ] The chat archive is not included in the skill catalog.
- [ ] The user manually reviews the chat archive before public release if privacy matters.

## Release Decision

Publish only after the checklist above is complete and the final diff has been reviewed by a human maintainer.
