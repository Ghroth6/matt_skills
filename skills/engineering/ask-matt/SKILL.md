---
name: ask-matt
description: Ask which skill or flow fits your situation. A router over the skills in this repo.
disable-model-invocation: true
---

# Ask Matt

You don't remember every skill, so ask.

A **flow** is a path through the skills. Most paths run along one **main flow**, and two **on-ramps** merge onto it. Everything else is standalone, or a vocabulary layer that runs underneath.

## The main flow: idea → ship

The route most work travels. You have an idea and want it built.

1. **`/grill-with-docs`** sharpens the idea by interview. Start here whenever you are **working in a working directory**: it's stateful, retaining what it learns in `GLOSSARY.md` and ADRs. (No working directory? Use `/grill-me` instead, covered under Standalone. Both run the same `/grilling` primitive; `grill-with-docs` is the one that leaves a paper trail, which makes it the better of the two whenever a repo is there to leave it in.)
2. **Branch: can you settle every question in conversation?** If a question needs a runnable answer (state, business logic, a UI you have to see), detour through a prototype, bridged by **`/handoff`** in both directions (a prototype lives in its own directory, which is exactly what `/handoff` is for; see Phase boundaries):
   - **`/handoff`** out, then open a fresh session against that file,
   - **`/prototype`** to answer the question with throwaway code,
   - **`/handoff`** back what you learned, and reference it from the original idea thread.
3. **Branch: is this a multi-session build?**
   - **Yes** → **`/to-spec`** (turn the thread into a spec), then **`/to-tickets`** to split evidence-supported work into tracer-bullet tickets with source references and **blocking edges**. Local trackers store one file per ticket; real trackers use native edges where supported. A ticket can start when its material decisions and acceptance evidence are clear and its dependencies are satisfied. Choose an execution route:
     - **`/implement`** for each authorized deliverable. Prefer fresh context for independent work once its required decisions are recoverable; related phases can continue together.
     - **`/implement-spec`** to orchestrate the authorized, ready **frontier** in parallel on one **integration branch**. It recovers each ticket's sources and reports any unready or unverified remainder. Choose it when the build benefits from coordinating a task graph.
   - **No** → **`/implement`** right here, in the same context window.

   Both routes drive **`/tdd`** (one red-green slice at a time) and close with **`/code-review`**, a two-axis review (Standards + Spec) of the implementation diff. `/implement` reviews its deliverable; `/implement-spec` reviews the integration branch. When review requires committed changes, make a local checkpoint first; resolve findings and commit corrections before close-out. Reach for **`/tdd`** on its own to build a concrete behaviour test-first, and **`/code-review`** to review a branch or PR against a fixed point.

   When the work goes up as a pull request, **`/pr`** shapes the body: a visual summary, before/after evidence, and merge risk. It is a model-invoked reference; publication and merging follow the project's workflow and the user's authorization.

4. **`/retro`** is the user-invoked follow-up after work worth learning from. It traces user corrections and avoidable rework before proposing decision, workflow, or environment improvements. Mechanical mistakes still call for deterministic checks; guidance for earlier decisions belongs at that decision point. Recommend it when useful; its place in the flow does not authorize invoking it or applying its suggestions.

### Context hygiene

Keep related planning phases together while their context remains useful.
Preserve material decisions and references in the resulting artifacts so a
fresh implementation session can recover them. A long-lived overview session
can coordinate scope and results while execution sessions handle bounded work.
When the user invokes `/retro`, use the relevant session or its saved log.

Use the host's actual context state and signs of lost or conflicting decisions,
not a fixed token threshold, when judging continuity. At a useful boundary,
refresh the relevant sources or recommend a fresh session. Host compaction can
occur without a visible task change (see Phase boundaries).

## On-ramps

A starting situation that generates work, then merges onto the main flow.

- **Bugs and requests piling up** → **`/triage`**. It moves issues through triage roles and produces agent-ready issues, which **`/implement`** later picks up.

  Triage is for work that arrives raw. `/to-tickets` checks readiness itself;
  a material gap remains visible instead of being promoted by the act of
  writing a ticket. Another triage round is unnecessary just to repeat that check.

- **Something's broken** → **`/diagnosing-bugs`** for hard or unclear defects.
  Start with a useful inspection; simple explanation requests do not need the
  full workflow. A **tight feedback loop** tests the actual symptom. Provisional
  hypotheses can help construct it, including slow equipment or structured
  human observations, but a substitute test cannot establish a verified fix.
  Its post-mortem can recommend **`/improve-codebase-architecture`** when no
  useful regression seam exists.

- **A huge, foggy effort: a greenfield project or a huge feature build, too big for one session** → **`/wayfinder`**, the most cognitively demanding flow here. When the way from here to the destination isn't visible yet, it charts a **shared map** of **decision tickets** on the issue tracker and resolves them one at a time, producing **decisions, not deliverables**, until the fog is pushed back and the way is clear. Where **`/grill-with-docs`** sharpens an idea you can hold in one session, wayfinder is for the idea you can't, and it's slower and denser, so save it for exactly that, never a well-scoped feature.

  When the map clears, **it hands off, it doesn't build**: merge onto the main flow at **`/to-spec`**, which collapses the map's linked decisions into a buildable plan, then `/to-tickets` and `/implement` as usual. Looping the map straight into `/implement` skips that collapse and throws the linked detail away, so go straight to `/implement` only when the effort turned out genuinely small.

