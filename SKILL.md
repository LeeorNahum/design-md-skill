---
name: design-md
description: Create, update, and maintain a DESIGN.md file as a repository's living source of truth for its visual identity, following the open DESIGN.md token-and-prose spec and validating with its CLI. Use when starting a design system, defining or changing design tokens, or keeping DESIGN.md in sync with the implemented UI.
metadata:
  author: Leeor Nahum
  version: "1.1.0"
---

# DESIGN.md

A `DESIGN.md` at the repository root is the living source of truth for a product's visual identity. It pairs machine-readable design tokens in YAML front matter with human-readable rationale in Markdown prose. The tokens are normative; the prose explains how to apply them. Keep this one file authoritative so every agent and every session designs from the same identity instead of drifting.

This skill follows the open DESIGN.md standard. The full spec is vendored at `references/spec.md` and synced from its upstream source of truth, [google-labs-code/design.md](https://github.com/google-labs-code/design.md).

## Reference Loading

- Read `references/spec.md` before creating or editing a DESIGN.md, or whenever unsure about the token schema, the token reference syntax, the section set, or the required section order. It is the normative spec; follow it exactly.

## Modes

- Create: author a new `DESIGN.md` at the repo root from the product's brand and UI intent, following the spec's section order and token schema.
- Update: when a design decision changes, change the tokens or prose in `DESIGN.md` first, so the file stays the current truth.
- Use: before any UI work, read `DESIGN.md` and apply its exact token values rather than inventing new ones.

## Keep It In Sync

`DESIGN.md` and the implemented UI must agree, and the file is the spec the UI follows, not a record written after the fact.

- When the design changes, update `DESIGN.md` in the same change.
- When the UI contradicts the file, treat it as a UI bug unless there is a deliberate, stated reason the implementation diverged.
- When a component needs a value, take it from the file. Extend the file rather than introducing a one-off value that contradicts it.

## Validate

Validate every create or edit with the official CLI as the gate:

```bash
npx "@google/design.md" lint DESIGN.md
```

Quote the package name, since the `@` and the `.md` confuse some shells. In a `package.json` script, use the `designmd` alias instead of `design.md`. Fix errors. Warnings may remain only with a documented reason.

## Tokens

When a project has no design system or token wiring yet, let `DESIGN.md` be the generator: export its tokens and maintain that generated output as the theme.

```bash
npx "@google/design.md" export --format css-tailwind DESIGN.md
```

When a project already wires its own tokens, do not impose this export; it dictates an output shape and adds a generated file to keep in sync. Use `DESIGN.md` as the reference those existing tokens follow instead.

Compare two versions for regressions during review with `npx "@google/design.md" diff <before> <after>`.
