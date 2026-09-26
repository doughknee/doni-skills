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
4. Create two documents in the project: `Home brief` and `Home register`, both empty, for the home skill.
5. Apply any labels the repo's `CLAUDE.md` requires to every issue created from here on.

The project is found again next time by the same search, so nothing needs to be stored. If the repo's `CLAUDE.md` says to use outcome projects instead of one per repo, follow it and never create a catch-all.

## The project brain

Linear holds what only Home and the user read. The repo's `CLAUDE.md` holds what workers must obey. Never duplicate across the two.

**`Home brief` document.** One per project: what the project is in two lines, the test surface and how to reach it, resource limits (devices, ports, hosts), what has shipped, and the current direction. Home reads it on entry instead of re-deriving the project, and rewrites the changed sections at closeout. Keep it under a screen; history goes in status updates, not here.

**Milestones are batches.** Every approved plan table becomes one milestone named for the batch, with its issues attached (`save_milestone`, then `save_issue` with the milestone). Progress and history then live in Linear's own view. A single-unit plan needs no milestone.

**Status updates are closeouts.** At the end of a batch, post a project status update (`save_status_update`) with the closeout text: outcome, what is implemented, tested, published and feature-verified, what remains. Set health from evidence: on track when everything landed, at risk when acceptance is open, off track when a worker failed twice or the user is blocked. The feed is the project changelog.

**Backlog is the inbox.** Any improvement Home proposes gets filed to Backlog as it is proposed, before the user answers, with a one-line description. "What's next" is then answered by reading Backlog by priority, never by inventing a fresh list. The user reorders in Linear.

**PRs attach to issues.** When a worker's PR opens, attach its URL to the issue (`create_attachment`) unless Linear's GitHub integration already did. Done issues carry their evidence.

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
| Home brief and register | `get_document` / `save_document` on the project's `Home brief` and `Home register` |
| Milestone per batch | `save_milestone`, then `save_issue` with the milestone |
| Closeout | `save_status_update` on the project |
| PR on issue | `create_attachment` with the PR URL |

Search before creating. Reuse a matching issue rather than opening a duplicate.
