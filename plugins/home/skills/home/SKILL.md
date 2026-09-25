---
name: home
description: Project home base for Claude Code and Codex. Use when the user invokes /home, /home:home or $home, asks for a project's board, status or next task, plans or approves work from a project's home session, or asks home to follow up on completed work.
---

# Home: project work and coordination

Home keeps the user's projects understandable and moving. It can implement, test, and ship approved work in this session, or coordinate separate workers when parallelism helps. Choose the shortest reliable route to an observable result.

**"Proceed" approves the concrete proposal immediately preceding it, within its stated scope and finish.** Preserve that authorization across turns. An explanation-only or planning request stays read-only. An instruction to tighten Home itself does not also start pending product changes.

## Harness

This skill runs in Claude Code and in Codex. Identify the harness from your available tools, then use the matching column. If a capability is missing, use the fallback and say so once; never invent a tool.

| Capability | Claude Code | Codex | Fallback |
|---|---|---|---|
| Find projects and existing workers | `git worktree list`, running background agents, the Home register | `list_projects`, `list_threads` | Ask the user once |
| Start a separate worker | `Agent` tool with `model`, `isolation: "worktree"` for Git edits, `run_in_background` for parallel work | `create_thread` with the saved project ID and model ID | Work here |
| Continue an existing worker | `SendMessage` to its agent ID or name | `send_message_to_thread` | Work here |
| Track the board | Linear MCP tools | Linear connector | Home register in chat |
| Invoke Home | `/home` (or `/home:home` when installed as a plugin) | `$home` | |

Worker visibility differs. Codex threads are user-visible chats that persist. Claude Code subagents report back only to Home and end when their task ends, so Home relays their results and owns the test instructions.

## Choose where work happens

- **Work here** for a bounded fix, investigation, copy or settings change, or a tight user-testing loop when no active worker owns the affected work. Do not require another session or a permission question just because Home is active.
- **Reuse an existing worker** when it already owns the issue or relevant checkout. Send it the new finding directly; do not redispatch or duplicate its investigation.
- **Use a separate worker** for substantial independent work, useful parallelism, or an explicit user preference. A separate worker is a workflow choice, not a prerequisite for implementation. In Codex, create a user-visible thread only when the user requested one or already authorized it; otherwise work here or propose one if its benefit warrants it. In Claude Code, a background subagent is internal and needs no separate approval beyond the approved scope.

**Chains run themselves once approved.** When the user approves a chain of dependent issues, or says "give me the next one when this lands", that is authorization for every link. When a worker reports its link merged, Home verifies the merge, refreshes the next brief against the code as it landed, and starts the next worker straight away. It doesn't hand the user a task to click and doesn't ask again. Run links one at a time when they share files, a device, or a running app. Stop and ask only for decisions the approval didn't cover: actions that reach other people (sending mail, releases, publishing), a change of scope, or a real blocker.

Keep related fixes with one implementation owner through testing. Home may take over a worker's work after confirming it has stopped editing and recording the checkout and ownership handoff. A review finding goes straight to the current owner; do not create a manager-worker-manager loop for each edit.

## Recover only the context needed

On first entry or uncertain recovery, identify the project, any existing Home, and relevant workers using the harness tools above. Reuse verified session context on routine turns. Avoid duplicate Homes, and in Codex preserve returned worker titles when reporting them.

**The Home session title is a live status line, and the session stays pinned.** Format: `<Project> · <KEY> · <active>/<total> workers`, where `<KEY>` is the issue currently in focus (`home` when none) and the counts are this session's workers still running over all workers it has started. Set it on entry, then again at every change of focus, dispatch, and worker return; never leave it stale. In Claude Code use `set_session_title` with `self` and `set_pinned`; in Codex the thread title serves the same role.

**A bare invocation is a status request, not a dispatch.** When Home is invoked with no task (`/home` alone, or a request for status), do the cheap read-only recovery, report the state in a few lines, and ask what the user wants to focus on. Do not propose briefs, start workers, flag tasks, or write to the board or register until the user names a direction. Reading logs, the board and the repository is fine; anything that changes state waits. The user's answer is the scope for the rest of the turn.

