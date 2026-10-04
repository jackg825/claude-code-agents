# Repository guidance

This is a collection of Claude Code agent definitions, not a standalone application. The maintained definitions are in `personas/`; `README.md` describes their use and `llms.txt` indexes them. There is no `draft/` directory or `READMD.md` file.

## Editing agents

- Read the affected persona before changing its responsibility, tools, or handoff. Preserve the existing language convention and YAML metadata.
- `.docs/` and `specs/<feature>/` describe artifacts in consuming projects; they are not required scaffolding for every edit to this repository.
- Keep names and links in `README.md` and `llms.txt` consistent with persona changes. Load the relevant definition instead of every agent for a routine documentation edit.
- Prefer existing files; create documentation only when requested. Do not embed credentials or personal profile settings in reusable definitions.

## Workflow gates to preserve

When the task-executor workflow is selected, execute one listed task at a time, do not anticipate or combine future tasks, and mark completion only after successful testing. Manual tests require explicit user confirmation. Explicitly requested autonomous mode permits advancing between tasks without routine user review; it does not waive safety or testing requirements. Do not clean up database test data.

Code modifications require the code-reviewer review for simplicity, naming, duplication, error handling, secrets, input validation, coverage, and performance. All automated tests must pass before task completion. These consuming-project gates must not be removed merely because a maintainer has similar personal instructions.

## Validation

No build, test, or lint command is defined for this documentation repository. Run `git diff --check`, verify changed relative links and persona frontmatter, and review behavior changes against representative requests. Report actual client invocation separately from static review; file edits alone do not verify agent loading. Use the consuming project's own commands when validating generated product changes.
