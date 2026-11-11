---
name: website-update
description: >-
  Update marketing website content from an app's store description, release
  notes, and changelog. Use for syncing app capabilities to marketing website
  or completing the release-copy workflow. Preserve feature coverage and
  balanced layouts, propose merging or dropping older highlights, and always
  obtain confirmation before applying website changes.
---

# Website updates

Keep each app's website accurate and selective. Translate current app positioning
into website copy; do not turn the homepage into a chronological release log.

## Sources and scope

The release-copy workflow is **changelog → release notes → app description → website**.
Use the existing [changelog](../changelog/SKILL.md),
[release-notes](../release-notes/SKILL.md), and
[store-description](../store-description/SKILL.md) skills for their stages.
Complete requested upstream work before deriving website copy. A request for one
stage does not authorize rewriting every other stage.

Locate the target website repository or directory:
- Sibling repository: e.g. `<app>-website/`
- Subdirectory: e.g. `website/`, `docs/`, `www/`
- Or user-specified path. If unsure or missing, ask for its path.

Read the selected website's instructions and working-tree status before preparing
edits. Do not create a replacement repository. Keep claims and source files separate across multiple sites. Do not update unrelated websites unless requested.

Read the selected app's files in workflow order:

1. `CHANGELOG.md` (or `lib/CHANGELOG.md`): factual changes, removals, and platform restrictions for
   the relevant release or range. Exclude `Private` work from public copy.
2. `RELEASE_NOTES.md`: user benefits and release priorities.
3. `STORE_DESCRIPTION.md`: current positioning, feature grouping, requirements,
   and compatibility language; this is the primary copy source for the website.

Older changelog entries supply context, not proof a capability still exists.
Resolve conflicting claims against current app code or canonical support assets
before presenting them as facts. Do not promote an unreleased change as available;
surface unclear release status in the proposal. If upstream copy is stale, flag
the specific correction and include it in the proposed scope instead of silently
rewriting it during a website-only request.

## Prepare a concrete proposal

Inspect the actual homepage and related copy surfaces. Discover the project's actual entry points (e.g. `app/page.tsx`, `components/features.tsx`, `components/hero.tsx`, `lib/site-metadata.ts`, or HTML/MDX templates). Check repeated claims in highlight sections, FAQs, press-kit descriptions, and metadata when relevant to the requested change.

Map material capabilities to their existing or proposed website location. Include
source references and mark each highlight as keep, rewrite, add, merge, or drop.
Flag missing important capabilities and unsupported or outdated website claims.
Feature symmetry has two parts:

- **Coverage:** the website and app description must agree on capabilities,
  availability, compatibility, and restrictions. Summarizing is fine; duplicating
  every description bullet is unnecessary. Similar positioning across sites
  does not mean advertising features that only another app has.
- **Layout:** preserve balanced feature groups, complete rows at the site's
  existing responsive breakpoints, comparable card lengths, and clear hierarchy.
  Inspect each site's actual grid or row layout; do not change the design merely to fit another bullet.

When adding a highlight, first consider replacing a weaker older highlight or
merging related ones. Prefer current differentiators and high-impact workflows;
demote redundant, niche, or baseline capabilities to supporting copy or remove
their standalone promotion. Age alone is not a reason to drop a useful feature.
Explain each merge or removal and where any still-important information remains.
Dropping a website highlight does not remove the capability from the app or
rewrite historical changelog entries. Never pad a grid with invented features.

Draft exact replacement copy and the resulting feature arrangement, including
before/after counts for affected groups. Prepare a reviewable patch in temporary
storage or show proposed text in chat before changing website files. Preserve
existing user edits and keep the patch limited to the proposed scope.

## Required confirmation

**Always ask for explicit confirmation of the concrete proposal before applying
website changes, including copy-only edits and merges or removals.** A general
request to update the website authorizes inspection and drafting, not approval
of an unseen proposal. Show the changed copy or patch, affected files, feature
merges/removals with reasons, and resulting layout first. Then ask whether to
apply those specific changes and wait for the answer.

Explain that this skill requires confirmation before application. If available,
use the user-input tool to ask. While waiting, continue only independent read-only
checks. Silence is not approval. Approval covers the reviewed proposal; ask again
if material scope or claims change. Do not ask again for an unchanged proposal
already explicitly approved.

After confirmation, apply the approved edits and verify factual consistency,
links, and responsive layout on desktop and mobile using the available preview.
Run the website's applicable existing checks/build; report any checks that could
not run. Inspect the final diff for unapproved changes. Report changed files,
feature merges/removals, and validation results.

Applying local edits does not authorize publishing. Do not push, deploy, or
trigger an automatic production deployment without explicit approval for that
action. When publishing is requested, present the verified result and deployment
target for confirmation before triggering it.

