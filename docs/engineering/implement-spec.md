## What it does

`implement-spec` takes a [spec](https://www.aihero.dev/ai-coding-dictionary/spec) and its [tickets](https://www.aihero.dev/ai-coding-dictionary/ticket) and coordinates their implementation on one **integration branch**. The orchestrating [agent](https://www.aihero.dev/ai-coding-dictionary/agent) gives each ready ticket to an implementer [subagent](https://www.aihero.dev/ai-coding-dictionary/subagent) in a separate worktree, integrates the results, and reviews the combined change.

It reads the tickets as a **task graph**, not a list. The **frontier** contains authorized work with clear scope, decisions, and acceptance evidence whose dependencies are satisfied. A ticket without blockers can still be unready. Missing decisions or verification stay visible while independent work continues.

## When to reach for it

You invoke this by typing `/implement-spec`, and the agent won't reach for it on its own.

| Your situation | Reach for |
| --- | --- |
| A spec split into tickets that you want coordinated in parallel | `/implement-spec` |
| A bounded deliverable you want to drive directly | [implement](https://aihero.dev/skills-implement) |
| A spec that is not split into tickets yet | [to-tickets](https://aihero.dev/skills-to-tickets) first |
| Missing product decisions that determine what should be built | Resolve the affected decisions before dispatching that work |

Related phases can continue in a useful [context window](https://www.aihero.dev/ai-coding-dictionary/context-window). A fresh execution session is useful for independent work once its decisions are recoverable; clearing is not a prerequisite.

## Prerequisites

- **An issue tracker**, configured by [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) or equivalent project instructions. Without one, the skill asks you to configure it.
- **Tickets with current sources and dependency relationships.** The spec, comments, corrections, and relevant prototype evidence must establish the work and how to verify it. Writing a ticket does not make it ready.
- **A [harness](https://www.aihero.dev/ai-coding-dictionary/harness) that supports isolated subagents and worktrees.** Parallelism stays within the host's available capacity.

## The integration branch

Every implementer starts from the integration branch, recovers its ticket's current contract, and builds with [tdd](https://aihero.dev/skills-tdd). It brings in the integration tip before reporting its commits and evidence. Merges are then serialized against the latest tip and checked for integration regressions. Worktrees isolate edits; they do not guarantee conflict-free or fast-forward merges.

Implementers receive [context pointers](https://www.aihero.dev/ai-coding-dictionary/context-pointer) to the spec, comments, decisions, and shared exploration notes. These pointers preserve the reasons behind the ticket without copying the entire project history into every prompt. When a result invalidates a premise, affected work is reassessed before dispatch and active implementers are notified.

| Delivery workflow | Result |
| --- | --- |
| Repository workflow or user authorizes a PR | A draft opens after the first integration; only fully covered work gets closing keywords |
| Tracker closes through PR merge | Issues remain open until that workflow completes; verified work on the integration branch can satisfy internal dependencies |
| Local tracker or branch-only delivery | Completed work is resolved through the configured workflow; the integration branch is reported |
| Required decisions or verification remain missing | Independent work proceeds, but the missing scope is reported and any PR awaiting that evidence stays draft |

## Common questions

**How is this different from running `/implement` on each ticket myself?**

With `implement`, you choose each deliverable. `implement-spec` coordinates the frontier and gives you one integration branch to review. Invoking it to build a spec authorizes that spec's ready work; a planning conversation or router recommendation does not start execution.

**Does it need GitHub? I want it to stop at the branch.**

No. The endpoint follows the configured workflow and your authorization. A local markdown tracker can resolve completed work offline. A PR-backed tracker can keep issues open until merge without stalling tickets whose required dependency evidence is already available on the integration branch.

**Its review kept treating unbuilt tickets as failures.**

The final [code-review](https://aihero.dev/skills-code-review) receives the pre-work commit, current contract, verification evidence, and explicitly deferred scope. It reviews the implemented scope without turning missing decisions into new assignments. One implementer handles actionable findings, followed by focused checks and verification of the final diff, rather than restarting a broad review after every fix.

**Does it drive tdd like implement does?**

Yes. Each implementer calls `tdd`. Name agreed seams in the spec or relevant sources so they survive dispatch. A substitute test still cannot prove device, GUI, or end-to-end acceptance that was not observed.

**Two implementers collided on a file or chose different names.**

Worktrees postpone collisions until integration. Shared mutable surfaces may need sequential work or an agreed contract before parallel dispatch. The merger checks the latest integration tip and reruns affected checks instead of assuming each implementer's earlier merge guaranteed compatibility.

**A key test was skipped inside its worktree, and it reported green.**

Gitignored fixtures, local databases, credentials, and device access may be absent in a worktree. The report must name the missing evidence. Arrange the required resources or an authorized run in the appropriate environment; keep acceptance unverified until the real observation exists. A worktree holding unfinished work or unrecovered evidence is retained.

## It's working if

- Independent, ready work runs in parallel within available capacity.
- Tickets with missing decisions wait while unaffected work progresses.
- A predecessor can unlock a dependent once the evidence it needs is verified on the integration branch, even while a PR remains open.
- Implementers recover corrections and acceptance examples from their sources.
- The final report separates implemented work, verified acceptance, and remaining gaps.
- A PR becomes ready only when its declared scope is verified and review findings are resolved.

## Where it fits

`implement-spec` is the parallel build alternative to [implement](https://aihero.dev/skills-implement). It consumes the graph from [to-tickets](https://aihero.dev/skills-to-tickets) and runs `code-review` over the integration branch. Afterward, you can invoke [retro](https://aihero.dev/skills-retro) for environment improvements; it is not run automatically. [ask-matt](https://aihero.dev/skills-ask-matt) routes you when you are unsure which flow fits.
