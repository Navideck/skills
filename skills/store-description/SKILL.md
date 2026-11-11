---
name: store-description
description: >-
  Writes and updates store listing descriptions for mobile or desktop apps:
  front-loaded first 2–3 lines, compact scannable body, inside App Store /
  Google Play budgets (4000 full description, 80 Play short description). Use
  when updating an app description, store listing copy, or "app description", as
  opposed to release notes or changelog.
---

# Store description (app listing copy)

## Goal

The **store listing description**: short, front-loaded copy that sells an app in App Store Connect and Google Play Console. Not a feature dump, not release notes.

For **`RELEASE_NOTES.md`**, use `release-notes`. For changelogs, use `changelog`. This skill is about the **store description only**.

Release-copy workflow: **changelog → release notes → app description → website**.
For the full workflow, complete [changelog](../changelog/SKILL.md) and
[release-notes](../release-notes/SKILL.md) first. Update the description from those
sources while retaining relevant existing capabilities, then use
[website-update](../website-update/SKILL.md). Website changes require confirmation
of the concrete proposal. A description-only request stays scoped here.

## Which app, which file

Locate the canonical store description file:

- **Single-app repository**: `STORE_DESCRIPTION.md` at repository root.
- **Monorepo / multi-app repository**: `<app>/STORE_DESCRIPTION.md` (e.g. `btcam/STORE_DESCRIPTION.md`, `cinemaslate/STORE_DESCRIPTION.md`).

Rules that apply to all projects:

- Always edit that file; never keep the description only in chat, and do not create a second copy elsewhere.
- Plain text, no markdown styling — it is pasted into the stores as-is. Keep the file's existing section headings (`KEY FEATURES`, `ADDITIONAL FEATURES`, …) unless the user asks to restructure.

## Where it goes

- **App Store Connect** → app → Distribution → *Description* (+ *Promotional Text*, *Subtitle*, *Keywords*).
- **Google Play Console** → Main store listing → *Short description* / *Full description*.

`<app>/android/fastlane/metadata/android/<locale>/` is where fastlane `supply` reads metadata when in use; do not add description files there unless the user says they deliver metadata through fastlane.

## Hard limits

| Field | Store | Budget |
| --- | --- | --- |
| Full description | App Store, Play | **4000** chars |
| Short description | Play | **80** chars |
| Promotional text | App Store | **170** chars |
| Subtitle | App Store | **30** chars |
| Keywords | App Store | **100** chars |

Target **4000** — that is the cap itself, for both stores. Do not add an artificial margin unless copy contains emoji or symbols that stores count as multiple units. Existing files often sit close to the cap; when adding a line, free the same amount of room elsewhere. When user asks for description update, write the full description; only write other fields if asked.

## Top-loaded structure

The first **2–3 lines** must carry the pitch, because that is all a visitor sees before "more":

1. **Line 1 — what it is + who it is for.** e.g. "Focused multicam capture for film sets, studios, and streaming rigs."
2. **Line 2 — the single biggest benefit.** What they can now do that they could not.
3. **Line 3 (optional) — the second reason to install**, or credibility (hardware, formats, integrations).

Rules for the head:

- Treat **≤ 240 chars** as the goal for the first 3 non-empty lines. A supported-hardware or brand list may run long because it must name everything; do not split or shorten such a list to hit the guide.
- One short "<App> is…" opener is fine; do not stack preamble, history, or version talk, and no `[iOS]`-style tags.
- Play's *short description* (80 chars) is effectively a fourth head line: make it the one sentence you would say out loud.

Then the body:

- **Compact feature bullets**, grouped by workflow, 1 line each, benefit-led (`Thing — why it matters`) like release notes. Keep bullet lines short (≈100 chars).
- Paragraph-style alternative: some apps write the body as short paragraphs between headings instead. Keep those to 2–4 sentences.
- Close with **requirements/compatibility** (supported devices, OS floor, formats) and **one** contact/support line.
- **Cut, do not compress**: fewer bullets beats dense paragraphs. Model/hardware lists are expected to be the bulk of a near-cap file — keep prose lean around them.
- Plain text for App Store (no markdown, no styling). Play renders a small set of tags (`<b>`, `<i>`, `<u>`); avoid them unless there is a real reason. No emoji walls, no all-caps lines, no keyword stuffing.

## Sources of truth

- Where the app has a machine-readable support list asset (e.g. camera compatibility or device matrices), sync against that canonical asset.
- Otherwise, write from real capability: user's brief, `RELEASE_NOTES.md`, `CHANGELOG.md`, or the app code. **Do not invent features**, certifications, or device support.

## Validate before handing over

Pass the path to `STORE_DESCRIPTION.md`:

```bash
FILE="STORE_DESCRIPTION.md"  # or <app>/STORE_DESCRIPTION.md
FILE="$FILE" python3 <<'PY'
from pathlib import Path
import os, sys

path = Path(os.environ["FILE"])
text = path.read_text(encoding="utf-8").rstrip("\n")
lines = [l for l in text.splitlines() if l.strip()]

head = "\n".join(lines[:3])
total = len(text)
longest = max((len(l) for l in lines[3:] if not l.startswith("- ")), default=0)

print(f"{path}")
print(f"head (first 3 non-empty lines): {len(head)} chars  [goal <= 240, list line excepted]")
print(f"longest non-bullet line: {longest} chars  [bullet files: target <= 100]")
print(f"total: {total} chars  [limit 4000]")

bad = False
if total > 4000:
    print("OVER STORE LIMIT by", total - 4000); bad = True
if longest > 100:
    print("note: a prose line is over 100 chars")
sys.exit(1 if bad else 0)
PY
```

Also check any Play *short description* (80 chars) before pasting:

```bash
python3 -c "import sys; s=input().strip(); print(len(s), 'chars [limit 80]'); sys.exit(1 if len(s) > 80 else 0)"
```

## Checklist

- [ ] Edited the right app's **`STORE_DESCRIPTION.md`** (not only in chat).
- [ ] Pitch in the **first 2–3 lines** (list line excepted); no stacked preamble.
- [ ] Full description ≤ 4000 chars and lean; Play short description ≤ 80. Bullet files: lines ≈100 chars; paragraph-style files kept to 2–4 sentences.
- [ ] Domain-specific support list mirrored where one exists.
- [ ] Benefit-led bullets, no invented features, no platform tags.
- [ ] Requirements/support line present where relevant.
- [ ] Character counts run and reported, not eyeballed.