## Codebase health

Not feature work, just upkeep.

- **`/improve-codebase-architecture`** runs whenever you have a spare moment to keep the codebase good for agents to operate in. It surfaces **deepening opportunities**; picking one _generates an idea_ you can take into the main flow at `/grill-with-docs`. It's the survey that finds the candidates; **`/codebase-design`** (below) is the bench you design the chosen one on.

## Vocabulary underneath

Two model-invoked references that run *beneath* the other skills, each the single source of truth for its vocabulary. Reach for them directly when the **words**, not the process, are the problem; or let the skills above pull them in.

- **`/domain-modeling`**: sharpen the project's *domain* language: challenge a fuzzy term, resolve an overloaded word ("account" doing three jobs), record a hard-to-reverse decision as an ADR. It's the active discipline `/grill-with-docs` drives to keep `GLOSSARY.md` a clean glossary.
- **`/codebase-design`** is the deep-module vocabulary (module, interface, depth, seam, adapter, leverage, locality) for designing a module's *shape*: a lot of behaviour behind a small interface at a clean seam. `/tdd` and `/improve-codebase-architecture` both speak it.

## Phase boundaries

A **phase** is a chunk of work inside a session: the grilling, the implementation, the QA. At the **boundary** between two of them you have five options, and picking between them is the fuzziest decision in this whole map:

- **Continue**: stay put while the relevant context remains coherent and useful.
- **`/clear`**: empty the window, when nothing here matters to what's next.
- **`/handoff`** writes a portable markdown file. Narrow: only for a **new harness**, a **new directory**, a **colleague**, or forking a side task **mid-phase**. What it buys is portability.
- **Subagent**: send a tightly-scoped task to its own window and get a report back.
- **`/compact`** compresses this context and seeds a fresh session with it. The **default**, at the bottom of the tree rather than the first reach.

Read [PHASE-BOUNDARIES.md](PHASE-BOUNDARIES.md) for the ordered tree. Prefer a
natural boundary for a switch and keep active investigation together when its
observations are interdependent. Wayfinder retains a one-ticket default, with
explicit user-requested continuation after saving and rechecking map state.
Routing recommends a next step; it does not create sessions or invoke
user-invoked skills on the user's behalf.

## Standalone

Off the main flow entirely.

- **`/grill-me`**: the same relentless interview as `/grill-with-docs`, but **stateless**: it saves nothing locally and builds no `GLOSSARY.md`. Reach for it when you are **not working in a working directory** (sharpening a plan, a design, a piece of writing, anything with no repo under it). If you are in a working directory, use `/grill-with-docs` instead: it runs the same interview and leaves a paper trail, so it is strictly the better one.
- **`/grilling`** is the interview primitive: rounds, an in-scope frontier,
  facts the agent finds, and material decisions the user makes. It reuses
  settled answers and ordinary implementation discretion the user has delegated;
  it still ends at shared understanding confirmed by the user. `/grill-me`
  and `/grill-with-docs` are the named wrappers; `/triage`, `/wayfinder`, and
  `/improve-codebase-architecture` also use it.
- **`/prototype`** is a small, throwaway program that answers one design question: does this state model feel right, or what should this UI look like. Throwaway is a constraint on how the code is written, not a promise to destroy it: the answer folds into the real code, and the prototype itself is kept as a **primary source** on a `prototype/<name>` branch out of main, pointed at from the implementation issue. It's the detour in step 2 of the main flow, but reach for it any time a design question is hard to settle on paper.
- **`/research`**: delegate reading legwork to a **background agent**: it investigates a question against **primary sources**, then leaves a cited Markdown file in the repo. Keep working while it reads. The file it produces is something to take *into* the main flow at `/grill-with-docs`, since research feeds the thinking rather than replacing it.
- **`/to-questionnaire`** comes in when the thing blocking you isn't in your head or the codebase but in **someone else's**, and it writes them a questionnaire to fill in. It's the inverse of `/grill-me`: instead of interviewing you about the subject, it interviews you about the **send** (who it's going to, what you need back) and aims the questions at the gap. What comes back is material for `/grill-with-docs` or `/to-spec`.
- **`/wizard`** is for the steps only a **human** can take: provisioning infrastructure, setting up credentials or CI secrets, clicking through an unfamiliar third-party dashboard, running a one-off migration or cutover. It generates an interactive bash script that opens each URL, captures each value, and writes it into `.env` and GitHub secrets, so the procedure stops being something you re-explain to an agent every time. Model-invoked, so the agent reaches for it the moment it hits a wall only you can pass. If the agent could just do it itself, it should; this is for where a human is genuinely in the loop.
- **`/wait-what`** is the corrective for a message that didn't land. Use it mid-conversation, inside any other skill, and the agent re-pitches what it just said with the context you were missing, in plain English, using the `GLOSSARY.md` vocabulary. It works after the fact; `/grill-with-docs` is the upfront cure, because a shared language agreed early is what stops the jargon arriving at all.
- **`/teach`**: learn a concept over multiple sessions, using the current directory as a stateful workspace.
- **`/writing-for-agents`** is the reference for writing documents agents consume: skills, AGENTS.md, pointed-at docs.

## Precondition

**`/setup-matt-pocock-skills`**: run before your first engineering flow to configure the issue tracker, triage labels, and doc layout the other skills assume. Custom issue trackers also work.
