# Navideck Skills

A collection of reusable skills for AI coding agents (Antigravity, Claude Code, etc.) designed to streamline software release and marketing workflows.

## The Release Pipeline

These skills work together in a structured 4-stage release workflow:

```text
CHANGELOG.md ──> RELEASE_NOTES.md ──> STORE_DESCRIPTION.md ──> Website copy
```

Each stage builds on the previous, filtering internal technical details into user benefits, store listing copy, and public website highlights.

## Skills

| Skill | Description | Target Files |
|-------|-------------|--------------|
| **[`changelog`](skills/changelog/SKILL.md)** | Developer-facing release history. Gathers changes from git logs/PRs into `Added`, `Improved`, `Fixed`, and `Private` sections. | `CHANGELOG.md`, `lib/CHANGELOG.md` |
| **[`release-notes`](skills/release-notes/SKILL.md)** | User-facing release notes for App Store, Google Play, blogs, and email. Benefit-led, platform-agnostic, and scannable. | `RELEASE_NOTES.md` |
| **[`store-description`](skills/store-description/SKILL.md)** | App Store and Google Play listing copy. Top-loaded 2–3 line pitch, budget enforcement (4000 char full description, 80 char short description). | `STORE_DESCRIPTION.md` |
| **[`website-update`](skills/website-update/SKILL.md)** | Syncs marketing website copy with current store description and release notes. Enforces feature symmetry and requires confirmation before applying changes. | `app/page.tsx`, `components/features.tsx`, etc. |

## Installation

### Antigravity / Gemini CLI

#### Machine-global (recommended)
Clone or symlink the skills into `~/.gemini/config/skills/`:

```bash
git clone https://github.com/Navideck/skills.git ~/.agents/skills/navideck-skills
# Link desired skills into Antigravity config:
ln -s ~/.agents/skills/navideck-skills/skills/* ~/.gemini/config/skills/
```

#### Project-level
Copy or symlink into your repository's `.agents/skills/` folder:

```bash
mkdir -p .agents/skills
cp -R path/to/skills/skills/* .agents/skills/
```

### Other Coding Agents (Claude Code, Cursor, Codex)

Install into your user or workspace `.agents/skills/` directory:

```bash
# Global
mkdir -p ~/.agents/skills
cp -R path/to/skills/skills/* ~/.agents/skills/

# Project
mkdir -p .agents/skills
cp -R path/to/skills/skills/* .agents/skills/
```

## License

MIT License. See [LICENSE](LICENSE) for details.
