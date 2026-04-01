# EU5 Modding Project Guidelines

## Game Version
Current: **1.1.10**
Update this line when the game updates, then re-check affected annotations.

## Project Structure
- `annotations/` — Reference guides for vanilla game systems (read-only reference)
- `mod/` — All mods live here, one folder per mod
- Git tracks only `annotations/` and `mod/`; all game files are ignored

## Git & Branches
- `main` — stable scaffolding only
- `vanilla-annotation` — annotation work; PR to main when a system is fully documented
- `mod-dev` — active mod development

## Mod File Conventions
- Mod files mirror EU5 standard: `in_game/common/` and `main_menu/common/`
- Prefix mod-specific files with a short mod identifier (e.g. `BPW_country.txt`)
- In-file comments are encouraged for complex or non-obvious changes
- Commit frequently with descriptive messages

## Agent Routing
- **Annotation work** (`vanilla-annotation` branch): spawn the `annotator` agent for each system. After it completes, spawn the `reviewer` agent on the written `.md` file.
- **Mod work** (`mod-dev` branch): spawn the `modder` agent for mod implementation tasks.
- **Writing review**: the `reviewer` agent checks annotation prose for conciseness, clarity, and consistency. It does not check technical accuracy.
