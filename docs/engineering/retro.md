## What it does

`retro` looks back over a coding [session](https://www.aihero.dev/ai-coding-dictionary/session) and traces user corrections and avoidable rework before suggesting improvements to the agent's decisions, workflow, and **[environment](https://www.aihero.dev/ai-coding-dictionary/environment)**. It distinguishes requirements learned later from instructions or evidence already available when the agent made a choice.

It reads the session's own record and returns evidence-backed candidates ordered by impact and recurrence risk. The bug the agent shipped, the file it took twenty [tool calls](https://www.aihero.dev/ai-coding-dictionary/tool-call) to find, or the principle it applied to only one folder each needs a remedy at the point the failure arose. It only proposes; nothing changes until you pick a candidate.

## When to reach for it

You invoke this by typing `/retro`, and the agent won't reach for it on its own.

Reach for it at the end of a session that felt harder than it should have:

| Your situation | Reach for |
| --- | --- |
| You repeatedly had to point out consequences of an already agreed principle | `/retro` to trace missed decisions and their scope |
| The agent spent too long finding a file or fact | `/retro` for navigation improvements |
| A machine could have caught the mistake | `/retro` for a deterministic check |
| Required information was unavailable to the agent | `/retro` for a way to make that evidence accessible |
| You want a verdict on the code produced | [code-review](https://aihero.dev/skills-code-review) |

A smooth session has little to teach; a painful one is where the findings are.

## Where the findings land

Each candidate starts with a specific moment: what was known, what the agent did, what rework followed, and what earlier action could have prevented it. These categories help choose where a remedy belongs; they do not determine priority:

| What went wrong in the session | Fix it with |
| --- | --- |
| Known intent did not shape the initial choice or its related cases | Guidance at that decision point, or a reusable task Skill |
| The agent took a long time to find a file or fact | A **navigation pointer** from a file it already reads |
| It made a mistake a tool could have caught | An **[automated check](https://www.aihero.dev/ai-coding-dictionary/automated-check)**: lint rule, type, test, pre-commit hook, CI job |
| The reviewer missed a judgement-call mistake | A rule in `CODING_STANDARDS.md` for the reviewer agent |
| `AGENTS.md` or `CLAUDE.md` is large | Move its steering out, into standards or checks |
| A tool call was expensive for what it returned | Streamline the tool, or replace it |
| A steering file is full of lines that change nothing | Delete the **no-ops** |
| The agent needed information it couldn't reach | Widen its access: tee the dev server log to a file, give read-only access to a service |

Review-only standards belong with the **reviewer**. Scope, dependency selection, and first-use design need guidance before implementation. A task-specific procedure can live in a Skill; an essential cross-task rule may justify a short instruction in [AGENTS.md](https://www.aihero.dev/ai-coding-dictionary/agents-md), whose cost is paid in every session's [context window](https://www.aihero.dev/ai-coding-dictionary/context-window). If a rule already exists, investigate whether the agent reached and applied it before adding another.

Before any rule gets written, the violation is classified. A **mechanical** one (a banned API, an import shape, a file-location rule) gets a deterministic check, because a check can fail and a sentence in a standards file can't. Only genuine judgement calls, the kind no linter could ever enforce, become prose. A repo with no guardrail at all (no pre-commit hook, no CI job running lint, typecheck, and tests) is reported as a finding in its own right.

## Common questions

**Why did I have to keep correcting the agent when the principle was already clear?**

That is part of the retrospective. It follows the corrections and checks whether the agent applied each confirmed principle across the agreed scope. It also separates genuinely new requirements from missed earlier evidence, so it does not blame the agent for information it could not yet have known. A cause that the record cannot establish stays a hypothesis.

**Does it write the lint rule itself, or wait for a yes? Can I wire it to run after every session?**

It waits. `retro` only proposes; nothing changes until you pick a candidate, so there's no hand-editing and no auto-applied hook either. That is deliberate: one user asked for exactly this after being "burned by auto-hooks that blocked good changes." Deciding what deserves a permanent check takes judgement, so the skill stays [human-in-the-loop](https://www.aihero.dev/ai-coding-dictionary/human-in-the-loop) and user-invoked. Some users do chain it after every implementation run, but a smooth session has little to teach, and running it on every one mostly produces rules nobody needed. There is no dry-run mode: a proposed check is built like any other code, so try it against the repo before you let it block merges.

**Won't this pile up lint rules forever? Does it ever suggest removing one?**

Partly, and this is its weakest spot. The removal side it has covers prose: no-ops in steering files, and steering in `AGENTS.md` or `CLAUDE.md` that belongs in standards or a check. Those it will flag for deletion when the files are large, judged against the session it is reading, so treat each one as a candidate for the deletion test rather than a verdict. It does not audit the lint rules, hooks, or CI jobs it proposed last month. It sees one session, so it can't tell you a rule has gone noisy or outlived the bug that justified it. Pruning checks is still your job; a rule that fires constantly on good code is the cue.

**Won't it just invent generic advice to fill its categories?**

That's the sharpest critique it gets. One user found that "once the job is finished, the AI tends to forget the struggles from the middle of the session and invents generic advice to satisfy the retro categories." The defence is that every candidate has to come from the session's own record, so the advice is specific to that session. That cuts both ways: it rarely hallucinates something irrelevant, but it can over-index on whatever this one session happened to be about. Discard any candidate you can't trace to a specific moment. Treat the severity order as a first draft too: a quiet, expensive mistake can rank below a loud, cheap one.

**My session is long. Run it now, or start fresh?**

By default it reviews the current session, which is the best case: the struggles are still in the context window. If the session has drifted out of the [smart zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone) already, [clear](https://www.aihero.dev/ai-coding-dictionary/clearing) and point a fresh `/retro` at the previous session in the session logs instead.

**The agent keeps making the same mistake. Should I add a line to `CLAUDE.md`?**

First check whether an existing instruction already covers it. A mechanical mistake calls for a failing check, a review-only judgement belongs in standards, and a decision made during execution needs guidance at that point. Keep always-loaded instructions short and reserve them for essential cross-task behavior. `retro` is not a [memory system](https://www.aihero.dev/ai-coding-dictionary/memory-system): it proposes changes and tests them in later work rather than treating a new sentence as proof of improvement.

**My setup mentions `CODING_STANDARDS.md` and I don't have one. Where does it come from?**

Nothing ships the file. The first time a session turns up a judgement-call rule for the reviewer, `retro` proposes starting it, and once you accept, [code-review](https://aihero.dev/skills-code-review) reads it from then on. Any other standards doc you already keep, such as `CONTRIBUTING.md`, works the same way.

**How is it different from `improve-codebase-architecture`?**

The input. [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) needs nothing but the code and looks for structural improvements to it. `retro` needs a session history and proposes changes to the agent's decisions, workflow, or environment. They sit side by side; neither replaces the other.

## It's working if

- Every candidate points back to a specific moment in the session, not a generic best practice.
- Repeated user corrections are explained using what was known at the time, and genuinely new requirements are identified separately.
- Each candidate names an earlier behavior to change and a concrete test; existing rules are inspected before more are proposed.
- Repeat mistakes turn into failing checks, and your `AGENTS.md` gets shorter over time rather than longer.
- A missing check that already existed but sat unwired shows up as the finding, rather than a proposal to build a new one.
- The next session on the same kind of task finds its way faster.

## Where it fits

`retro` is the last step of the main chain, where the flow looks back at itself:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

Run it after a build worth learning from, in the same session or pointed at that session's log. A smooth build can skip it.

- [code-review](https://aihero.dev/skills-code-review) is the reviewer agent `retro` most often tunes: new coding standards land where its Standards axis reads them.
- [writing-for-agents](https://aihero.dev/skills-writing-for-agents) sets the writing style for every steering file and skill `retro` proposes, and `retro` loads it before it starts.

[ask-matt](https://aihero.dev/skills-ask-matt) routes across the whole set when you are unsure which skill the situation wants.
