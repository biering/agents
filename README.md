# agents

A collection of reusable AI subagents for [Cursor](https://cursor.com), organized by category. Each agent is a single Markdown file with YAML frontmatter that Cursor's Agent can delegate to automatically or you can invoke explicitly with `/name`.

The design goal: small, focused, single-purpose agents that compose. Project-specific rules (stack, commands, conventions) live in each project's `AGENTS.md`, so these agents stay generic and portable.

## Categories

Agents are grouped by domain. Add new categories as folders; each category has its own `README.md`.

| Category | What lives here | Status |
|---|---|---|
| [`dev/`](./dev) | Building and maintaining code — orchestration, review, simplification, testing, docs | ✅ populated |
| [`ops/`](./ops) | Infrastructure, deployment, CI/CD, incident response | 🌱 placeholder |
| [`research/`](./research) | Codebase exploration, dependency & security audits, technical spikes | 🌱 placeholder |
| [`writing/`](./writing) | Non-code writing — changelogs, release notes, PR descriptions, announcements | 🌱 placeholder |

## Install into a project

Cursor loads subagents from `.cursor/agents/` (project) or `~/.cursor/agents/` (all projects). Copy the agents you want from a category into that folder:

```bash
# from your project root — pull in the whole dev fleet
mkdir -p .cursor/agents
cp /path/to/agents/dev/*.md .cursor/agents/
```

Or symlink a category so updates flow through:

```bash
ln -s /path/to/agents/dev .cursor/agents
```

Cursor also reads `.claude/agents/` and `.codex/agents/` for cross-tool compatibility, so the same files work there.

Commit `.cursor/agents/` into each project so your team gets the agents too.

## How the dev fleet works together

The `dev/` category is a coordinated fleet, not five unrelated tools. `lead` orchestrates the rest:

```
plan → build → test → simplify → review → docs
```

See [`dev/README.md`](./dev/README.md) for the full pipeline, parallel patterns, and the shared auto-fix safety policy.

## Conventions for agents in this repo

- **One responsibility per agent.** No generic "helper" agents.
- **Invest in the `description`.** It's what Cursor reads to decide when to delegate — be specific about *when* to use the agent.
- **Read `AGENTS.md` first.** Every agent should defer to the host project's conventions over its own defaults.
- **Keep prompts concise.** Aim for well under ~200 lines; long prompts dilute focus.
- **Declare write scope.** Reviewers/auditors set `readonly: true`. Writers follow an explicit auto-fix policy (apply low-risk, flag risky).

## Adding a new agent

1. Pick or create a category folder.
2. Add `<name>.md` with frontmatter (`name`, `description`, `model: inherit`, and `readonly: true` for non-editing agents).
3. Write a focused prompt: when invoked → what to check → what to output.
4. Update that category's `README.md` table.

## Adding a new category

Create a folder, add a `README.md` describing its purpose and listing its agents, then add a row to the table above.

## License

MIT (or your choice — add a `LICENSE` file before publishing).
