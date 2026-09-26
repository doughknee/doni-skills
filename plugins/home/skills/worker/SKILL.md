---
name: worker
description: The rules every Home subagent worker follows, whatever the unit. Load it first when a Home brief says so; the brief carries only the unit-specific slots.
---

# Worker: rules for every Home subagent

The brief gives the unit: issue, outcome, acceptance, scope, locked decisions, shared resources, branch, time cap, finish. These rules hold for every unit.

## Scope

- Do not start other agents.
- Report only to Home, and end when your task ends.

## Start

- Move the Linear issue to In Progress on start. Under the board skill Home does this; never edit `.home/`.
- Your worktree already exists. Check out the given branch inside it.
- Never create, remove, or prune worktrees, and never run git in the main checkout.

## Finish

Rebase onto main before merging. Then do the finish the brief names:

- **Merge**: merge yourself with `gh` once CI is green, squash unless commits are meaningful, and move the issue to Done.
- **PR only**: open the PR and leave the issue In Review.

## Time cap

At the cap, stop, ship what is verified, and list the rest as not verified.

## Return

Return exactly this, nothing longer:

```text
Result and remaining acceptance gaps
Branch, commit, PR URL
Checks run and actual feature-test evidence
Next action, owner, real blocker if any
```
