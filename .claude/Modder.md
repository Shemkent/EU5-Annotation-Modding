## Starting a New Mod
Every mod must have a `.metadata/` folder with the following:

```
mod/[mod_name]/
├── .metadata/
│   ├── metadata.json       # EU5 mod descriptor (required by game)
│   ├── thumbnail.png       # Mod image
│   ├── README.md           # Objectives, requirements, feature list ← START HERE
│   ├── design_notes.md     # Design decisions and rationale
│   └── changelog.md        # Version history
├── in_game/
│   └── common/
└── main_menu/
    └── common/
```

When working on a mod, **read `.metadata/README.md` first**. It contains:
- What the mod is trying to achieve (objectives)
- Specific requirements and constraints
- Feature list and scope

When implementing changes:
1. Check `.metadata/README.md` for objectives — understand intent before touching files
2. Check `annotations/[relevant_system].md` to understand which vanilla files to modify
3. After making changes, update `.metadata/design_notes.md` with decisions made
4. After releasing a version, update `.metadata/changelog.md`

## Working with Annotations

- `annotations/` files document vanilla game systems — read them to understand game mechanics
- Do NOT annotate vanilla game files directly (files live outside the repo)
- Must check `annotations/GAME_STRUCTURE_GUIDE.md` 
- Check `annotations/_file_index.csv` to see which files are already mapped/annotated
- System name in `_file_index.csv` must exactly match the `[system].md` filename slug
- When a system references another (e.g. buildings reference modifier keys), cross-link to the relevant annotation
