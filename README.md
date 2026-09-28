# Standardized Project

This repository is a reference implementation of a normalized multi-workspace GitHub project layout.

The default branch `main` represents the stable product/source line. Regular source work uses short-lived semantic branches such as `feat/*`, `fix/*`, and `refactor/*`, which are merged back into `main` after verification and then deleted.

Long-lived asset workspaces are separated into dedicated branches:

- `docs` — governance, plans, records, and live handoff state.
- `package` — game/package assets only.
- `plugin` — standalone development tools only.
- `skills` — AI skill assets and their index.
- `reference/<project>` — upstream reference mirrors, created only for real upstream projects.

Repository-wide governance is authoritative on the `docs` branch. Local/CLI agents use branch-local `AGENTS.md`; Claude Code enters through `CLAUDE.md`. Web agents use the persistent Web adapter stored on the `docs` branch as a template.

No active task is represented in this template repository, so `docs:HANDOFF.md` intentionally does not exist.
