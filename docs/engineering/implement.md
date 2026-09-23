## What it does

`implement` builds work that has already been decided. You point it at a [ticket](https://www.aihero.dev/ai-coding-dictionary/ticket), a [spec](https://www.aihero.dev/ai-coding-dictionary/spec), or the plan you just agreed in the conversation, and it writes the code, drives [tdd](https://aihero.dev/skills-tdd) at the seams, typechecks as it goes, runs [code-review](https://aihero.dev/skills-code-review) at the end, and commits to the current branch.

It reuses settled decisions instead of interviewing you again. In this fork, a fresh [agent](https://www.aihero.dev/ai-coding-dictionary/agent) first recovers the current goal, corrections, exclusions, and acceptance evidence from the task and relevant sources. A missing required source or material conflict is named before the affected work proceeds; independent authorized work can continue.

## When to reach for it

You invoke this by typing `/implement` yourself: the agent won't reach for it on its own. It ships with `disable-model-invocation: true`, so no other skill can call it either. Wherever [ask-matt](https://aihero.dev/skills-ask-matt) or [to-tickets](https://aihero.dev/skills-to-tickets) says "then `/implement` per ticket", that is an instruction to you, not something the agent will do unprompted.

Where the work currently lives decides whether this is the right skill:

| The work is… | Reach for |
| --- | --- |
| A ticket on the tracker | `/implement` with its full reference; prefer a fresh [session](https://www.aihero.dev/ai-coding-dictionary/session) for independent work whose decisions are recoverable |
| A spec, not yet split up, and the build spans sessions | [to-tickets](https://aihero.dev/skills-to-tickets) first, then `/implement` per ticket |
| A spec, and the build is small | `/implement` directly against the spec |
| Only in the conversation you just had, and it's still small | `/implement` right there, in the same window |
| Not written down anywhere yet | [grill-with-docs](https://aihero.dev/skills-grill-with-docs), or [grill-me](https://aihero.dev/skills-grill-me) if there's no codebase |
| One concrete behaviour you want test-first, with no spec | [tdd](https://aihero.dev/skills-tdd) directly |
| Already built, and you want it checked | [code-review](https://aihero.dev/skills-code-review) directly |

An agreed conversation is a supported input. A small change need not gain a spec file merely to enter implementation; its deliverable and completion evidence still need to be clear.

## Prerequisites

`implement` commits to the branch you are on. It does not create one, and it does not ask. Check you are on the branch you want the work on before you start.

If the tickets came from [to-tickets](https://aihero.dev/skills-to-tickets), the tracker they live on was configured by [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills). `code-review` reads the same configuration to find the originating spec at close-out.

## What one run does

A run connects the accepted work to a reviewed local commit:

1. Read the current task and relevant comments, decisions, and prototype evidence; recover its acceptance criteria and exclusions.
2. Drive [tdd](https://aihero.dev/skills-tdd) at the pre-agreed seams, one red-green slice at a time.
3. Typecheck often, run single test files as it goes.
4. Run the full test suite once, at the end.
5. Check actual behavior against acceptance, run [code-review](https://aihero.dev/skills-code-review) on a diff that includes the work, resolve actionable findings, and finish with a commit on the current branch.

Keep the run bounded to the authorized deliverable. Tickets from [to-tickets](https://aihero.dev/skills-to-tickets) carry enough context and references for a fresh reader, without making the entire project history a prerequisite. Related planning, debugging, and acceptance phases can stay together when that context remains useful.

## Pre-agreed seams

The idea the skill runs on is the **seam**: the public boundary you observe behaviour at, without reaching inside. Tests live at seams. Working at a seam agreed before any code is written is what keeps the tests durable, because the implementation underneath can be rewritten without the tests moving.

The word "pre-agreed" is doing real work, and it is also the skill's weakest joint. Nothing inside `implement` agrees the seams. `tdd` is the skill that asks, and it refuses to write a test at an unconfirmed seam. So in practice the agreement happens either upstream in the spec, or in the first exchange of the run. If it happens nowhere, the precondition never fires and the run quietly becomes "just write the code". Naming the seams in the spec is what stops that.

## Common questions

**It finished, but my ticket is still open and the acceptance criteria are still unchecked.**

Its default endpoint is a reviewed local commit, with the implemented outcome and verification limits reported. Publication, tracker transitions, and installation follow your authorization and repository workflow. If a dependency chain needs ticket closure, make that authorized transition explicit; it is separate from resolving actionable code-review findings, which is part of completing the implementation.

**Can I point it at all my tickets at once, or run several in parallel?**

It accepts the work you authorize from a spec, ticket set, or agreed conversation, but it is not a queue dispatcher. Keep each deliverable bounded and make concurrency a separate repository decision. Several sessions sharing a checkout also share its index and HEAD; isolation and integration need an explicit workflow. Finishing one item does not grant permission to drain the remaining queue.

**Can it open a pull request instead of committing?**

The default endpoint is a local commit. An explicit request or repository workflow can authorize publication and a PR afterward; the skill itself does not grant that authority. Set the intended branch and delivery scope before starting.

**`code-review` says it cannot see my changes.**

The reviewer needs an explicit diff containing the implementation. When its entrypoint only accepts committed changes, this fork makes a local checkpoint and reviews against the pre-work commit. Actionable findings must be resolved before that checkpoint is treated as completed work.

Separately, some people deliberately do not want the review inside the run at all, because an agent reviewing the code it just wrote is biased toward its own solution. Running [code-review](https://aihero.dev/skills-code-review) in a fresh session against a fixed point is a legitimate alternative, and is the same reason that skill runs its two axes in separate sub-agents.

**One ticket burned 150k tokens. Am I using it wrong?**

A token count alone does not diagnose a bad run. Consider the actual host context, discovery cost, repeated corrections, and whether one independently verifiable outcome is still in view. If the scope keeps expanding, revisit the slices in [to-tickets](https://aihero.dev/skills-to-tickets). Preserve the decisions needed for recovery before choosing whether to continue or start fresh.

**`/implement #2` in a fresh session worked on something completely unrelated.**

A bare number can be ambiguous. This fork resolves the tracker repository and title, reads the body and comments, and follows the sources that affect the work. Pass the issue URL or `owner/repo#2` when possible. A missing or conflicting required reference should be exposed before editing the affected scope.

**Tests passed. Does that mean device or GUI acceptance passed?**
Only if those observations were actually made. The close-out compares behavior with the original criteria and linked examples, and states unverified boundaries. A passing substitute test supports its own claim; it does not establish device, GUI, or end-to-end acceptance.

## It's working if

- The session opens by reading the ticket or spec and restating what it will build, rather than asking you what to build.
- Where test-first work is possible, it uses `/tdd` at the agreed seams; absent acceptance evidence is reported rather than hidden behind passing substitute tests.
- Typechecks and single test files run repeatedly during the run, and the full suite runs once near the end.
- The run reaches a commit on your current branch without you prompting it to carry on.
- The diff matches the authorized deliverable, and corrections and exclusions remain intact.
- The report names the commit and distinguishes observed acceptance from verification still missing.

## Where it fits

`implement` is the build step of the main chain, second from the end:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

Its neighbours are [to-tickets](https://aihero.dev/skills-to-tickets), which supplies scoped outcomes, readiness, and dependencies; [tdd](https://aihero.dev/skills-tdd), which it uses at agreed seams; and [code-review](https://aihero.dev/skills-code-review), which checks the actual implementation diff. It recovers the accepted plan and checks its completion evidence without turning every implementation into another design interview.

That trust is why [wayfinder](https://aihero.dev/skills-wayfinder) merges onto the chain at [to-spec](https://aihero.dev/skills-to-spec) rather than looping its map straight into `implement`. Go straight to `implement` from a map only when the effort turned out genuinely small.

[ask-matt](https://aihero.dev/skills-ask-matt) is the router over the whole set when you are not sure which flow you are in.
