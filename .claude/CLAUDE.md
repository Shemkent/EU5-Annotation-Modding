# EU5 Modding Project
**Game version:** 1.1.10 — update when game updates, re-check affected annotations.

## Structure
- `annotations/` — vanilla system references (read-only)
- `mod/` — one folder per mod
- Git tracks only `annotations/` and `mod/`

## Branches
- `main` — stable
- `vanilla-annotation` — annotation work; PR to main when complete
- `mod-dev` — mod development

## Mod conventions
- Mirror EU5 paths: `in_game/common/` and `main_menu/common/`
- Prefix mod files with a short mod ID (e.g. `BPW_country.txt`)
- Read `.metadata/README.md` before touching any mod files

## Agents
- **Mod work:** spawn `modder`
- **Writing review:** after writing an annotation, spawn `reviewer` on the output

## Memory
Do not write new files to the user memory directory (`~/.claude/projects/.../memory/`). The only permitted file there is `feedback_commits.md`. Project knowledge lives in `CLAUDE.md`, `agents/`, and `annotations/`.

## Annotation work
Annotation sessions run at session level — no subagent needed.

### Key files
| File | Purpose |
|---|---|
| `annotations/[system].md` | Output — human-readable reference |
| `annotations/_file_index.csv` | `file, systems, stage, game_version` |
| `annotations/GAME_STRUCTURE_GUIDE.md` | System index, domain clusters, priority tiers |

### Workflow
Run both phases together when scope fits in one pass.

**Phase A — Map**
1. Read plain-text game script files in scope (skip binaries, images, JSON assets)
2. Identify system(s) per file; note block types and keywords
3. Add rows to `_file_index.csv` (`stage=mapped`); `|`-separate multiple systems
4. Add/expand system entry in `GAME_STRUCTURE_GUIDE.md`

**Phase B — Annotate**
1. Read files not yet at `stage=annotated`
2. Write `[system].md` using the format below
3. Mark rows `stage=annotated` in `_file_index.csv`
4. Set stage header in `[system].md` to `complete`
5. Commit on `vanilla-annotation`: `annotate: [system name]`
6. Recommend 1–2 next systems from the same domain cluster that fit a single session

### Annotation format
```markdown
# System Name
**Stage:** complete
**Keywords:** top-level identifiers

> **System type: [Gameplay | AI | UI/Presentation | Scripted Logic | Data/Reference]**

## Overview
What it does and why modders care (one paragraph).

## Vanilla File Locations
Folder and key files. Full list in `_file_index.csv`.

## Block Structure
Syntax skeleton with inline comments. For large blocks: list categories, show 1–2 entries only.

## Key Fields Reference
Table: field | purpose | key constraint. Combine related fields; skip self-evident ones.

## Modding Notes
- Load order, override approach
- Risky vs. safe fields
- Cross-system dependencies
- Non-obvious patterns

## Example
One representative vanilla block with brief commentary.
```

### System types
- **Gameplay** — rules, content, mechanics
- **AI** — AI decisions
- **UI/Presentation** — display only, no gameplay logic
- **Scripted Logic** — shared triggers/effects
- **Data/Reference** — static lookup tables

### Completeness criteria
An annotation is `complete` when: all major fields documented, at least one example, all source files marked `annotated` in `_file_index.csv`, `GAME_STRUCTURE_GUIDE.md` entry links to the annotation.
