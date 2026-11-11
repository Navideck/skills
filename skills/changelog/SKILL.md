---
name: changelog
description: >-
  Maintains CHANGELOG.md (or lib/CHANGELOG.md) for any app or multi-app
  repository: version blocks, Added/Improved/Fixed/Private sections, and factual
  bullets from git or PRs. Use when updating a changelog, drafting release
  history for developers, or when the user mentions CHANGELOG.md.
---

# Changelog (`CHANGELOG.md` / `lib/CHANGELOG.md`)

## Goal

Accurate **developer-facing** history: what shipped, grouped for maintainers and support. Not marketing copy.

For user-facing store copy, use the **`release-notes`** skill. This skill is about the app's changelog only.

Release-copy workflow: **changelog → release notes → app description → website**.
When the full workflow is requested, finish this stage first, then use
[release-notes](../release-notes/SKILL.md),
[store-description](../store-description/SKILL.md), and
[website-update](../website-update/SKILL.md) in order. Website changes require
confirmation of the concrete proposal. A changelog-only request stays scoped here.

## Which app, which file

Locate the canonical changelog:

- **Single-app repository**: `CHANGELOG.md` at repository root, or `lib/CHANGELOG.md` (common in Flutter/Dart).
- **Monorepo / multi-app repository**: `<app>/CHANGELOG.md` or `<app>/lib/CHANGELOG.md` (e.g. `btcam/lib/CHANGELOG.md`, `cinemaslate/lib/CHANGELOG.md`).
- Version source: read from `<app>/pubspec.yaml`, `package.json`, `Cargo.toml`, or app build config as a hint, not as the final release number.

Rules that apply to all projects:

- Always edit that app's file; never keep the entry only in chat, and do not write one app's changes into another app's changelog.
- One entry per release of that app, covering **that app's** changes plus shared work that ships in it.
- In multi-app repos sharing tags, match releases to apps by the app's version definition.
- Match the file's existing layout pattern: usually `# Changelog`, `## [x.y.z] - YYYY-MM-DD`, an optional `**Git tag:** —` line, then section headings.

## Gather facts

- **Version** (e.g. `1.2.0`) and **date** `YYYY-MM-DD` — ask the user if either is unstated; take version hints from the project manifest file.
- **Change set**: `git log --oneline <previous-tag>..HEAD` for the tag that last shipped that app (`git tag --sort=-creatordate`), plus `git show --stat` for commits whose scope is unclear. Or ask the user. **Do not invent** shipped features.
- **Scope to the app**: list only that app's user-visible changes. Other app work stays out. Shared-package and tooling work goes under **`### Private`** — there is no user-facing entry for it.

## Update the file

- Add `## [x.y.z] - YYYY-MM-DD` **below** any newer unreleased section (e.g. a future stub) and **above** the last shipped version — match the file's existing pattern.
- Sections, in order:
  - **`### Added`**
  - **`### Improved`**
  - **`### Fixed`**
  - **`### Private`** — tooling, CI, dependency churn, internal refactors, store-copy/skill docs, localization string churn with no user-visible behavior change, etc.
- Keep the sections the file already shows, even when one ends up empty. Omit a section only if the file's existing entries omit it in the same case.
- Bullets: **short**, **factual**, same tone as surrounding entries. Name models, brands, and platforms explicitly — that is what support and compatibility questions hinge on.
- **Platform-specific changes**: prefix with tags when it helps scanning: `[iOS]`, `[Android]`, `[Web]`, `[macOS]`, `[Windows]`, `[Linux]`, `[Desktop]` as used elsewhere in the file.
- Do **not** paste long marketing paragraphs here; keep lists scannable.

## Checklist

- [ ] Edited the right app's changelog file (not only in chat), with that app's changes only.
- [ ] Version line and date match what the user is shipping.
- [ ] Sections present in order; nothing user-visible buried only under Private without reason.
- [ ] Platform tags on changelog bullets where the fix/feature is platform-specific.
- [ ] No fictional changes.

