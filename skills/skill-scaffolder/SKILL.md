# SKILL: skill-scaffolder

---

## 1. NAME

`skill-scaffolder`

---

## 2. DESCRIPTION

Creates new skills from the canonical template when no existing skill in the catalog matches the current task. Guides the agent through the complete skill creation process: classifying content into the correct location (AGENTS.md vs skill vs docs), filling all 14 required sections, generating trigger and anti-trigger examples, creating eval prompts, and updating the catalog. Prevents creation of vague, mega-skills, or duplicate skills.

---

## 3. PURPOSE

Without a structured scaffolding process, new skills tend to be vague, overly broad, or duplicative of existing ones. This skill exists to:

- Provide a repeatable process for skill creation.
- Enforce the quality standards from `docs/skill-authoring-rules.md`.
- Prevent mega-skills (skills that try to do too many things).
- Ensure every new skill has eval prompts from day one.
- Keep the catalog accurate and up-to-date.

---

## 4. USE WHEN

- Agent checked the catalog and found no matching skill for the current task type.
- User explicitly asks to create a new skill.
- A recurring task pattern has been identified that would benefit from formalization.

---

## 5. DO NOT USE WHEN

- An existing skill already covers the task (even partially — consider extending it first).
- The need is a one-time rule that fits in `AGENTS.md`.
- The need is project-specific and belongs in a project overlay.
- The need is a reference document that belongs in `docs/`.

---

## 6. EXPECTED INPUTS

- Description of the task type that needs a new skill.
- Optionally: examples of prompts that should trigger the new skill.
- Optionally: examples of prompts that should NOT trigger the new skill.

---

## 7. EXPECTED OUTPUTS

1. A complete `SKILL.md` with all 14 sections filled.
2. A catalog entry for `skills/_catalog/README.md`.
3. An eval prompt file for `evals/prompts/<skill-name>.md` with at least 5 test prompts.
4. A classification report: what goes in the skill vs what should go elsewhere.

---

## 8. WORKFLOW

1. **Verify no existing skill covers this.** Re-check `skills/_catalog/README.md`. If a partial match exists, consider extending that skill instead.
2. **Classify the content:**
   - Does this belong in a skill, or is it a rule for `AGENTS.md`? (One-line rule → AGENTS.md; workflow → skill)
   - Does this need a docs page? (Explanation/rationale → docs; procedure → skill)
   - Is this project-specific? (Yes → project overlay; No → canonical skill)
3. **Choose a name** following `docs/naming-and-triggering-guidelines.md`:
   - Lowercase, hyphenated, verb-noun or adjective-noun, max 4 words.
   - Verify uniqueness against the catalog.
4. **Copy the template** from `templates/skill-template/SKILL.md`.
5. **Fill Section 2 (DESCRIPTION) first.** This is the most critical section. Apply the checklist from `docs/naming-and-triggering-guidelines.md`:
   - [ ] Specifies task type?
   - [ ] Specifies context?
   - [ ] Lists concrete behaviors?
   - [ ] Distinguishable from all other skills?
   - [ ] Under 3 sentences?
6. **Fill remaining sections 1, 3–14** following `docs/skill-authoring-rules.md`.
7. **Check for trigger overlap** against existing skills. If overlap found:
   - Sharpen both descriptions.
   - Add cross-references in anti-triggers.
   - Add boundary test prompts.
8. **Generate eval prompts:**
   - At least 3 positive trigger prompts.
   - At least 2 negative trigger prompts.
   - Expected behavior and pass/fail criteria for each.
9. **Create catalog entry** with all required fields.
10. **Run `evals/trigger-checklist.md`** against the new skill.

---

## 9. CONSTRAINTS

- MUST verify no duplicate or overlapping skill exists before creating.
- MUST fill ALL 14 sections — no blanks, no "TBD."
- MUST generate eval prompts alongside the skill (not "later").
- MUST NOT create mega-skills. If the skill has more than 12 workflow steps, it's too broad — split it.
- MUST update the catalog immediately after creating the skill.
- MUST run the trigger checklist before considering the skill complete.
- The new skill MUST be immediately usable by an agent — no "fill in project details later" placeholders.

---

## 10. ANTI-HALLUCINATION RULES

- Do NOT fabricate trigger examples that don't represent real use cases.
- Do NOT claim the new skill is "comprehensive" without verifying coverage.
- Do NOT invent dependencies on tools or libraries that don't exist.
- Do NOT create skills for tasks that are already covered (even if phrased differently).

---

## 11. POSITIVE TRIGGER EXAMPLES

1. "I keep having to explain API design principles. Can we make a skill for that?"
2. "There's no skill for database schema review. Create one."
3. "I checked the catalog — nothing covers CI/CD pipeline design. Scaffold a skill."
4. "We need a skill for technical writing/documentation tasks."

---

## 12. NEGATIVE / NON-TRIGGER EXAMPLES

1. "Use the review-debug skill to check this code." → Existing skill. Don't scaffold.
2. "Add a rule: always use TypeScript." → One-line rule. Goes in AGENTS.md or project overlay.
3. "Document our deployment process." → This is a docs task, not a skill creation task.
4. "Fix the trigger description for requirement-intake." → This is a skill edit, not a scaffold.

---

## 13. ADAPTATION NOTES

- This skill is **meta** — it creates other skills. Adaptation means adjusting the skill creation process itself.
- **For domain-specific repos:** Add domain-specific section requirements (e.g., "all embedded skills must include ISR safety notes").
- **For team repos:** Add review/approval requirements to the workflow.
- These adaptations go in a **project overlay**.

---

## 14. REFERENCES / SCRIPTS / ASSETS

- Template: `templates/skill-template/SKILL.md` — the structural base for new skills.
- Reference: `docs/skill-authoring-rules.md` — quality standards for all sections.
- Reference: `docs/naming-and-triggering-guidelines.md` — naming and trigger rules.
- Reference: `evals/trigger-checklist.md` — validation checklist.
