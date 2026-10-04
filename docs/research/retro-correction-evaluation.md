# Correction-led retrospective candidate evaluation

Date: 2026-10-04. Maintenance task:
[Ghroth6/skills#41](https://github.com/Ghroth6/skills/issues/41).

## Change and activation

P007 changes the order and scope of retrospective reasoning: trace material
user interventions before choosing remedies. Existing instructions and what
was known at the time constrain each causal claim. Mechanical checks remain
appropriate for mechanical failures; decision guidance can act before review.

The Skill, human docs, and `ask-matt` route are synchronized. The existing
Claude and Codex user-invoked controls are unchanged. This is a source
candidate, not an installed change; merge and installation remain separate.

## Method

Baseline: `bc73fd998ef65e069800a35f5df82414b9b2c2a6`'s `retro/SKILL.md`.
Candidate: the changed Skill in this branch. Each received one independent,
fresh-context, read-only subagent run with the same inherited model settings
and [synthetic session](retro-correction-case.md). Each could read the requested
Skill and its `writing-for-agents` reference, but not the other's output,
evaluation report, other repository sources, or previous chats. Network,
delegation, and file changes were excluded. No expected answer was supplied.

The synthetic record was constructed from the failure classes under discussion;
it is not an independent reconstruction of the original long conversation.
Its final user request explicitly asks about corrections, which may help both
versions focus on the right issue.

## Observations

| Criterion | Baseline | Candidate |
| --- | --- | --- |
| Recognize incomplete application of ownership to both projects | Yes | Yes |
| Identify archive creation as contrary to already known intent | Yes | Yes |
| Identify first-use setup gap rather than merely broken links | Yes | Yes |
| Treat later PowerShell choice as a new requirement | Yes | Yes |
| Respect supplied evidence that PR CI already exists | Yes | Yes |
| Remain proposal-only | Yes | Yes |

The baseline returned three recommendations: per-project completion checks,
first-use verification, and preserving the newly chosen platform in existing
entrypoints. It correctly rejected generic missing-CI and global-rule findings.

The candidate first accounted for the interventions in a table, then proposed
three remedies with a decision point, owner, and behavioral check. It explicitly
qualified whether the agent had actually read command help and kept the later
platform requirement separate. This is an observed difference in explanation
structure and evidentiary precision, not proof of better outcomes.

## Structural review

- Skill invocation metadata is unchanged, including Codex
  `policy.allow_implicit_invocation: false`.
- The router and human docs describe decision and workflow review as well as
  environment improvement; no automatic invocation or application was added.
- `node scripts/sync-plugin-version.mjs --check` passes at version 1.2.3.
- Changed prose and local references are checked before the delivery commit;
  no plugin manifest changed.

For the required reader-question check, the local audience wiki was absent;
the changelog had no matching retrospective entry. A live upstream issue-title
search returned adjacent session-source and routing questions. The added FAQ
comes from the owner's actual question about repeated corrections, rather
than an invented question or a claim of upstream acceptance.

## Limits and disposition

Both versions passed this small, explicitly framed example. It does not show
that the old Skill necessarily fails, that the candidate improves success
rates, or that its added instructions earn their cost across ordinary sessions.
No multi-round compaction, long raw-session reconstruction, cross-host
invocation, or installed-copy behavior was tested. Keep P007 as Candidate for
owner review; a real future retrospective with a generic invocation is the
next useful test, not more variants of this short fixture.
