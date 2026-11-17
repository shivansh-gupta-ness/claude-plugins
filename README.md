# claude-plugins

Private plugin marketplace for the Mini WMS evaluation (see `mini-wms`, `Claude Code Adoption Plan.md`).

| Plugin | Contents | Status |
|---|---|---|
| `core` | `ticket-scout` agent, `start-ticket` skill | pilot set |

Not shipped here on purpose: `change-implementer` and `test-writer`. Plugin subagents ignore `hooks`,
`mcpServers` and `permissionMode`, so the two editing agents live in the project's `.claude/agents/`
where the harness hooks in `.claude/settings.json` apply to them.

Backlog (build only if adoption widens): quality (`test-cases-from-ac`, `failure-triager`), design (`adr-draft`, `threat-model`, `design-reviewer`),
platform (`release-notes`, `runbook`, `incident-review`, `iac-reviewer`, `incident-triager`), leadership (`delivery-report`), and core extras (`capture-learning`, `spec-from-ticket`, `change-workflow`, `pr-summary`).

## Install
```
/plugin marketplace add shivansh-gupta-ness/claude-plugins
/plugin install core@mini-wms-plugins
```
Pin a version with a git tag (`v0.1.0`) once released. Changes go through a PR like code.