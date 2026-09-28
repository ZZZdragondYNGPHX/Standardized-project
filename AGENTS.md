# Local Agent Instructions — package

This workspace contains game/Package assets, not the product source tree.

## Fast path

- Work directly in the target game's top-level directory.
- Do not create ordinary `feat/*` branches merely because a game is being developed here.
- Do not merge `main` into this workspace.
- Keep historical `.atria` outputs under `<game>/releases/`.
- Do not modify unrelated games.
- Use a separate `main` worktree/runtime/installed product when package compatibility needs product-side validation.
- Prefer local Git, filesystem tools, local package validation, and local test/runtime tooling.
- Protect unrelated dirty changes.

For resumed/multi-stage work, read only the relevant HANDOFF, package Plan, and package Record. Read `docs:README.md` for governance-sensitive operations.
