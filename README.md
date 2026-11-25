# claude-plugins

Private plugin marketplace for the Mini WMS evaluation (see `mini-wms`, `Claude Code Adoption Plan.md`).

| Plugin | Contents | Status |
|---|---|---|
| `core` | `ticket-scout`, `change-implementer`, `test-writer` agents; `own-code-review`, `independent-code-review`, `test-critic`, `ef-query-verifier`, `spec-drift-auditor` review agents; `start-ticket`, `run-feature-be`, `run-feature-fe`, `own-code-review`, `independent-code-review`, `test-critique`, `ef-verify`, `spec-drift` skills; the three adapted pipeline prompts in `plugins/core/prompts/` | v0.4.0 |

Editing agents in a plugin: plugin subagents ignore their own `hooks`, `mcpServers` and `permissionMode` fields. `change-implementer` and `test-writer` are shipped here, but the scope guard, command guard, formatting and test hooks must come from the consuming repo's `.claude/settings.json` (settings hooks also run inside subagents). Install this plugin only in repos that carry that harness (`mini-wms` does). An agent of the same name in a repo's `.claude/agents/` takes precedence over the plugin's.

Since v0.3.2 `start-ticket` also hands each editing agent's work back with `node .claude/hooks/worktree-apply.mjs "<worktree path>" --remove`, and writes `docs/reports/<ID>/ac-results.md` and a row in `docs/reports/ac-log.md`. Those hooks (`worktree-create`, `worktree-apply`, `worktree-remove`) and the report folder come from the consuming repo, like the guards; `mini-wms` has them. The agents and skills here are kept the same as the copies in `mini-wms/.claude/` (only the prompt paths differ: the plugin reads them through `${CLAUDE_PLUGIN_ROOT}`); change one, change both.

Since v0.4.0 the plugin ships the review agents and skills. They are read-only by instruction: they have no Edit or Write tool, but they have a shell. They name files of `mini-wms` (its ADRs, `docs/knowledge-map.yaml`, `docs/specs/`, the Locations module), so another repo must adapt them. The agents and pipelines load only the `REPO_CONTEXT.md` files that apply to a ticket; the rule ("Context files") and the tests for the 500-line limit live in the consuming repo.

Pipeline skills: `run-feature-be` and `run-feature-fe` read their prompts from `plugins/core/prompts/` through the plugin root, so any repo that installs `core` gets the full pipeline. They assume the consuming repo has `tickets/<ID>.md`, `docs/`, `src/backend` or `src/frontend`, and the harness hooks. In a plugin the skills are namespaced (`/core:run-feature-be`); a same-named skill in the repo's `.claude/skills/` is separate and uses the repo's own `dev_prompts/local/`.

Backlog (build only if adoption widens): quality (`test-cases-from-ac`, `failure-triager`), design (`adr-draft`, `threat-model`, `design-reviewer`),
platform (`release-notes`, `runbook`, `incident-review`, `iac-reviewer`, `incident-triager`), leadership (`delivery-report`), and core extras (`capture-learning`, `spec-from-ticket`, `change-workflow`, `pr-summary`).

## Install
```
/plugin marketplace add shivansh-gupta-ness/claude-plugins
/plugin install core@mini-wms-plugins
```
Pin a version with a git tag (`v0.1.0`) once released. Changes go through a PR like code.