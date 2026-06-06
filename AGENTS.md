# AGENTS.md

Baseline agent instructions. Copy this into a new project, fill in the project-specific sections at the top, and keep the standards below. Agents read this file first; project specifics override the generic guidance.

## Project

- **What it is:** <one-line description>
- **Stack:** <languages / frameworks / runtime>
- **Structure:** <key directories and what lives in them>

## Commands

- **Install:** `<...>`
- **Dev:** `<...>`
- **Build:** `<...>`
- **Test:** `<...>`
- **Lint / format:** `<...>`

Prefer these over ad-hoc commands. If a command here is wrong, fix it as part of your change.

## Boil the ocean

The marginal cost of completeness is near zero with AI. Do the whole thing. Do it right. Do it with tests. Do it with documentation. Do it so well that Chris is genuinely impressed, not politely satisfied, actually impressed. Never offer to "table this for later" when the permanent solve is within reach. Never leave a dangling thread when tying it off takes five more minutes. Never present a workaround when the real fix exists. The standard isn't "good enough" it's "holy shit, that's done." Search before building. Test before shipping. Ship the complete thing. When Chris asks for something, the answer is the finished product, not a plan to build it. Time is not an excuse. Fatigue is not an excuse. Complexity is not an excuse. Boil the ocean.

## Coding agent guidelines

Behavioral guidelines for agents editing this repo. Bias to caution over speed; use judgment on trivial tasks.

- **Think before coding:** Do not assume; surface trade-offs; ask when unclear or when multiple interpretations exist.
- **Simplicity first:** Minimum code that solves the problem—no speculative features, one-off abstractions, or unnecessary configurability; rewrite obvious bloat.
- **Surgical changes:** Touch only what you must; match existing style; do not "clean up" unrelated code. Remove imports/vars/functions only when **your** change made them unused.
- **No unnecessary legacy/back-compat:** Do **not** add backward-compatibility shims, deprecation aliases, "legacy" fallbacks, dual code paths, or migration glue unless explicitly required. Clean code beats back-compat. When in doubt, **ask first** — propose the clean break and the back-compat option, and let the user choose.
- **Goal-driven execution:** Define verifiable success (e.g. failing test → green); for multi-step work, a short numbered plan with a verify step per item helps.
- **Nested guides:** When a subdirectory has its own `AGENTS.md`, read and follow it before marking work in that directory complete.
- **Keep build config in sync:** When adding a dependency or package, update every build/deploy config that needs it (Dockerfiles, bundler aliases, deploy manifests), not just the package manifest. A passing local build is not proof it ships.
- **Cursor subagents:** Versioned under `.cursor/agents/`; commit them with the repo like any other team config.
