# research

Agents for understanding code and making informed technical decisions. Mostly read-only. Placeholder category — add agents as you build them.

## Suggested agents

| Agent | Role |
|---|---|
| `explorer` | Maps an unfamiliar codebase or feature area and reports structure and entry points |
| `dependency-auditor` | Reviews dependencies for risk, staleness, license, and known vulnerabilities |
| `security-auditor` | Deep security pass on a module (injection, authz, secrets, data exposure) |
| `spike` | Investigates a technical question and writes up options with trade-offs |

These are typically `readonly: true` — they inform decisions, they don't change code. Follow the repo conventions: focused `description`, read `AGENTS.md` first.
