# Plugin Workspace

This long-lived workspace contains standalone development tools.

Each tool owns one top-level directory, for example:

```text
mcp/
validator/
preview-tool/
```

A tool may choose its own internal source/test/release structure.

Rules:

- Do not place product source or game assets here.
- Do not merge `main` merely to obtain product source.
- Keep unrelated tools isolated by directory.
- Validate integrations against a separate product worktree/runtime when needed.
- Complex/multi-stage tool work is documented under `docs:plans/plugin/` and `docs:records/plugin/`.
- `_example-tool/` demonstrates directory ownership only.
