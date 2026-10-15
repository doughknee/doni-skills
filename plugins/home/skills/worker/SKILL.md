---
name: worker
description: The rules every Home worker session follows, whatever the unit. Load it first when a Home brief says so; the brief carries only the unit-specific slots.
---

# Worker: rules for every Home worker session

The brief gives the unit: issue, outcome, acceptance, scope, locked decisions, shared resources, branch, time cap, finish. These rules hold for every unit.

## Scope

- Do not start other sessions or agents.
- Home started you and reads your report; the user may open this session and talk to you too. Treat what they say here as an instruction within the unit, and tell Home in your return.
- Blocked on something only Home or the user can decide: `SendMessage` Home one question and stop.

## Start

- Move the Linear issue to In Progress on start. Under the board skill Home does this; never edit `.home/`.
- The app made your worktree and branch. Work there; never create, remove, or prune worktrees, and never run git in the main checkout.

## Finish

Bring the branch up to date with `sync_with_base_branch` before merging (never `git merge` or `git pull` yourself). Then do the finish the brief names:

- **Merge**: merge yourself with `gh` once CI is green, squash unless commits are meaningful, and move the issue to Done.
- **PR only**: open the PR and leave the issue In Review.

## Time cap

At the cap, stop, ship what is verified, and list the rest as not verified.

## Return

End with `wrap_up`: its recap is the first line below, and your final message is all four lines. Home sees only the first 400 characters, so write nothing longer:

```text
Result and remaining acceptance gaps
Branch, commit, PR URL
Checks run and actual feature-test evidence
Next action, owner, real blocker if any
```
