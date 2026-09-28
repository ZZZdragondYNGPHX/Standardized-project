# Repository Governance

**Governance version: 1.0**

This branch is the authoritative repository-governance workspace. These rules describe the required repository state and lifecycle independently of whether work is performed by a web agent, desktop agent, Codex CLI, Claude Code, or a human.

## 1. Authority model

For rules and intent:

1. Current explicit user instruction.
2. This Repository Governance.
3. The current approved task Plan.
4. Current live task state in HANDOFF.
5. Environment-specific execution adapter.
6. Default behavior.

For factual repository state:

1. Actual Git/repository state.
2. HANDOFF.
3. Record.
4. Plan.

Documents must be corrected when they disagree with actual repository state. Do not roll code backward merely to match stale documentation.

## 2. Branch model

### `main`

Stable product/source line.

Ordinary product work is performed on short-lived semantic branches such as:

- `feat/<task>`
- `fix/<task>`
- `refactor/<task>`
- other semantic prefixes only when clearly justified.

A completed task branch is merged into `main`, verified, then deleted.

### `reference/<project>`

External upstream mirror/reference branches.

Rules:

- Create only for a real external project.
- Treat as upstream material, not as a normal development workspace.
- User saying **reference <project>** authorizes reading that one reference branch.
- User saying **update <project>** authorizes syncing that reference branch.
- Reference permission does not imply update permission; update permission does not imply reference permission.
- Permission for one reference does not authorize reading other references.
- Do not add local governance files to a reference mirror unless those files originate upstream.

### `package`

Long-lived game/Package asset workspace.

- Contains game development data only.
- One top-level directory per game/package.
- Each game keeps historical distributable `.atria` artifacts under its own `releases/` directory.
- Do not merge `main` into `package` merely to obtain product source.
- Do not place product source, standalone tools, or AI Skills here.
- Package development normally happens directly in this long-lived workspace, separated by game directory.

### `plugin`

Long-lived standalone tool workspace.

- One top-level directory per tool.
- Contains utilities such as MCP servers, validators, preview tools, or other development helpers.
- Do not merge `main` into `plugin` merely to obtain product source.
- Keep tools isolated by directory.

### `docs`

Long-lived governance and project-documentation workspace.

Primary structure:

- `README.md` — this authoritative Governance and repository router.
- `plans/` — approved designs and implementation plans.
- `records/` — permanent implementation history.
- `HANDOFF.md` — optional live recovery state for the one current task that needs handoff.
- `WEB-PERSISTENT-PROMPT.md` — reusable Web execution adapter template.

### `skills`

Long-lived AI Skill asset workspace.

- One directory per Skill.
- `SKILLS.md` is the routing/index document.
- Load only Skills required by the user or the current approved Plan.
- Third-party Skills retain source/upstream metadata.

## 3. Independent long-lived workspaces

`docs`, `package`, `plugin`, and `skills` are logically independent long-lived workspaces and should be created/migrated as orphan/independent-root branches when local Git can do so.

This template repository was initialized through a remote GitHub connector that cannot create parentless commits, so these example branches share only the initial bootstrap ancestry with `main`. Their current file trees and future responsibilities are isolated. When applying this standard with local Git, create true orphan roots for these long-lived workspaces.

## 4. Task identity and ownership

Every substantial task should have one stable Task ID matching its primary ownership, for example:

- `feat/custom-start-form`
- `fix/startup`
- `refactor/memory-runtime`
- `package/cultist-simulator`
- `plugin/mcp`

A task has one **Primary Workspace**. Other workspaces may support validation or integration, but do not create duplicate Records for the same task merely because supporting assets were touched.

## 5. Plans

Plans describe intended design and rationale.

Suggested organization:

- `plans/feat/`
- `plans/fix/`
- `plans/refactor/`
- `plans/package/`
- `plans/plugin/`
- `plans/architecture/`

Rules:

- Small/local tasks may proceed without a formal Plan.
- Larger features, refactors, architecture work, complex packages/plugins, or tasks explicitly discussed before implementation should have a Plan.
- Update a Plan when the approved design materially changes; do not churn it for ordinary implementation details.
- Plans are environment-neutral. They describe what and why, not a client-specific Git/API procedure.

## 6. Records

Records are permanent implementation history.

Suggested organization mirrors real executed task ownership:

- `records/feat/`
- `records/fix/`
- `records/refactor/`
- `records/package/`
- `records/plugin/`

Rules:

- A completed formal task has a Record.
- Small single-pass work may write the Record once at completion.
- Multi-stage work updates the **same Record after every completed stage**. Preserve earlier stages and append/organize later stages.
- Do not wait until the final stage and reconstruct early work from memory.
- A stage entry should normally capture start/end HEADs, completed work, key decisions, validation/CI, known limitations, and the next trusted checkpoint.
- At final completion, normalize the accumulated Record into a clear final form without discarding useful stage history.

## 7. HANDOFF

`HANDOFF.md` is live recovery state, not permanent history.

Create it when at least one applies:

- a multi-stage task is active;
- a task will continue across conversations or agents;
- work must stop for an external dependency;
- the user explicitly requests handoff.

Rules:

- There is at most one live repository-level `HANDOFF.md`.
- Once it exists, every actual work round must keep it current.
- It records the current task, Primary Workspace, branch/HEAD, current stage, completed/pending work, validation state, key decisions, files to read next, and what must not be repeated.
- It may include a new-chat bootstrap prompt, but that prompt is a hint, not a substitute for repository verification.
- Delete `HANDOFF.md` when the task finishes.
- No live task exists in this template repository, so `HANDOFF.md` is intentionally absent.

