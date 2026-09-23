## What it does

`to-spec` turns the conversation you have just had into a **[spec](https://www.aihero.dev/ai-coding-dictionary/spec)**, and publishes it to your issue tracker as a single issue.

It does not interview you. It synthesises what is known from the thread, codebase, domain docs, and relevant decision or prototype sources. Confirmed choices stay distinct from assumptions and unresolved questions; writing a spec does not itself make the work ready to implement.

## When to reach for it

You invoke this by typing `/to-spec`; the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) won't reach for it on its own.

Reach for it when the build is too big for one agent [session](https://www.aihero.dev/ai-coding-dictionary/session) and has to survive being split across several. That is the whole trigger:

| Where you are | What to run |
| --- | --- |
| You haven't decided anything yet | [grill-with-docs](https://aihero.dev/skills-grill-with-docs) first |
| Decided, and the work fits one [context window](https://www.aihero.dev/ai-coding-dictionary/context-window) | [implement](https://aihero.dev/skills-implement): skip the spec |
| Decided, and the work spans several sessions | `/to-spec`, then [to-tickets](https://aihero.dev/skills-to-tickets) |
| A [wayfinder](https://aihero.dev/skills-wayfinder) map has cleared | `/to-spec #<map_issue>` |

## Prerequisites

`to-spec` publishes the spec as an issue, so [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) must have configured a tracker and the triage-label vocabulary for this repo first. Either kind works: a real tracker like GitHub, or local markdown files under `.scratch/`, which is supported out of the box.

## The spec is a decision record

The spec exists because context windows end. Everything you settled while [grilling](https://www.aihero.dev/ai-coding-dictionary/grilling) (the shape of the solution, the choices you argued through, what you deliberately refused) is in one conversation that is about to be cleared. The spec is what survives that.

It checks that material corrections, exclusions, rationale, and acceptance examples survive in the spec or its specific source references. It does not invent product decisions to complete the template. A fresh session should be able to recover the intended work without reading the entire project history.

## Seams before prose

Before drafting, `to-spec` identifies the **seams** the feature will be tested at. It reuses seams you already agreed and asks about a new one when it changes what acceptance proves. Ordinary test placement within an agreed seam does not reopen that decision. Existing, high-level seams are preferred to a collection of new low-level ones.

Those agreed seams then travel. [tdd](https://aihero.dev/skills-tdd) works only at pre-agreed seams, and [code-review](https://aihero.dev/skills-code-review) reviews the diff against the spec, so a seam nobody agreed to shows up as a review finding. The binding is indirect: it runs through this document, which is exactly why the seam conversation is worth taking seriously here rather than deferring it to implementation.

## Common questions

**Where did `/to-prd` go?**
It is this skill, renamed in v1.1. "Spec" is now the single through-line term, and the old `to-prd` slug is dead; reinstall under the new name. The pair that replaced the old vocabulary is *spec* and *tickets*: the spec is the destination and the decisions that fix it, the [tickets](https://www.aihero.dev/ai-coding-dictionary/ticket) are the execution steps that get there. If you pivot, delete the unfinished tickets and keep the spec.

**Does every generated spec get the `ready-for-agent` label?**
- **Scope, acceptance, and material decisions are clear:** the configured ready status can apply.
- **A material gap remains:** use the configured non-ready status and record the gap.

Readiness and dependency completion are separate, and neither is an instruction to start implementation. If an [AFK](https://www.aihero.dev/ai-coding-dictionary/afk) dispatcher polls readiness labels, configure which artifacts it may execute so it does not mistake a parent spec for one ticket-sized deliverable.

**Why not go straight from grilling to `/to-tickets` and skip the spec?**
Often you should; the spec earns its step only on multi-session work. Where it pays is that the tickets are disposable and the spec isn't: each ticket is sized for one fresh context window and gets deleted or closed, while the spec stays as the one place the reasoning behind them lives. On a single-session change that buys you nothing, and you have paid an extra synthesis step where the [model](https://www.aihero.dev/ai-coding-dictionary/model) can drift. Go grilling → `/implement`.

**I just finished a wayfinder map. What do I feed it?**
The main map issue: `/to-spec #<map_issue>`, not the individual decision tickets. [wayfinder](https://aihero.dev/skills-wayfinder) produces decisions rather than deliverables, scattered across a map; `to-spec` is the step that collapses them into one buildable document. Looping the map straight into `/implement` throws that collapse away.

**Is the spec for me to review, or is it just for the agent?**
It must support both implementation and your review. Check the accepted behavior, concrete examples, seams, exclusions, and remaining questions. This fork has no target length for user stories: it covers materially distinct behavior within the agreed scope. A surprising assertion may be a synthesis error, so check its source instead of treating its presence in the spec as agreement.

**Do I keep the spec frozen once tickets start, or let the agent rewrite it?**
It records what the evidence supports now. When a completed slice invalidates a premise, revisit the affected plan before treating later work as a commitment. Unrelated future work can remain a named question. There is no automatic synchronization service; enduring domain terms and architectural decisions still belong in `CONTEXT.md` and ADRs.

**My work is a refactor or a module boundary, not a feature. Does the template fit?**
Less well, and this is a known limitation. The template leans hard on user stories, which is the wrong shape for architectural work: you end up writing stories nobody asked for around decisions that are really about interfaces and invariants. Lean on the implementation-decisions and testing-decisions sections instead, and let the durable architectural calls land as ADRs via [grill-with-docs](https://aihero.dev/skills-grill-with-docs) rather than trying to make the spec carry them.

**Will it check the tracker for related work, or cite the ADRs it's respecting?**
It reads supplied issue bodies and comments, then follows the decisions and prototype references needed for this scope. Important meaning must remain in the spec or a specific source pointer. That is a bounded evidence check, not a promise to search the whole tracker for duplicate work. Search overlapping issues separately when the area is busy.

**`/to-tickets` couldn't read my spec: it kept truncating.**
Keep related synthesis phases together when their context is coherent, but preserve specific source pointers for a fresh reader. A host may [compact](https://www.aihero.dev/ai-coding-dictionary/compaction) even within one visible session. Truncated or inaccessible required evidence remains a gap to recover, not a reason to assume the missing decisions.

## It's working if

- It starts writing rather than asking you a fresh round of questions.
- It reuses agreed seams and asks only when a new seam changes what acceptance proves.
- It comes back in your project's nouns, not generic product-management boilerplate.
- Confirmed decisions, corrections, and examples retain their meaning; assumptions and unanswered questions are visibly separate.
- A spec with a material unresolved decision stays non-ready instead of gaining readiness merely by being written.
- The out-of-scope section has real things in it: the things you refused are usually the most useful lines on the page.

## Where it fits

`to-spec` is a step in the main build chain, and only on the multi-session branch of it:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

Its neighbours upstream are [grill-with-docs](https://aihero.dev/skills-grill-with-docs), which does the deciding this skill only records, and [wayfinder](https://aihero.dev/skills-wayfinder), whose finished map merges onto the chain right here. Downstream, [to-tickets](https://aihero.dev/skills-to-tickets) cuts the spec into tracer-bullet tickets for [implement](https://aihero.dev/skills-implement) to build. When you're unsure which skill or flow fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
