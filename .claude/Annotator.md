# Annotator Guide

## Artifacts
| File | Purpose |
|---|---|
| `annotations/[system].md` | Human-readable reference |
| `annotations/_file_index.csv` | `file, systems, stage, game_version` — master file index |
| `annotations/GAME_STRUCTURE_GUIDE.md` | System index with folder paths and keywords |

## Workflow
Both phases run together when scope is small enough to read all files in one pass.

**Phase A — Map**
1. Read plain-text game script files in scope
2. Identify system(s) per file; note block types and keywords
3. Add rows to `_file_index.csv` (`stage=mapped`); use `|` for multiple systems
4. Add/expand system entry in `GAME_STRUCTURE_GUIDE.md`

**Phase B — Annotate**
1. Read files not yet at `stage=annotated`
2. Write/expand `[system].md` using the format below
3. Set rows to `stage=annotated` in `_file_index.csv`
4. Set stage header in `[system].md` to `complete`
5. Commit on `vanilla-annotation`: `annotate: [system name]`

## Annotation Format

```markdown
# System Name
**Stage:** complete
**Keywords:** top-level identifiers, cross-system refs

> **System type: [Gameplay | AI | UI/Presentation | Scripted Logic | Data/Reference]**
> One-line note if the file is non-functional, a foreign artifact, or display-only.

## Overview
One paragraph: what it does in-game and why modders care.

## Vanilla File Locations
Folder path and what each key file covers.
For full file list see `_file_index.csv`.

## Block Structure
Syntax skeleton with inline comments.
For large multi-element blocks (e.g. modifier): use a comment listing categories of entries,
show 1–2 representative entries only — do not enumerate all values.

## Key Fields Reference
Concise table: field | purpose | key constraint.
Combine related fields on one row. Skip self-evident fields.

## Modding Notes
- Load order (numbered prefix, override approach)
- Risky vs. safe fields
- Cross-system dependencies
- Non-obvious patterns

## Example
One representative vanilla block with brief commentary.
```

## System Types
Tag each annotation with one of:
- **Gameplay** — defines rules, content, or mechanics
- **AI** — drives AI decisions
- **UI/Presentation** — display config only; no gameplay logic
- **Scripted Logic** — shared triggers/effects referenced across systems
- **Data/Reference** — static lookup tables, hardcoded lists

> **TODO:** Restructure `GAME_STRUCTURE_GUIDE.md` by system type once coverage is sufficient.
> Currently flat-alphabetical; grouping by type will make it more useful to modders.
