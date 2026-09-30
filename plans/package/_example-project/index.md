# Example Project — Plan Index

> Structural example only; this is not an active project.

## Goal

Demonstrate how a large Plan is split into an index and domain modules.

## Frozen core principles

- Read this file before any module.
- Load only modules required by the current stage.
- Detailed rules have one authoritative module.

## Module map

| Module | Authority | Depends on |
| --- | --- | --- |
| `nation.md` | Nation/state design | `religion.md` only for church-state interfaces |
| `religion.md` | Religion/church design | `nation.md` only for state interfaces |

## Stage routing

### Phase 1 — Nation foundation

Required reading:
- `index.md`
- `nation.md`

Do not load unless needed:
- `religion.md`

### Phase 2 — Religion system

Required reading:
- `index.md`
- `religion.md`

Optional:
- `nation.md` only when implementing church-state interactions.
