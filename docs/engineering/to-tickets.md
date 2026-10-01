## What it does

`to-tickets` takes a plan, a [spec](https://www.aihero.dev/ai-coding-dictionary/spec), or the conversation you are in, and breaks it into a set of **[tickets](https://www.aihero.dev/ai-coding-dictionary/ticket)** on your issue tracker. Each ticket declares its **blocking edges**: the other tickets that have to finish before it can start.

Each implementation slice is a **tracer bullet**: a narrow but complete path through every layer of the change (schema, API, UI, tests) with an independently verifiable outcome. It has a bounded discovery cost and relevant source pointers, so a fresh [session](https://www.aihero.dev/ai-coding-dictionary/session) can recover its meaning without reading the whole project history. Future work whose premises remain untested stays tentative instead of becoming a detailed implementation promise.

## When to reach for it

You invoke this by typing `/to-tickets`. The [agent](https://www.aihero.dev/ai-coding-dictionary/agent) won't reach for it on its own.

| Where you are | What to run |
| --- | --- |
| You have a spec issue and the build spans several sessions | `/to-tickets`, or `/to-tickets #<spec_issue>` |
| The plan is only in the conversation, never written up | `/to-tickets` reads the thread directly, no spec needed |
| The whole change fits in one context window | [implement](https://aihero.dev/skills-implement), skip the tickets |
| Nothing is decided yet | [grill-with-docs](https://aihero.dev/skills-grill-with-docs), then [to-spec](https://aihero.dev/skills-to-spec) |
| A [wayfinder](https://aihero.dev/skills-wayfinder) map has cleared | [to-spec](https://aihero.dev/skills-to-spec) first, to collapse the map, then `/to-tickets` |

This fork checks readiness while creating tickets: scope, acceptance evidence, and material decisions must be clear. A generated ticket with a gap stays non-ready. Another [triage](https://aihero.dev/skills-triage) round is unnecessary just to repeat that check.

## Prerequisites

`to-tickets` publishes into a tracker, so [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) must have configured one for this repo, along with the triage-label vocabulary. Either kind works: a real tracker like GitHub or Linear, or local markdown files under `.scratch/`, which is supported out of the box.

## Tracer bullets, not layers

A **horizontal** slice ships one layer of the change. Nothing works until every layer has landed, and each ticket's acceptance criteria have to reach into work that another ticket owns. A **vertical** slice (the tracer bullet) ships one thin path through all the layers at once, so it is verifiable alone and owns everything it grades.

This is the rule people break most often, and the consequences are well documented. One team ran a 26-ticket stack sliced by layer (corpus, producer, aggregator, selector) and got roughly twenty agent runs per closed ticket, about three quarters of them rework. Their own post-mortem traced every failure class back to the horizontal slicing rather than to the implementations.

Before publishing, `to-tickets` looks for prefactoring (the principle "make the change easy, then make the easy change") and orders that work first. Its numbered proposal shows each outcome, blockers, and readiness, then checks granularity with you. Relevant decisions, corrections, exclusions, and prototype examples travel into the affected ticket or its specific references. Publication follows your approved breakdown and tracker authorization.

## Blocking edges

The edges are the point of the artifact. They read two ways depending on the tracker:

| Tracker | Where the edges live | How you work them |
| --- | --- | --- |
| Local markdown | Text in one file per ticket under `.scratch/<feature>/issues/<NN>-<slug>.md`, numbered blockers-first | Top to bottom, by hand |
| A real tracker (GitHub, Linear) | Native blocking links, or sub-issues where the tracker has them | A ready ticket whose blockers are done is on the **frontier** and can be grabbed |

The edges live in the ticket either way. The medium only decides whether anything can act on them in parallel. `to-tickets` produces the artifact; running it (one session at a time, or a fleet) is your job, not the skill's.

No blockers does not imply readiness. A precise decision question can exist before its answer is known, while downstream implementation still waits for that answer. When a result invalidates a premise, revisit the affected slices before dispatching them.

## The wide-refactor exception

One shape breaks the tracer-bullet rule. A **wide refactor** is a single mechanical change (rename a column, retype a shared symbol) whose **blast radius** fans across the whole codebase, so one edit breaks thousands of call sites and no vertical slice can land green.

`to-tickets` sequences that as **expand–contract** instead:

- **Expand**: add the new form beside the old, so nothing breaks.
- **Migrate**: move call sites over in batches sized by blast radius (per package, per directory), one ticket per batch, each blocked by the expand. CI stays green because the old form still exists.
- **Contract**: delete the old form once no caller remains, in a ticket blocked by every migrate batch.

Where even the batches can't stay green alone, they share an integration branch and all block a final integrate-and-verify ticket. Green is promised only there.

## Common questions

**It produced twelve tickets for a three-line change.**
Over-decomposition is the most reported friction on this skill, and it is consistent across practitioners: the [model](https://www.aihero.dev/ai-coding-dictionary/model) defaults to atomic units and loses the grouping that would make them meaningful. The quiz step exists for exactly this: ask it to merge, and it will. The deeper answer is that the tickets have a floor: if the whole change fits in one context window, you don't need this skill at all. Go straight to [implement](https://aihero.dev/skills-implement).

**The tickets came out one per layer: all the schema in one, all the API in another.**
This is the failure the vertical-slice rule is written against, and the skill still produces it sometimes. Catch it at the quiz step by asking one question per ticket: what can I demo when this is done? A ticket with no answer is a horizontal slice. Some people add a "demo path" line to each ticket for this reason, and report it nudges the model toward vertical decomposition.

**On GitHub the tickets weren't created as sub-issues of the spec issue.**
Known and unfixed. It has been reported across a dozen runs and several models, [most fully in issue #554](https://github.com/mattpocock/skills/issues/554), and it is worse on Codex than on Claude. `gh` has supported this natively since v2.94: `gh issue create --parent <n>`, and `gh issue edit <parent> --add-sub-issue <n>` after the fact. Until the tracker template prefers those, wiring the parent links yourself after a run is the reliable move.

**"Blocked by" was written into the issue body instead of a real blocking link.**
Same class of problem, [reported in issue #513](https://github.com/mattpocock/skills/issues/513), where the agent went as far as asserting GitHub has no native blocking relationship at all. It does: `gh issue create --blocked-by 12,15`. Because blockers are published first, their numbers are always available at creation time. The body text is meant to be the fallback for trackers with no native edge, not the default.

**Where do the local tickets go? The v1.1 notes said a root-level `tickets.md`.**
They did, and that was a bug: a single shared file also raced when parallel agents wrote to it. Local mode now writes one file per ticket under `.scratch/<feature-slug>/issues/<NN>-<slug>.md`, in dependency order, matching the layout the local tracker template already described. The `NN` prefix is a real ticket ID, so `/implement 03` works instead of retyping a long title.

**It kept truncating when it tried to read my spec.**
A very large spec can make recovery difficult. Keep related synthesis phases together when useful, and retain specific references for a fresh reader. A visible session can already contain a host [compaction](https://www.aihero.dev/ai-coding-dictionary/compaction); do not assume it holds every original decision. Recover missing required evidence before treating the affected slice as ready.

**The acceptance criteria graded nothing: some passed before any work was done.**
Each criterion now needs an observable result and evidence that could refute it. A check for new behavior should expose its present absence. A regression criterion can already pass at the starting commit because its purpose is to preserve existing behavior. A criterion satisfied only by another ticket is a sign that the slice or its dependencies need revisiting.

**The tickets are published. How do I actually run them?**
The skill stops at the artifact; it does not dispatch a queue. Choose ready work with no open blockers and authorize its implementation. Independent deliverables usually benefit from fresh context once their decisions are recoverable, while related phases can continue together. Tracker transitions follow your authorization and repository workflow; a local commit does not by itself close a ticket.

## It's working if

- Every ticket has an answer to "what can I demo when this is done?", and the answer is behaviour, not a layer.
- The list comes back numbered, with blockers and readiness on each item, before publication.
- You can distinguish ready work from a ticket that merely has no blockers.
- Source paths and revisions locate relevant evidence; they are not a stale file-by-file implementation recipe.
- Each ready implementation ticket exposes an outcome a fresh session can finish; non-ready work names the missing decision or evidence.
- Prefactoring, where it found any, is at the front of the order rather than mixed into feature tickets.

## Where it fits

`to-tickets` is a step in the main build chain:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

Upstream is [to-spec](https://aihero.dev/skills-to-spec), which supplies the decisions and known gaps to slice against; related synthesis phases can stay together. Downstream is [implement](https://aihero.dev/skills-implement), which builds the authorized deliverable, driving [tdd](https://aihero.dev/skills-tdd) at agreed seams and closing with [code-review](https://aihero.dev/skills-code-review). For parallel execution, [implement-spec](https://aihero.dev/skills-implement-spec) reads the same graph and coordinates the authorized, ready frontier on one integration branch. When you're unsure which skill or flow fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
