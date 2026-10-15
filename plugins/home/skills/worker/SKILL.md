---
name: worker
description: The rules every Home worker follows, whatever the unit. Load it first when a feature brief says so; the brief carries only the unit-specific slots.
---

# Worker: one unit in a feature's checkout

The brief gives the unit: what it produces, acceptance, scope, locked decisions, shared resources, checks to run, time cap. You share the feature session's checkout with other workers; these rules keep you out of each other's way.

## Scope

- Do not start other sessions or agents.
- The feature session started you and reads your report; the user may open this session and talk to you too. Treat what they say here as an instruction within the unit, and tell the feature in your return.
- Blocked on something only the feature or the user can decide: `SendMessage` the feature one question and stop.

## Work

- Edit only the files in your scope. The checkout has other workers' edits in progress; leave every other file alone, including ones that look wrong.
- **No git.** Do not branch, stage, commit, stash, or pull. The feature session commits after it verifies the wave.
- Run exactly the checks the brief names. Do not run the dev app or claim a device unless the brief says you own it.
- Do not touch the board.

## Time cap

At the cap, stop, and list what is not verified.

## Return

End with `wrap_up`: its recap is the first line below, and your final message is all four lines. The feature sees only the first 400 characters, so write nothing longer:

```text
Result and remaining acceptance gaps
Files changed
Checks run and actual evidence
Next action, real blocker if any
```
