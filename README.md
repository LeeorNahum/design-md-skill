# design-md

A slim Agent Skill for creating, updating, using, and validating a `DESIGN.md`, the open token-and-prose file that serves as a repository's living source of truth for its visual identity.

It redirects to one vendored reference, the full spec, kept in sync with its upstream source of truth, [google-labs-code/design.md](https://github.com/google-labs-code/design.md), so every repo designs from the same standard.

## Install

Add as a submodule into your agent's skills directory:

```bash
git submodule add https://github.com/LeeorNahum/design-md-skill.git .agents/skills/design-md-skill
```

## What's inside

| File | Purpose |
| --- | --- |
| `SKILL.md` | How to create, update, use, and validate a DESIGN.md |
| `references/spec.md` | The full DESIGN.md spec, vendored from upstream |
| `scripts/sync.mjs` | Pulls `docs/spec.md` from the upstream repo |
| `.github/workflows/sync-upstream.yml` | Weekly and on-demand sync, commits only when the spec changed |

## Stays up to date

`references/spec.md` is vendored from `google-labs-code/design.md` `docs/spec.md`. The sync workflow runs weekly and on demand, and records the exact upstream commit in each sync commit. Validate any DESIGN.md with the official CLI: `npx "@google/design.md" lint DESIGN.md`.
