---
name: feature
description: One feature, one PR, from brief to merge, run by a feature session that Home started. Load it first when a Home brief says so; the brief carries the issue, acceptance, scope, and where the session runs.
---

# Feature: one PR from brief to merge

Home gave you one issue and one PR. You own its branch, split the work into units, run workers in your checkout when that is faster than doing it yourself, verify between waves, commit, and at the end audit once, open the PR, and merge. Setup is paid once at the start and audit once at the end; nothing in between pays either.

## Start

- Move the issue to In Progress. Under the board skill Home does this; never edit `.home/`.
- **Where: checkout.** You are in the project's main checkout, which Home confirmed free. Create the branch from `origin/main` here. No environment setup.
- **Where: worktree.** The app made your worktree and branch. Set the environment up once, following the repo's `CLAUDE.md` under `## Home` if it names a bootstrap; if setup takes more than a few minutes and nothing names a bootstrap, say so in your return so Home records one.
- Never create, remove, or prune worktrees, and never run git outside your own checkout.

## Size, then split

Split the feature into units: file-disjoint parts, each with an observable check. Then decide who does them.

- **Fewer than three units that can run at the same time: do it yourself.** Writing briefs and starting sessions costs minutes; for a small feature the parallel path is the slow one.
- **Three or more: workers, in waves.** Wave 1 is every unit with no unmet dependency and no file overlap. A later wave starts when its dependencies are verified and committed.
- Same file means same unit. One worker at a time runs the dev app or holds a device; the rest do code, tests, or docs. Cap four workers.
- **Model per unit:** `sonnet` by default, `haiku` for mechanical copy and repetitive replacements, `opus` only for an open-ended investigation and with a stated reason.

## Workers

Every worker gets the `worker` skill and this brief. Copy it into the `start_session` `prompt` and fill every slot; `background` carries the feature's outcome in a line and what the other running units own:

```text
You are a worker for <KEY> <title>. Load the home:worker skill first (Skill tool) and follow it.
Unit: <what this unit produces>
Acceptance: <observable checks, one per line>
Scope: <files you own>. Do not touch: <files owned by other units>.
Locked decisions: <choices already made; do not reopen>
Shared resources you own: <dev app | device | none>
Checks to run: <exact commands>
Time cap: <N> minutes
```

`start_session` with `initiation: "user_asked"`, `context: "fresh"`, `use_worktree: false` (the worker shares your checkout), `model`, `title: "<KEY> · <unit>"`, `name: "<key>-<n>"`. Record the returned `local_…` id. Continue a worker through `SendMessage` rather than starting over; a worker that messages you because it is blocked gets an answer, or the question goes to Home.

**You are the only session that runs git here.** Workers edit files and stop. Two sessions committing in one checkout race each other.

## Between waves

Only once every worker in the wave has reported, because tests run against half-edited files mean nothing:

1. Run the units' checks.
2. Read the wave's diff against its units: nothing outside scope, nothing missing.
3. Commit, only the files the units own. Leave anything else in the checkout alone.
4. Fix a small gap yourself. For a real one, send the worker one retry with the failure attached; if that fails too, stop and report to Home.
5. Start the next wave.

## Finish

1. Every acceptance line observed, and the negative path where one exists.
2. Bring the branch up to date: `sync_with_base_branch` in a worktree; `git merge origin/main` in the checkout. Resolve conflicts yourself.
3. Push and open the PR with the outcome and the acceptance evidence. Attach it to the issue.
4. **Audit once, the whole PR:** the full diff against scope and acceptance, the full test suite, CI green. Fix here, not in a worker.
5. Merge, squash by default, delete the remote branch. In the checkout, return it to main and pull.
6. Move the issue to Done with a comment linking the merge commit.

Do not archive your workers; Home archives the family after it verifies.

## Time cap

At the cap, stop, push what is verified, open the PR as a draft, and list the rest as not verified.

## Return

End with `wrap_up`: its recap is the first line below, and your final message is all four lines. Home sees only the first 400 characters, so write nothing longer:

```text
Result and remaining acceptance gaps
PR URL and merge commit
Checks run and actual feature-test evidence
Next action, owner, real blocker if any
```
