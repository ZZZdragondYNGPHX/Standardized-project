# Package Workspace

This long-lived workspace contains game/Package development data only.

## Layout

Each game/package owns one top-level directory:

```text
<Game Name>/
├─ README.md
├─ ...game-specific development files...
└─ releases/
   ├─ <game>-v0.1.0.atria
   ├─ <game>-v0.2.0.atria
   └─ ...
```

Only `README.md` and `releases/` are structural expectations; other directories depend on the game.

Rules:

- Do not merge product `main` into this workspace merely to obtain source.
- Keep each game's files inside its own directory.
- Historical `.atria` deliverables are retained under that game's `releases/`.
- Do not overwrite old release artifacts unless the user explicitly requests cleanup.
- Complex/multi-stage package work is documented under `docs:plans/package/` and `docs:records/package/`.
- `_example-game/` demonstrates layout only and is not a real release.
