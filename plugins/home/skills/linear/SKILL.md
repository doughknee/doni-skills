---
name: linear
description: How Home and any other session use Linear as the project board. Use when a Linear issue key is mentioned (e.g. REL-12), when the user reports a bug, TODO or "we should" during work, when work is finished and needs its issue updated, or when the home skill needs the board and Linear's MCP tools are available.
---

# Linear: the board

Linear is present when its MCP tools (`list_issues`, `save_issue`, `list_projects`, and so on) are available. If they are not, this skill does not apply; the home skill decides between asking for the connector and the `board` skill.

## First run on a repo

Once per repository, before any issue work:

1. Find the project. Search projects for the repository name. If the repo's `CLAUDE.md` names a team or project, that wins.
2. If none matches, list teams. One team: use it. Several: ask the user once which team owns this repo.
3. Create a project named after the repository in that team.
4. Create a document in the project named `Home register`, empty, for the home skill.
5. Apply any labels the repo's `CLAUDE.md` requires to every issue created from here on.

The project is found again next time by the same search, so nothing needs to be stored. If the repo's `CLAUDE.md` says to use outcome projects instead of one per repo, follow it and never create a catch-all.

## Lifecycle

- **An issue key is mentioned to start work.** Fetch it, move it to In Progress, and use its `gitBranchName` for the branch.
- **A bug, TODO, or "we should" comes up mid-work.** Search first; if nothing matches, create the issue in Backlog in this repo's project, then tell the user the key. Do not ask permission for this.
- **Work is finished and committed.** Comment a short summary with the commit or PR link and move the issue to In Review, or to Done when the work is merged and verified.
- **Session end.** Every issue touched reflects reality: status, a last comment if anything changed, nothing left In Progress that is not.
- **Never** delete or archive an issue without the user asking.

Statuses mean: Backlog is an idea or unverified report. Todo is ready and specified, not started. In Progress has an owner working. In Review has a PR open. Done is merged and verified.

## The issue brief

One current brief per issue, kept in the issue description and updated when scope changes:

```text
Outcome: <what must be true when done>
Acceptance:
- <observable check>
Scope: <files/dirs>
Test path: <how to see it work>
Finish: <merge | PR only>
```

Comments hold evidence: start, real blockers, review readiness, verified completion with links. Routine tool calls, unchanged polls, and individual edits do not get comments.

## Operations

| Need | Tool |
|---|---|
| Find issues | `list_issues` with a query, or `get_issue` by key |
| Create or update an issue | `save_issue` |
| Change status | `save_issue` with the state; `list_issue_statuses` when unsure of names |
| Comment | `save_comment` |
| Find or create the project | `list_projects`, `save_project` |
| Home register | `get_document` / `save_document` on the project's `Home register` |

Search before creating. Reuse a matching issue rather than opening a duplicate.
