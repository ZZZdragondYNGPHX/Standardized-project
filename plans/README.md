# Plans

Plans document intended design and rationale before or during implementation.

Use semantic categories such as:

- `feat/`
- `fix/`
- `refactor/`
- `package/`
- `plugin/`
- `architecture/`

A small localized task may have no Plan.

## Single-file Plan

Use one Markdown file when the design is compact enough to read efficiently:

```text
plans/feat/custom-start-form.md
```

## Plan Bundle

For large projects, use one project directory:

```text
plans/package/example-project/
├─ index.md
├─ decisions.md
├─ nation.md
├─ religion.md
├─ economy.md
└─ ui.md
```

`index.md` is the only required entrypoint. It routes the agent to the modules needed by each stage.

Keep module ownership explicit. A detailed rule should have one authoritative module; dependent modules link to it instead of duplicating it.

`decisions.md` is optional and contains frozen cross-module decisions.

When working on a Plan Bundle:

1. read `index.md`;
2. read only the modules required for the current stage;
3. avoid loading unrelated modules;
4. update only materially changed modules;
5. update `index.md` when routing, dependencies, stage mapping, or frozen global decisions change.

Templates are available under `templates/PLAN-BUNDLE/`.
