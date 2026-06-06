# dev

Agents that build and maintain code. A coordinated fleet: `lead` plans a task and delegates to the four specialists, then integrates their results.

## Agents

| Agent | Role | Writes? |
|---|---|---|
| [`lead`](./lead.md) | Orchestrator / tech lead — plans a task and delegates to the others | coordinates |
| [`simplifier`](./simplifier.md) | Reduces complexity, improves architecture and testability | safe-only |
| [`test-engineer`](./test-engineer.md) | Writes/runs tests, raises coverage, fixes failures | safe-only |
| [`code-reviewer`](./code-reviewer.md) | Independent review by severity (Critical→Low) | read-only |
| [`docs-keeper`](./docs-keeper.md) | Keeps docs, READMEs, and AGENTS.md accurate | safe-only |

Why these five: the four specialists cover quality, testing, review, and docs; `lead` is the glue that sequences them so you delegate one task instead of running four agents by hand. This is Cursor's recommended **orchestrator pattern**.

## How they work together

### 1. Default feature pipeline (sequential, via `lead`)

```
  ┌────────┐
  │  lead  │  reads AGENTS.md, explores, writes a plan
  └───┬────┘
      │ build (lead or a focused agent)
      ▼
  test-engineer  ── adds tests, gets suite green
      ▼
  simplifier     ── complexity pass on the diff (behavior-preserving)
      ▼
  code-reviewer  ── independent audit, findings by severity   ◄── read-only gate
      ▼
  docs-keeper    ── updates whatever the change made stale
```

`lead` does not call a task done until `code-reviewer` has run and all Critical/High findings are resolved.

### 2. Parallel review fan-out (for an existing diff)

> Review this diff and update the docs in parallel.

`code-reviewer` (read-only) and `docs-keeper` don't conflict, so they run concurrently. Keep `simplifier` and `test-engineer` sequential when they edit the same files.

### 3. Refactor loop

`simplifier → test-engineer → code-reviewer` — simplify behavior-preservingly, prove nothing broke, confirm. The safe way to act on "can we make this simpler."

### 4. Standalone

Any agent works alone: `/code-reviewer` on a PR, `/test-engineer` to backfill coverage, `/docs-keeper` after changing a command or env var.

## Shared auto-fix safety policy

Every writing agent follows the same rule:

**Auto-apply (low risk, behavior-preserving):** formatting/lint, clarifying renames within a file, removing dead code, extracting obvious duplication, adding/updating tests, doc and comment fixes, tightening types.

**Flag for approval (don't silently apply):** public API or signature changes, schema/migrations, dependency changes, anything touching auth/payments/security, cross-module refactors, deleting code with external callers, or any behavior change. `code-reviewer` never edits.

## Extending the fleet

The most common useful addition is a `debugger` (root-cause analysis on errors and test failures). Add it here and wire `lead` to delegate to it when a build or test fails.
