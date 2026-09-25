# doni-skills

Doni's skills, packaged as a plugin marketplace that works in both Claude Code and Codex.

## Plugins

| Plugin | What it does | Run it |
|---|---|---|
| `home` | Project home base: keeps projects moving, coordinates workers, tracks work in Linear, and ships verified results. | Claude Code: `/home:home` · Codex: `$home` |

## Install

**Claude Code** (in a session):

```
/plugin marketplace add doughknee/doni-skills
/plugin install home@doni-skills
```

**Codex** (in a terminal):

```
codex plugin marketplace add doughknee/doni-skills
codex plugin add home@doni-skills
```

## Get updates

Every push to `main` is a new release.

**Claude Code:** open `/plugin`, go to **Marketplaces**, select `doni-skills`, and choose **Enable auto-update**. Or update by hand with `/plugin marketplace update doni-skills`.

**Codex:**

```
codex plugin marketplace upgrade doni-skills
codex plugin add home@doni-skills
```

## Layout

```
.claude-plugin/marketplace.json        marketplace catalog (read by both Claude Code and Codex)
plugins/home/.claude-plugin/plugin.json   Claude Code manifest
plugins/home/.codex-plugin/plugin.json    Codex manifest
plugins/home/skills/home/SKILL.md         the skill itself (shared)
```

To change the skill, edit `plugins/home/skills/home/SKILL.md` and push. Both harnesses read the same file.
