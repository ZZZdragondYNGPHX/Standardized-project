# Local Agent Instructions — plugin

This workspace contains standalone tools.

## Fast path

- Work only in the target tool's top-level directory unless the task explicitly spans tools.
- Do not put tool implementation into `main`.
- Do not merge product `main` into this workspace.
- Prefer local Git/filesystem/search/tests/builds.
- Use a separate product worktree/runtime for integration validation when needed.
- Protect unrelated dirty changes.

For resumed/multi-stage work, read HANDOFF, then the plugin Plan entrypoint. If it is a Plan Bundle, read `index.md` first and only the modules required by the current stage; then read the relevant plugin Record.

Read `docs:README.md` for governance-sensitive operations.
