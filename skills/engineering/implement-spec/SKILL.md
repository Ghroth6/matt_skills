---
name: implement-spec
description: "Implement the result of /to-spec and /to-tickets in code."
disable-model-invocation: true
---

You have been provided a spec. This spec should have tickets associated with it, describing how to implement the spec.

The issue tracker should have been provided to you. If not, tell the user to run `/setup-matt-pocock-skills`.

The goal is the authorized, ready scope implemented and verified on a single **integration branch**, with work resolved the way the issue tracker closes it. Invoking this skill to build the spec authorizes its ready work; planning or a router recommendation alone does not. Report any remaining scope explicitly.

The tickets form a **task graph**. Its **frontier** contains authorized tickets whose current scope, material decisions, and acceptance evidence are clear and whose dependencies are satisfied. An empty frontier can mean missing decisions or verification, not completion.

Communication to and from subagents should be sparse. Communicate primarily through **context pointers**: to the spec, tickets, research notes, and previous commits. Don't duplicate information already available via pointers.

**Implementer subagents** should be run in the background where possible for maximum concurrency.

## Steps

1. Read the current spec, tickets, and comments. Follow relevant decisions, corrections, exclusions, and prototype evidence until each candidate's deliverable and completion evidence are clear. Separate current decisions from superseded text and tentative suggestions. If a required source or decision is missing, ask only for that gap and continue independent authorized work. Record the task graph and each ticket's readiness separately from its blockers.

2. (optional) Use an **exploration subagent** to conduct any exploration required by the tickets - relevant codebase files or external documentation. Ensure the exploration subagent can save files - it should save its markdown notes in a directory outside the repo, accessible by all future subagents. This lets **implementer subagents** focus on implementation rather than exploration.

3. Record the pre-work commit and create the integration branch. If the repository workflow or user authorizes a PR, open a draft after the first merge in step 5. Link the spec and tickets; add closing keywords only for fully covered work, and for the spec only when its entire acceptance contract is met. Keep the PR's scope current as work lands.

4. Dispatch the current frontier within the host's concurrency limits, each ticket in its own worktree and branch. Sequence tickets sharing a mutable surface when their changes cannot be integrated independently. Each implementer subagent:
   - starts from the integration branch, preserving any existing work when correcting its base;
   - reads its current ticket and comments plus the relevant source pointers from step 1, recovering corrections, exclusions, acceptance examples, and agreed seams without reopening settled questions;
   - calls the Skill tool with `tdd` to build the ticket;
   - compares actual behavior and verification with the current acceptance contract. A skipped check or substitute test does not establish device, GUI, or end-to-end acceptance; report missing fixtures, access, and observations explicitly;
   - merges the integration branch tip into its own branch and reports its commits, evidence, changed assumptions, and any unfinished work.

5. Use a **merger subagent** to integrate completed work serially against the latest integration tip. Resolve conflicts by intent and rerun checks affected by integration before recording what landed and what was verified. Preserve unverified work as such. Internal dependency satisfaction requires the evidence the dependent ticket needs; it is separate from tracker closure, which follows the repository workflow. Do not close a PR-backed issue merely to unlock the frontier.

6. Recompute the **frontier** after each integration. If a result or source update invalidates a premise, reassess the affected tickets before dispatch and notify any affected active implementers. Continue unaffected work. When no work can proceed, record the missing decisions, evidence, or external dependencies instead of declaring the spec complete.

7. Once the runnable scope has landed, call the Skill tool with `code-review` against the pre-work commit. Supply the current contract, relevant sources, verification results, and explicitly deferred scope, so the review covers every implementation commit without treating deferred work as a new assignment. Use one implementer for actionable findings; integrate its fixes and run focused checks. Confirm that the final diff includes the implementation and fixes and that evidence covers the claimed acceptance criteria.

8. Report the implemented scope, unresolved items, verification limits, and integration branch. Mark a draft PR ready only when its declared scope is verified and review findings are resolved; otherwise leave it draft with the remaining gaps. Resolve only completed work and only through the configured workflow. Merge, deployment, installation, and additional scope follow the user's authorization.

9. Clean up this run's worktrees only after their commits and required untracked evidence are recoverable. Retain any worktree still needed for unfinished work and report why.
