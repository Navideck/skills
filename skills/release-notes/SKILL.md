---
name: release-notes
description: >-
  Maintains RELEASE_NOTES.md for any app: user-facing release copy,
  benefit-led lines, platform-tag stripping, unified platform-agnostic notes
  (no per-channel length limits), and prioritization by user impact. Use for
  store “what’s new”, public release blurbs, or when the user mentions
  RELEASE_NOTES.md without asking for CHANGELOG.md only.
---

# Release notes (`RELEASE_NOTES.md`)

## Goal

**User-facing** text: stores, blog snippets, email, etc. Prioritize **high-impact** features and fixes and clear **benefits**, not internal detail.

For developer-facing changes, use **`changelog`**. This skill is about the app's **`RELEASE_NOTES.md`** only.

Release-copy workflow: **changelog → release notes → app description → website**.
For the full workflow, complete [changelog](../changelog/SKILL.md) first; derive
these notes from that app's relevant changelog section, then continue with
[store-description](../store-description/SKILL.md) and
[website-update](../website-update/SKILL.md). Website changes require confirmation
of the concrete proposal. A release-notes-only request stays scoped here.

## Which app, which file

Locate the canonical release notes:

- **Single-app repository**: `RELEASE_NOTES.md` at repository root.
- **Monorepo / multi-app repository**: `<app>/RELEASE_NOTES.md` (e.g. `btcam/RELEASE_NOTES.md`, `cinemaslate/RELEASE_NOTES.md`).
- Title heading: `# <App Name> Release Notes`.

Rules that apply to all projects:

- Always edit that app's file; never keep the notes only in chat, and never publish one app's notes as another's.
- Notes are per app: one app's section names that app's own features.

## Source material

Use **`git log` / PRs**, an existing **changelog section**, or the user’s bullet list. Do not invent features.

## Unified, platform-agnostic

Each app ships **one** set of release notes for all destinations (Google Play, App Store, blog, email). Write them **platform-agnostic**:

- **No per-channel drafts, no length caps, no per-locale variants.** Do not produce Play-short vs App Store-long copies or count Unicode scalars.
- Still keep the block **short and scannable** — a handful of benefit-led lines. Fitting Play’s 500-scalar budget naturally is a bonus, not a requirement.
- Avoid platform-specific phrasing (`[iOS]`, “on iPhone”, etc.) unless the feature is genuinely platform-specific and needs plain-language qualification.

## Update the app's `RELEASE_NOTES.md`

- New section **at the top** (after the app’s title line), matching house style:

  ```markdown
  ## x.y — Mon DD, YYYY

  [Optional one-line hook]

  Feature — Benefit-oriented line
  ...

  ---
  ```

- **Heading**: use the same **version + date style** as neighboring sections in *that* file (e.g. `4.7.1 — September 10, 2026`). Drop a trailing `.0` only if the file already does.
- **From changelog or commits**: rewrite into **benefit-led** lines (`Thing — Why it matters`). Name brands and supported models where the user has to check compatibility.
- **Strip bracket platform prefixes** from changelog-style tags: `[iOS]`, `[Android]`, `[Web]`, `[macOS]`, `[Windows]`, `[Linux]`, `[Desktop]` (case-insensitive inside brackets). **Do not** lead release lines with those tags.
  - If platform still matters, use plain language (e.g. “Smoother discovery on iPhone”).
- **Tone**: confident, clear; avoid § and heavy jargon. Focus on **what changed**, no misleading hype.
- **Length**: no channel cap — keep the section **short and scannable**.

## Prioritize (impact + positioning)

1. New capabilities users **notice** (integrations, hardware, major UI).
2. Workflow wins (multicam, timecode, sync, capture, pro/value messaging).
3. High-visibility fixes (crashes, data issues, common paths, big brands).
4. “Stability improvements” **only** as a **last** line if space remains — not instead of a headline item.

**Omit or demote:** refactors, lint/tests/CI, dependency bumps, niche edge cases, and **changelog `### Private`** items unless truly user-visible.

## Validate length (informational)

No cap is enforced, but for a quick sanity check, measure the new section from its `## …` heading through the **first** following `---` (inclusive). Pass the release notes path and exact heading:

```bash
FILE="RELEASE_NOTES.md"                 # or <app>/RELEASE_NOTES.md
NEEDLE="## 1.2.0 — September 10, 2026"  # exact new heading
FILE="$FILE" NEEDLE="$NEEDLE" python3 <<'PY'
from pathlib import Path
import os, sys

path = Path(os.environ["FILE"])
text = path.read_text(encoding="utf-8")
needle = os.environ["NEEDLE"]
start = text.find(needle)
if start == -1:
    sys.exit("error: heading not found in " + str(path) + ": " + needle)
end = text.find("\n---", start)
if end == -1:
    sys.exit("error: --- after section not found")
block = text[start : end + 5]
n = len(block)
print(f"{path}: {n} Unicode scalars")
if n > 500:
    print("OVER 500 SCALARS by", n - 500)
    sys.exit(1)
PY
```

The script exits 1 when the section exceeds 500 scalars — that is **informational only**; do not trim or restructure the notes to force it under 500.

## Checklist

- [ ] Edited the right app's **`RELEASE_NOTES.md`** (not only in chat).
- [ ] New section at top; `Feature — …` style; **no** `[Platform]` **prefixes**.
- [ ] Unified single draft per app — no per-channel caps, no per-locale variants, short and scannable.
- [ ] No fictional features; changelog **Private** items excluded unless user-visible.

## Locales

Release notes are **unified** — one copy across languages and channels. Do not edit `.arb` files or per-locale notes unless the user explicitly asks.

