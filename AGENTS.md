# Local Agent Instructions — main

This workspace is the stable product/source line.

## Fast path

- Treat `main` as stable. Do not perform ordinary feature/fix/refactor work directly on it.
- Create short-lived semantic task branches such as `feat/<name>`, `fix/<name>`, or `refactor/<name>`.
- Prefer the local filesystem, local Git, local search, local tests, and local builds over remote/API detours.
- Inspect `git status` before modifying the working tree. Protect unrelated user changes; use a separate worktree when needed.
- Do not place game/package assets, standalone tools, or AI skill assets in this workspace.
- Do not read or update `reference/*` unless the user explicitly authorizes that reference/update operation.

## Context routing

Load only the context required by the current task.

- Existing multi-stage/resumed task: read HANDOFF, then the Plan entrypoint. If it is a Plan Bundle, read `index.md` first and only the modules required by the current stage; then read the relevant Record.
- New ordinary task: start from this file and relevant source files; do not scan all docs/history.
- User/Plan explicitly names a Skill: read `skills:SKILLS.md`, then only that Skill.
- Governance-sensitive operation: read `docs:README.md`.

Governance-sensitive operations include changing long-lived branch structure, repository document lifecycle, cross-workspace ownership, rule files, or final task cleanup semantics.

Repository Governance on `docs:README.md` is authoritative if this hot-path summary is stale.
