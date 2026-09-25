# doni-skills

Doni's skills, packaged as a Claude Code plugin marketplace.

## Plugins

| Plugin | What it does | Run it |
|---|---|---|
| `home` | Project home base: keeps projects moving, coordinates workers, tracks work in Linear, and ships verified results. | `/home:home` |

## Install

```
/plugin marketplace add doughknee/doni-skills
/plugin install home@doni-skills
```

## Get updates

Every push to `main` is a new release.

Open `/plugin`, go to **Marketplaces**, select `doni-skills`, and choose **Enable auto-update**. Or update by hand with `/plugin marketplace update doni-skills`.

## Layout

```
.claude-plugin/marketplace.json        marketplace catalog
plugins/home/.claude-plugin/plugin.json   plugin manifest
plugins/home/skills/home/SKILL.md         the skill itself
```

To change the skill, edit `plugins/home/skills/home/SKILL.md` and push.
