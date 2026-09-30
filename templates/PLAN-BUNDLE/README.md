# Plan Bundle Template

Use a Plan Bundle when one Plan is too large for efficient stage-by-stage reading.

Create a project directory under the appropriate Plan category, for example:

```text
plans/package/my-project/
├─ index.md
├─ decisions.md
├─ nation.md
├─ religion.md
└─ economy.md
```

Rules:

- `index.md` is the single entrypoint and routing authority.
- Module files own only their domain.
- Do not duplicate detailed rules across modules.
- `decisions.md` is optional and stores frozen cross-module decisions.
- Each implementation stage should list the exact modules it must read.
- Agents read `index.md` first, then only the modules required for the current stage.
