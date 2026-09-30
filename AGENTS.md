# Local Agent Instructions — docs

This workspace contains repository governance and project documentation, not product implementation.

## Allowed responsibilities

- `README.md`: authoritative Repository Governance and router.
- `plans/`: intended design and rationale; large projects may use Plan Bundles with `index.md` plus module files.
- `records/`: permanent executed-task history.
- `HANDOFF.md`: optional single live recovery state.
- `WEB-PERSISTENT-PROMPT.md`: Web execution adapter template.

Do not implement product source, game/package assets, plugin tools, or Skills in this workspace.

## Fast path

- Use local Git/filesystem directly.
- When reading another branch, prefer `git show <branch>:<path>`.
- When editing docs while another workspace is active, prefer a separate docs worktree instead of repeatedly switching branches.
- For Plan Bundles, keep `index.md` as the routing entrypoint and avoid duplicated detailed rules across modules.
- Keep existing live HANDOFF current after every actual work round.
- For multi-stage work, update the same Record at every completed stage.
- Delete HANDOFF when the represented task completes.
- Protect unrelated dirty changes.

Read this branch's `README.md` before any governance-sensitive change.
