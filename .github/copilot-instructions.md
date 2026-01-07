# Copilot instructions (Spec Flow)

This repository is a **documentation/toolkit repo** (markdown prompts + checklists) that extends GitHub’s Spec Kit workflow. There is no application code to build/run here; most changes are edits to markdown artifacts.

## Repo “big picture”

- `README.md` is the primary entrypoint and must stay consistent with the toolkit contents and paths.
- `conversation-prompts/` contains **phase-specific prompt templates** (numbered `01-` … `05-`) that are meant to be copied/pasted into Copilot/agents.
- `memory/` contains **Spec Kit memory files** intended to be copied into a project’s `.specify/memory/` (see `memory/tooling.md`).
- `checklists/` contains reference checklists intended to be copied into a project’s `docs/`.
- `templates/` contains document templates (e.g., `templates/brainstorm-template.md`).

## Editing conventions (important)

- Preserve fenced blocks exactly (```…```), because they are used as **verbatim prompts**.
- Keep the phase structure stable:
  - Titles like “Phase N: …”
  - Top metadata lines like `> **Mode:**` / `> **Agent:**` / `> **Output:**`
- Use the same terminology as the README:
  - “Plan Mode” vs “Agent Mode”
  - Agents like `speckit.constitution`, `speckit.specify`, `speckit.plan`, `speckit.implement`
- Keep all paths aligned with Spec Kit outputs referenced in `README.md` (e.g., `.specify/memory/constitution.md`, `specs/001-feature/spec.md`).

## Cross-file dependencies to keep in sync

- If you change a prompt filename or expected output path, update:
  - `README.md` references to `conversation-prompts/*`, `memory/*`, `checklists/*`, and the “Toolkit Contents” tree.
- If you change framework-selection guidance in `memory/tooling.md`, ensure `README.md` and `conversation-prompts/04-plan.md` still reference the same tools (Stack Match / TechEmpower) and the same “skip when” guidance.

## Project-specific guidance you should not “generalize away”

- The workflow is **spec-first**: Brainstorm → Constitution → Specify → (Clarify) → Plan → Tasks → (Analyze) → Implement → QA → Learn.
- Call out the **greenfield scaffolding gotcha**: when scaffolding, prefer “in-place” (`.`) to avoid nested folders (see `conversation-prompts/05-implement.md` and README).
- This repo is language-agnostic; don’t add language-specific tooling unless it’s explicitly framed as an example or is already documented.

## When adding new files

- Prompts: `conversation-prompts/NN-short-name.md` (keep numbering consistent with workflow phases).
- Memory: `memory/<topic>.md` (written to survive upstream Spec Kit updates).
- Checklists: `checklists/<topic>-checklist.md`.
- Keep markdown headings and tables consistent with existing files.