## 8. Small tasks and multi-stage tasks

### Small task

Default behavior is one continuous closure:

analyze → create semantic task branch when applicable → modify → test/validate → commit/persist → push → verify → write Record → merge to `main` when applicable → verify `main` → delete temporary branch → remove HANDOFF if one was created.

Do not create artificial phases or repeatedly ask whether to continue ordinary steps.

### Multi-stage task

Use one task branch/workspace for the whole task unless the approved Plan says otherwise.

At the end of each stage:

1. complete implementation for that stage;
2. run appropriate validation;
3. persist and push the stage implementation;
4. update the Plan only if the design materially changed;
5. update the same Record with the completed stage;
6. update/create HANDOFF with the exact current state;
7. stop before the next stage and provide a new-chat bootstrap prompt.

Final merge/cleanup happens only after all stages are complete and verified.

## 9. Checkpoints and cross-workspace traceability

For multi-stage work, each completed stage creates a trusted logical checkpoint:

- stage name;
- start HEAD;
- tested/end HEAD;
- validation or CI result.

Implementation/asset workspaces do not need to record the current docs commit. Instead, docs Records/HANDOFF point to exact implementation/package/plugin HEADs. This avoids circular commit references.

When a task touches multiple workspaces, identify one Primary Workspace and record supporting workspace HEADs in the primary Record.

## 10. Minimal Context Routing

Context is loaded by task need, not by startup ritual.

Default progression:

- Level 0: user request + branch-local `AGENTS.md` or Web hot-path rules.
- Level 1: relevant Plan and HANDOFF when the task requires them.
- Level 2: relevant Record/history for resumed or dependency-sensitive work.
- Level 3: full Governance, explicitly selected Skill, or explicitly authorized reference branch.

Rules:

- Do not scan all Plans, Records, Skills, or reference branches “just in case.”
- Search is for locating relevant material; search results do not imply full-document loading.
- Every loaded Plan/Record/HANDOFF/Skill/reference should have a direct relationship to the current task.
- A user-provided handoff prompt is a bootstrap hint; verify current Git state and the named authoritative documents.

## 11. Skills

Skills are opt-in task methods, not global context.

Load a Skill only when:

- the user explicitly requests it; or
- the current approved Plan explicitly requires it.

`SKILLS.md` routes to the specific Skill. Do not load every Skill.

A Skill may guide implementation technique but may not expand task scope or override Governance/Plan constraints.

## 12. Governance-sensitive operations

Read this full Governance before performing operations such as:

- creating/deleting/renaming long-lived branches;
- changing long-lived workspace structure;
- changing Plan/Record/HANDOFF lifecycle;
- changing `reference/*` semantics;
- restructuring multiple workspaces;
- modifying `AGENTS.md`, `CLAUDE.md`, or the Web adapter;
- introducing a new asset/workspace category;
- resolving uncertainty about task ownership;
- performing repository-wide migration.

Ordinary localized product work should rely on the branch-local hot path instead of rereading this entire document every time.

## 13. Execution environment separation

Governance defines required outcomes, not client-specific mechanics.

### Web agents

Use `WEB-PERSISTENT-PROMPT.md` as the reusable execution adapter. A Web agent should use available GitHub/remote capabilities, treat remote refs as factual state, and never claim local validation it did not perform.

### Local/CLI agents

Use branch-local `AGENTS.md` as the fast-path execution adapter.

Local agents should prefer:

- local Git and filesystem operations;
- local search;
- local tests/builds;
- `git show <branch>:<path>` for read-only cross-branch access;
- `git worktree` for simultaneous writable workspaces.

Protect unrelated dirty worktree changes. Do not imitate Web/API detours when direct local operations are available.

`CLAUDE.md` is a thin Claude Code entry and must not become a second governance source.

## 14. Stop conditions

Two kinds of stops exist:

### Governance stop

Required regardless of environment, such as completion of a formally separated stage.

### Environment stop

Required only when the execution environment truly cannot continue, such as unavailable hardware/device evidence, user-only authorization/secret handling, or a clearly long-running remote validation dependency.

Ordinary code errors, test failures, merge conflicts, or implementation choices should normally be handled by the acting agent instead of being escalated to the user.

## 15. Completion criteria

### Product task (`feat/*`, `fix/*`, `refactor/*`)

Complete only when implementation is done, appropriate validation passed, remote state is persisted, Record is current, any materially changed Plan is current, work is integrated into `main`, `main` is verified, the temporary branch is removed, and live HANDOFF is deleted.

### Package task

Complete when package implementation and validation are done, Record is current, required release artifact/version is stored under the game's `releases/`, remote `package` state is persisted, and live HANDOFF is deleted.

### Plugin task

Complete when tool implementation/validation are done, Record is current, remote `plugin` state is persisted, and live HANDOFF is deleted.

### Skill task

Complete when the Skill asset and upstream metadata are current, `SKILLS.md` routing is current, structure is validated, and remote `skills` state is persisted.

## 16. Commit message guidance

Prefer concise semantic messages, for example:

- `feat(memory): add package memory bridge`
- `fix(startup): handle invalid bootstrap state`
- `refactor(runtime): simplify lifecycle`
- `package(cultist-simulator): implement church economy`
- `plugin(mcp): add preview endpoint`
- `docs(cultist-simulator): record phase 2`
- `skill(frontend-design): sync upstream skill`

These are guidance, not a reason to split coherent changes into artificial commits.