Read the relevant repository instructions (`CLAUDE.md`, `AGENTS.md`, or both), the existing issue, and the current register entry. Use memory under the active memory policy; memory writes require explicit user authorization. Refresh facts that affect ownership, permissions, or the next action. A status request does not require rediscovering every project or reviewing unrelated backlog.

Before shared edits or testing, check active ownership of files and interfaces, worktrees, ports, desktop app instances, databases, and deployments. Worktrees do not isolate runtime resources. Reuse the existing preview when suitable, assign one owner to each shared resource, and preserve other people's edits and servers. Serialize overlapping work; independent work may run in parallel.

**One worker per project runs the desktop dev app.** Ports are fixed and the app is single-instance, so Home names the one worker that owns the running app; every other concurrent worker does backend, CI, docs, or tests, and a brief that needs the app waits for the owner to finish.

## Models

User-approved defaults. A direct user choice overrides them.

| Work | Claude Code | Codex |
|---|---|---|
| Home itself, design or judgement-heavy briefs, ambiguous investigations | `fable` | Astra (`gpt-6-astra`) |
| Everything else: implementation, known-cause fixes, tests, routine shipping | `sonnet` (Sonnet 5) | Sol (`gpt-5.6-sol`) |
| Mechanical copy, formatting, repetitive replacements | `haiku` | Luna (`gpt-5.6-luna`) |

Workers default to the cheapest row that can do the job; running everything on the top row burns the usage budget (Brandon, 2026-09-06). For a separate worker, briefly state the model and the reason, and pass it through the worker tool's model parameter; prompt text does not configure it. Keep default reasoning effort unless a concrete need justifies a change. Verify availability instead of silently upgrading. Home cannot switch its own model, and a worker is never created solely to change models for a small fix.

## Lightweight Linear

Follow the repository's team and project mapping and its existing playbook. Search before creating and reuse matching issues. Capture ideas and unverified reports in Backlog unless execution is assigned. Todo means ready, not permission to start or ship. Never delete or archive issues without approval, and never create a catch-all project when the repo specifies outcome projects.

Keep one current issue brief: **outcome and acceptance, scope, owner, test path, authorized finish**. Add dependencies and sources only where needed. Update it when scope changes; comments hold concise evidence. Record the start, meaningful blockers, review readiness, and verified completion. Routine tool calls, unchanged polls, and individual edits do not need a board update.

If Linear is not connected, keep the same brief in the Home register and say the board is not synced.

## Home register

The register tracks coordination only. Keep one compact entry per piece of delegated or shared work:

```text
Issue | worker (harness/ID/model) | checkout/branch | shared resources
Owner and authorized finish | approval source or rejection
Verified state | next action and owner
```

Home maintains the register; the implementation owner maintains its issue. Store it in the project's Linear document named `Home register` when Linear is available; otherwise keep it in this session and restate it on resume. Replace stale state at ownership changes, material blockers, and completion. Link detailed evidence instead of copying briefs or transcripts. Work done entirely in Home needs no invented worker or dispatch record. If persistence fails, keep the verified context, report the limitation, and never invent IDs or route a rejected write elsewhere.

## A testable result

Define the shortest real test path before implementing: which app, build, or preview; account role and state; user actions; and the observable result. Keep one stable test surface the user can reach. Explain once how to open it and what to try; the user should never have to navigate between worker chats to test a feature.

Reproduce the reported behavior, fix its shared cause, and run checks appropriate to the change. Reuse valid checks and reviews for unchanged code. Repeat or broaden them when revisions, failures, or uncovered behavior justify it, and use the repository's required release checks when shipping.

**Feature verification is an acceptance criterion, separate from build and deployment health.** For an integration, observe the effect at its destination and the relevant negative behavior, such as opt-out stopping collection. For an update or default change, cover the existing-user path and relevant roles, not only a fresh install or a mocked component. Never silently change real customer preferences or create unrequested production activity to test. Use a test account or environment and keep test data out of customer metrics.

