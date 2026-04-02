# EU5 Modding Project
**Game version:** 1.1.10 — update when game updates, re-check affected annotations.

## Structure
- `annotations/` — vanilla system references (read-only)
- `mod/` — one folder per mod
- Git tracks only `annotations/` and `mod/`

## Branches
- `main` — stable
- `vanilla-annotation` — annotation work; PR to main when complete. Read `.claude/annotator.md`.
- `mod-dev` — mod development. Read `.claude/modder.md`.

## Agents
- **Writing review:** after writing an annotation, spawn `reviewer` agent on the output

## Memory
Do not write new files to the user memory directory (`~/.claude/projects/.../memory/`). The only permitted file there is `feedback_commits.md`. Project knowledge lives in `CLAUDE.md`, `.claude/annotator.md`, `.claude/modder.md`, and `annotations/`.
