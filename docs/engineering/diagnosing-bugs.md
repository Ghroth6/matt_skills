## What it does

`diagnosing-bugs` runs a six-phase diagnosis on a hard bug or a performance regression: build a repro, minimise it, rank hypotheses, instrument, fix with a regression test, clean up.

Its defining constraint is a **tight** feedback loop that can distinguish the reported failure from a fix. In this fork, code reading and provisional theories can help build that loop, but do not establish a root cause. Verification still needs evidence from the actual failure path, whether the loop is a command or a recorded device procedure.

## When to reach for it

Type `/diagnosing-bugs`, or the agent reaches for it when a requested diagnosis or a hard, unclear, recurring defect needs investigation. A simple explanatory question does not require the workflow.

Reach for it on the hard ones: a bug that resists a first look, an intermittent flake, a regression that crept in between two known-good states. It is heavy by design, and the wrong tool for a question you want answered in one message.

| Your situation | Where to go |
| --- | --- |
| A specific defect that resists a straightforward check | This skill |
| A simple question answerable from one useful inspection | A direct explanation; escalate if the inspection exposes uncertainty |
| A slow endpoint or a timing regression with a known before-and-after | This skill: it has a performance branch (measure a baseline, then bisect) |
| "Where are the bottlenecks in this codebase?", no specific symptom | Not this skill. It diagnoses one known failure, it does not audit |
| A raw bug report from someone else, not yet confirmed or written up | [triage](https://aihero.dev/skills-triage) first |
| Throwaway code to answer a design question, not chase a defect | [prototype](https://aihero.dev/skills-prototype) |
| Building a planned behaviour test-first | [tdd](https://aihero.dev/skills-tdd) |
| No good seam exists to lock the bug down | Record that limit; [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) can investigate it afterward |

## The tight loop is the skill

Phase 1 gets disproportionate effort because it is the only phase that is hard. The skill gives a ladder of ways to construct the loop, roughly in order of preference:

1. A failing test at whatever seam reaches the bug.
2. A curl or HTTP script against a running dev server.
3. A CLI invocation with a fixture input, diffed against a known-good snapshot.
4. A headless browser script asserting on DOM, console, or network.
5. A replayed capture: a saved request, payload, or event log, run through the code path in isolation.
6. A throwaway harness: a minimal subset of the system, one function call.
7. A property or fuzz loop, for "sometimes wrong output".
8. A bisection harness you can hand to `git bisect run`.
9. A differential loop: same input, old version against new.
10. A structured [human-in-the-loop](https://www.aihero.dev/ai-coding-dictionary/human-in-the-loop) observation when equipment or manual actions require it. Record setup, steps, expected symptom, result, and relevant logs. The supplied Bash template is useful where Bash fits; an equivalent explicit procedure works on other hosts.

**Tight** means sharp, repeatable, and as efficient as the real failure allows. Remove avoidable setup, but retain necessary boot, flashing, or equipment latency. An unrelated fast mock cannot replace a slow observation of the reported symptom. For an intermittent bug, increase and record the reproduction rate so competing hypotheses can be tested meaningfully.

When reproduction is unavailable, it states what it tried and the verification gap, then requests only the missing [environment](https://www.aihero.dev/ai-coding-dictionary/environment) access, captured evidence, or instrumentation authority. Useful authorized static inspection can continue. A candidate fix can be prepared within scope, but remains unverified until evidence reaches the original failure.

## The gates between phases

The phases separate provisional investigation from verified conclusions. The evidence needed for a completed diagnosis remains explicit.

| Gate | What has to be true |
| --- | --- |
| Reproduction loop established | A named command or structured procedure already exercised against the reported failure, with redacted observations |
| Testing causes against the loop | The scenario is reproduced and reasonably minimised without losing its essential device state or timing |
| Into Phase 4 | 3–5 ranked, falsifiable hypotheses exist, each stating its prediction, shown to you before any is tested |
| Into Phase 5 | Probes map to a specific prediction, one variable at a time, every debug log tagged `[DEBUG-a4f2]`-style so cleanup is one grep |
| Done | Original repro no longer reproduces, instrumentation gone, and the hypothesis that turned out correct is written into the commit message |

Phase 5 has an escape hatch worth knowing about. The regression test is written before the fix, but only if a **correct seam** exists for it: one where the test exercises the real bug pattern as it occurs at the call site. Where the only available seam is too shallow, the skill says so instead of writing a test that gives false confidence. That absence can become input to `improve-codebase-architecture`; it does not remove the need to recheck the original symptom.

## Common questions

**It fires on quick questions where I just wanted a direct answer.**
Users reported this in [issue #578](https://github.com/mattpocock/skills/issues/578), including GPT-5.6-Sol runs that built low-value reproductions before answering simple questions. This fork starts with the smallest useful inspection and escalates when the symptom or cause needs investigation. That is the intended behavior, not a demonstrated result for every current [model](https://www.aihero.dev/ai-coding-dictionary/model); an unnecessary full workflow is still a useful failure to report.

**Can I point it at a codebase and ask where the performance problems are?**
No. It diagnoses one failure you can already name. Its performance branch is for a regression with a symptom (establish a baseline measurement, then bisect, measure first and fix second), not for a proactive sweep. A skill for the proactive version was [proposed and closed](https://github.com/mattpocock/skills/issues/431); there is currently no skill for it.

**Does it stop and ask me before it writes the fix?**
No. Only Phase 3 has a human checkpoint: the ranked hypothesis list is shown to you before any is tested, and it proceeds on its own ranking if you are away. There is no gate between instrumentation and the fix, so the agent can start writing code before you have agreed with its root cause. [Issue #124](https://github.com/mattpocock/skills/issues/124) asks for that gate and is still open. If you want it, say so when you invoke the skill.

**I already ran `/triage` on this bug report. Is this the same work again?**
Reuse relevant reproduction evidence already obtained. Triage's bounded check may supply the failure observation and setup needed here; repeat or extend it only where this diagnosis needs more evidence. A prior check of a nearby symptom still cannot stand in for the actual reported failure.

**Will the repro output it pastes leak secrets?**
The source requires secrets to be redacted before commands, output, or captures are shown. Credentials stay in environment variables, and only relevant capture lines should be quoted. This is an instruction, not an automatic sanitizer; check evidence before sharing it outside its intended audience.

**My device takes minutes to reboot, and part of the repro is manual.**
That can still be a useful loop. Record the device setup, repeatable steps, expected failure, actual result, and timing. Keep necessary latency visible and remove only avoidable work. A host-side test can support the diagnosis without establishing that the device path is fixed.

**My security scanner flagged this skill as high risk.**
Snyk flags it, and the flag is a false positive. It is the only skill in the set that ships an executable shell script (`hitl-loop.template.sh`) alongside instructions to run it and to curl a dev server. Shipped `.sh` plus run-it instructions plus outbound HTTP is enough to trip a static scanner. The script itself is about 30 lines of `read -r -p` prompts that pause for human input. The scanner is rating the capability surface, not a proven exploit.

**What happened to `/diagnose`?**
Renamed to `/diagnosing-bugs` in v1.0.0. The old name no longer exists. Anything of yours that chains `/diagnose` (a wrapper skill, a saved prompt) needs updating.

## It's working if

- Simple questions get a useful inspection first; a hard diagnosis makes its reproduction procedure and observed failure explicit.
- The failure it reproduces is the one you reported, not a nearby one it found on the way.
- Provisional theories stay separate from verified causes, and minimization preserves the state and timing that trigger the failure.
- You are shown a ranked list of 3–5 hypotheses, each with a prediction you could falsify, before any of them is tested.
- Every debug log it adds carries a tag like `[DEBUG-a4f2]`, and a grep for that tag comes back empty when it declares done.
- The commit or PR message names which hypothesis was right.
- When it cannot lock the bug down with a test, it says so plainly instead of writing a shallow one.
- A missing device or end-to-end observation remains a verification gap, even when supporting tests pass.

## Where it fits

`diagnosing-bugs` is a reach-for-it-anytime standalone for hard or unclear failures. It needs access to the relevant observations, but no separate setup ceremony. [ask-matt](https://aihero.dev/skills-ask-matt) routes investigation here while leaving simple explanation requests light.

Two neighbours matter. [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) takes the [handoff](https://www.aihero.dev/ai-coding-dictionary/handoff) when the real finding is that the code has no seam to lock the bug down; the recommendation is made after the fix is in, when there is more information. [triage](https://aihero.dev/skills-triage) sits upstream of it for bugs that arrive as raw reports from other people, and does a shallower version of the same first two phases.