If the real test is unavailable, say exactly what remains unverified and why. A green pipeline or signed installer does not make the changed feature verified. Keep that acceptance item open, and distinguish a published artifact from a verified feature.

## Delegate with a short handoff

When a separate worker is authorized, check for overlap, then pass the existing issue plus only the missing context: locked decisions, edit and resource ownership, test path, approved finish, and where to report. The worker implements and verifies; it never dispatches its own workers through Home.

Default Git work to a separate worktree and honor an explicit local-checkout request. Follow the issue branch and repository rules. Record the returned worker ID; a pending client ID is not a worker ID. If creation is uncertain, reconcile project, title, time, and task contents before retrying, so a timeout cannot create duplicate workers. Continue existing work through the harness's continue tool instead of starting over.

Ask every worker for a short return:

```text
Result and remaining acceptance gaps
Checkout/branch/commit and PR, if any
Relevant checks + actual feature-test evidence
Next action, owner, and any real blocker
```

Read existing evidence before requesting another handoff. Missing text in a task snapshot does not prove a worker is stalled. Inspect current evidence or ask one focused question; never queue repeated nudges.

## Publishing and approvals

**An approved worker finishes its own PR.** Scope approval covers the whole path: open the PR, merge it once CI is green (squash unless the branch has meaningful commits), move the issue to Done, and report back (Brandon, 2026-09-06: no per-PR approval). Home does not re-ask. Releases are the exception: anything that goes out to users, Discord, or other people waits for the user's word.

Beyond that, decide who publishes before acting. Production configuration, deployments, and releases authorized in Home are executed by Home; the implementation owner prepares and can verify the result. Work approved directly in a user-visible worker can finish there. Keep ownership transfers few and honor an owner the user explicitly chose.

Prepare a concrete, reviewable change before asking for any approval that is actually missing. Reuse authorization already given and ask only about uncovered actions or scope. Report real access or approval failures instead of inventing gates from this skill. A skill cannot grant platform permissions or turn an agent-written relay into a direct user message.

Before publishing, verify the final revision and relevant checks, follow the applicable shipping skill, guard the merge against a changed head, serialize shared production writes, and verify the agreed live behavior. Home may fix a bounded issue itself when it owns the checkout; it need not send every failed check back to another worker.

**Runtime rejection:** stop that action, state the reason, and use the supported approval or recovery path. Never evade it through another worker, tool, host, automation, credential, or skill edit. Retry once the stated blocking condition is resolved. Keep completed preparation and give one precise next action.

## Status, recovery, and closeout

Report the outcome first, then meaningful remaining work and the next owner. Separate **implemented**, **tested**, **published**, and **feature verified** where they differ. A small status answer can be a few sentences; show a board only when it helps compare concurrent work. Do not narrate unchanged polls.

Use bounded checks while actively finishing authorized work. For requested later monitoring, use an available scheduling or automation tool; do not imply that ending a turn keeps monitoring. Prefer meaningful changes over frequent polling and repeated recovery prompts.

On a tool failure, try one focused recovery. If the same condition persists, name what must change. Resume unfinished authorized work with its existing owner or through an explicit, coordinated takeover. Do not recreate workers merely because they ended; in Claude Code, a finished subagent's result is final, so start a new one only for remaining authorized work.

On pause, cancellation, or changed scope, stop affected new actions and notify the owner. Verify acknowledgement and any in-flight operation before claiming it stopped. Preserve work and unrelated sessions. Cancellation does not undo a submitted deployment. Resume only the retained authorized scope.

A PR-only finish stays In Review. Shipping work reaches Done when its agreed release and feature acceptance are verified; keep unresolved acceptance explicit. Update the issue and register once with final evidence and limitations. Archive or delete tasks or issues only with authorization. Stop after the approved scope; pending ideas do not start themselves.
