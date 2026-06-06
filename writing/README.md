# writing

Agents for non-code writing that lives alongside the codebase. Placeholder category — add agents as you build them.

## Suggested agents

| Agent | Role |
|---|---|
| `changelog` | Generates a changelog entry from merged changes, grouped and human-readable |
| `release-notes` | Drafts user-facing release notes from a set of changes |
| `pr-describer` | Writes a clear PR title and description from the diff |
| `announcer` | Drafts internal/external announcements for shipped features |

Note: single-shot writing tasks (e.g. "format this changelog") are often better as a Cursor *skill* than a subagent. Use an agent here when the task needs its own context window or multi-step reasoning. Follow the repo conventions: focused `description`, read `AGENTS.md` first.
