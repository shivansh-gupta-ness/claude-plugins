# claude-plugins

Private plugin marketplace for the Mini WMS evaluation (see `mini-wms`, `Claude Code Adoption Plan.md`).

| Plugin | Contents | Status |
|---|---|---|
| `core` | `ticket-scout`, `change-implementer`, `test-writer` agents; `start-ticket`, `run-feature-be`, `run-feature-fe` skills; the three adapted pipeline prompts in `plugins/core/prompts/` | pilot set (v0.3.1) |

Editing agents in a plugin: plugin subagents ignore their own `hooks`, `mcpServers` and `permissionMode` fields. `change-implementer` and `test-writer` are shipped here, but the scope guard, command guard, formatting and test hooks must come from the consuming repo's `.claude/settings.json` (settings hooks also run inside subagents). Install this plugin only in repos that carry that harness (`mini-wms` does). An agent of the same name in a repo's `.claude/agents/` takes precedence over the plugin's.

Pipeline skills: `run-feature-be` and `run-feature-fe` read their prompts from `plugins/core/prompts/` through the plugin root, so any repo that installs `core` gets the full pipeline. They assume the consuming repo has `tickets/<ID>.md`, `docs/`, `src/backend` or `src/frontend`, and the harness hooks. In a plugin the skills are namespaced (`/core:run-feature-be`); a same-named skill in the repo's `.claude/skills/` is separate and uses the repo's own `dev_prompts/local/`.

Backlog (build only if adoption widens): quality (`test-cases-from-ac`, `failure-triager`), design (`adr-draft`, `threat-model`, `design-reviewer`),
platform (`release-notes`, `runbook`, `incident-review`, `iac-reviewer`, `incident-triager`), leadership (`delivery-report`), and core extras (`capture-learning`, `spec-from-ticket`, `change-workflow`, `pr-summary`).

## Install
```
/plugin marketplace add shivansh-gupta-ness/claude-plugins
/plugin install core@mini-wms-plugins
```
Pin a version with a git tag (`v0.1.0`) once released. Changes go through a PR like code.