---
name: board
description: A Linear-shaped issue board that lives in the repo, for projects where Linear is not connected. Use when the home skill needs to create, read, update, or comment on an issue and Linear's MCP tools are unavailable, or when the user asks to see or edit the local board.
---

# Board: Linear in the repo

One directory, `.home/`, committed with the code. It gives Home the same objects Linear does, so the home skill's rules apply unchanged: search before creating, one brief per issue, statuses mean the same thing, Done needs verified evidence.

## Layout

```text
.home/
  board.md          generated index, one line per open issue
  register.md       the Home register
  issues/
    MYP-1.md        one file per issue
    MYP-2.md
```

The key prefix is the repo name's first three letters, uppercased. Numbers are sequential and never reused. Branch name for an issue is its key lowercased plus a slug, for example `myp-2-sync-retry`.

## Issue file

```markdown
---
key: MYP-2
title: Sync API retries on 5xx
status: Todo
created: 2026-09-25
owner:
branch: myp-2-sync-retry
pr:
---

## Brief
Outcome: <what must be true when done>
Acceptance:
- <observable check>
Scope: <files/dirs>
Test path: <how to see it work>
Finish: <merge | PR only>

## Log
- 2026-09-25 created from user request
```

Statuses are exactly `Backlog`, `Todo`, `In Progress`, `In Review`, `Done`, `Canceled`. Comments are dated lines under `## Log`, newest last. Nothing else is invented; if Linear would not have a field for it, it goes in the log.

## Operations

| Linear | Board |
|---|---|
| Initialize | Create `.home/issues/`, an empty `board.md` and `register.md`, commit them |
| Search issues | Grep `.home/issues/` for the title or key |
| Create issue | Next number, new file from the template above, one log line |
| Move status | Edit `status:` in the frontmatter, add a log line |
| Comment | Append a dated line under `## Log` |
| Read brief | The `## Brief` section |
| Board view | Regenerate `board.md`: one line per issue not Done or Canceled, grouped by status |
| Home register | `.home/register.md`, same format as in the home skill |

Every write is followed by regenerating `board.md` and committing `.home/` with a one-line message such as `board: MYP-2 → In Review`. Workers commit their own issue file changes on their branch; Home commits the rest on main.

## Rules

- Never delete an issue file. Canceled is a status.
- Never renumber. A gap is fine.
- Keep `.home/` out of `.gitignore`. The board is only useful shared.
- If Linear becomes available later, offer once to migrate: create each open issue in Linear with its brief and log, mark the file `status: Migrated` with the Linear key in the log, and stop using the board.
