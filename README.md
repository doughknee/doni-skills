# doni-skills

Doni's skills, packaged as a Claude Code plugin marketplace.

## Plugins

| Plugin | What it does | Run it |
|---|---|---|
| `home` | Project home base: keeps projects moving, coordinates workers, tracks work in Linear, and ships verified results. | `/home:home` |
| `home` → `linear` | Linear as the board: first-run project setup, issue lifecycle, brief format. Also triggers on its own when an issue key is mentioned. | `/home:linear` |
| `home` → `board` | Linear-shaped board in `.home/` for repos without the Linear connector. Home switches to it after the opt-out phrase. | `/home:board` |
| `home` → `worker` | The rules every Home subagent worker follows: worktree and git limits, finish, time cap, return format. Workers load it first from their brief. | `/home:worker` |

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
plugins/home/skills/home/SKILL.md         the home skill
plugins/home/skills/linear/SKILL.md       Linear as the board
plugins/home/skills/board/SKILL.md        the local board fallback
plugins/home/skills/worker/SKILL.md       rules for every subagent worker
```

## Working on the skills

Do not edit the marketplace copy under `~/.claude/plugins/marketplaces/doni-skills`; anything inside `~/.claude` prompts on every file edit and drags worker worktrees in there too. Work in a normal clone (for example `~/Documents/.code/doni-skills`), push to `main`, then refresh the installed copy:

```
claude plugin marketplace update doni-skills
claude plugin update home@doni-skills
```

and restart the app.
