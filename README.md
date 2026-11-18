# claude-plugins

Private plugin marketplace for the Mini WMS evaluation (see `mini-wms`, `Claude Code Adoption Plan.md`).

| Plugin | Contents | Status |
|---|---|---|
| `core` | `ticket-scout`, `change-implementer`, `test-writer` agents, `start-ticket` skill | pilot set (v0.2.0) |

Editing agents in a plugin: plugin subagents ignore their own `hooks`, `mcpServers` and `permissionMode` fields. `change-implementer` and `test-writer` are shipped here, but the scope guard, command guard, formatting and test hooks must come from the consuming repo's `.claude/settings.json` (settings hooks also run inside subagents). Install this plugin only in repos that carry that harness (`mini-wms` does). An agent of the same name in a repo's `.claude/agents/` takes precedence over the plugin's.

Backlog (build only if adoption widens): quality (`test-cases-from-ac`, `failure-triager`), design (`adr-draft`, `threat-model`, `design-reviewer`),
platform (`release-notes`, `runbook`, `incident-review`, `iac-reviewer`, `incident-triager`), leadership (`delivery-report`), and core extras (`capture-learning`, `spec-from-ticket`, `change-workflow`, `pr-summary`).

## Install
```
/plugin marketplace add shivansh-gupta-ness/claude-plugins
/plugin install core@mini-wms-plugins
```
Pin a version with a git tag (`v0.1.0`) once released. Changes go through a PR like code.