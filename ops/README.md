# ops

Agents for infrastructure, deployment, and operations. Placeholder category — add agents as you build them.

## Suggested agents

| Agent | Role |
|---|---|
| `deployer` | Runs and verifies deploys, checks health after rollout, knows the rollback path |
| `incident-responder` | Triages alerts/errors, correlates logs and metrics, proposes mitigations |
| `infra-reviewer` | Reviews IaC / config changes (Workers config, bindings, env, DNS) for safety |
| `ci-fixer` | Diagnoses red CI pipelines and proposes minimal fixes |

Follow the repo conventions: one responsibility per agent, a specific `description`, read `AGENTS.md` first, and set `readonly: true` for anything that only inspects.
