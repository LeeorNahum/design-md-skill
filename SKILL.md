---
name: "design-md"
description: "Use when building or restyling UI, components, layouts, colors, typography, spacing, or themes in a repository that has, or should have, a DESIGN.md, including using its tokens and identity to guide external visual assets such as a logo or marketing material that need to stay on-brand. Use when starting a design system for a repository, when defining or changing design tokens that DESIGN.md should record, or when reading DESIGN.md and keeping it in sync with the implemented UI. Covers creating, updating, applying, and validating DESIGN.md, the token-and-prose file that is a repository's living source of truth for its visual identity."
compatibility: "Requires Node.js 18 or later, npm, and network access when the official CLI is not cached."
metadata:
  author: "Leeor Nahum"
  version: "1.4.0"
---

# DESIGN.md

A `DESIGN.md` at the repository root is the living source of truth for a product's visual identity. It pairs machine-readable design tokens in YAML front matter with human-readable rationale in Markdown prose. The tokens are normative. The prose explains how to apply them. Keep this one file authoritative so every agent and every session designs from the same identity instead of drifting.

This skill follows the open DESIGN.md standard. The full spec is vendored at [spec.md](references/spec.md) and synced from its upstream source of truth, [google-labs-code/design.md](https://github.com/google-labs-code/design.md).

## Reference Loading

- Read [spec.md](references/spec.md) before creating or editing a DESIGN.md, or whenever unsure about the token schema, the token reference syntax, the section set, or the required section order. It is the normative spec. Follow it exactly.

## Modes

- Create: author a new `DESIGN.md` at the repo root from the product's brand and UI intent, following the spec's section order and token schema.
- Update: change the tokens or prose in `DESIGN.md` as Keep It In Sync describes.
- Use: before any UI work, read `DESIGN.md` and apply its exact token values rather than inventing new ones.

## Keep It In Sync

`DESIGN.md` and the implemented UI must agree, and the file is the spec the UI follows, not a record written after the fact.

- When the design changes, update `DESIGN.md` first, in the same change, so the file stays the current truth.
- When the UI contradicts the file, treat it as a UI bug unless `DESIGN.md` records the divergence as a deliberate exception.
- When a component needs a value, take it from the file. Extend the file rather than introducing a one-off value that contradicts it.

## It Guides, It Does Not Cage

`DESIGN.md` exists to stop drift, not to prevent better design. It is a living file, and whoever designs against it has the standing to change it: the same judgment that authored it can revise it. Take it seriously and take it with a grain of salt.

So when a genuinely better choice conflicts with the file, neither violate it quietly nor abandon the choice. Make the change and update the file in the same pass, so the identity stays one thing. Treat a rule as binding when the reason behind it still holds, and rewrite the rule when it does not. A stated exception belongs in the file. An unstated one is just drift.

## Validate

Validate every create or edit with the official CLI as the gate:

```bash
npx --yes --package "@google/design.md" designmd lint DESIGN.md
```

The command selects Google's package explicitly and invokes its dot-free `designmd` executable. Use this form on every platform, including in a `package.json` script. Fix errors. Warnings may remain only with a documented reason.

## Tokens

When a project has no design system or token wiring yet, let `DESIGN.md` be the generator: export its tokens and maintain that generated output as the theme.

```bash
npx --yes --package "@google/design.md" designmd export --format css-tailwind DESIGN.md
```

When a project already wires its own tokens, do not impose this export. It dictates an output shape and adds a generated file to keep in sync. Use `DESIGN.md` as the reference those existing tokens follow instead.

Compare two versions for regressions during review with `npx --yes --package "@google/design.md" designmd diff <before> <after>`.
