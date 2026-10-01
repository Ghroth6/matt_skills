# Upstream sync validation

Date: 2026-10-01 (Asia/Shanghai). Review-branch integration for
[maintenance issue #39](https://github.com/Ghroth6/skills/issues/39).
Merge and installation remain owner decisions.

## Verified source state

- Fork main: `f592378087a981d12fe108782a936782a72244ce`.
- Upstream target: `d81f3a183412e71a5b1e84ca21bc1a35eea03a60`.
- Common upstream base: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7`;
  21 upstream commits. GitHub confirms fork PR #4 and PR #5 are merged.
- The local checkout initially remained on September 22's `6a3b1ed`, so its
  P002/P003 Proposed text was stale. Current main records accepted P001-P006.
- Seven actual merge conflicts matched the initial assessment: the retired
  `add-pr-skill` changeset, experimental index, router, diagnosis skill, and
  `implement`, `to-spec`, and `to-tickets` docs. Resolutions preserve fork
  behavior and upstream structure. The cleanly merged router docs also carried
  an obsolete experimental PR description, now corrected.
- The target's release PR is titled v1.3, while package/plugin metadata remains
  `1.2.3`. This integration retains that metadata rather than inventing a release.

## Installed-copy snapshot

Read-only comparison of 12 relevant installed `SKILL.md` files on this computer
found all 12 matching fork main `f592378` after line-ending normalization:
`ask-matt`, `diagnosing-bugs`, `wayfinder`, `to-spec`, `to-tickets`, `implement`,
`implement-spec`, `pr`, `retro`, `resolving-merge-conflicts`, `grilling`, and
`handoff`. This verifies those bodies only, not every supporting asset or Host.
In particular, the new parallel contract and GLOSSARY changes are not installed,
and the retired merge-conflict skill still exists locally. Unchanged bodies,
such as `retro`, also match the new source and do not establish an installation
refresh. The installed files were not edited.

## Changes and preserved contracts

Promote `implement-spec`, `pr`, and `retro`; remove the dedicated merge-conflict
skill while retaining its archived page; adopt GLOSSARY naming. Extend the
parallel execution path with current-source recovery, independent readiness and
dependency checks, acceptance evidence, serial integration, premise reassessment,
review scope, truthful tracker closure, and recoverable cleanup. Update the
router, human docs, indexes, and personalization registry to match.

P001-P006 remain implemented. Existing Wayfinder capture, planning, individual
implementation, grilling, handoff, and phase-boundary contracts are retained.
The diagnosis skill changes only its glossary filename. No installed package,
other project's glossary, or production environment was modified.

## Bounded instruction replays

Two independent agents received the same seven
[fixtures](upstream-sync-replay-cases-20261001.md) and separate instruction
snapshots. A received upstream `d81f3a1`; B received this candidate. Each received
`implement-spec`, `ask-matt`, and its phase-boundary reference, without parent
history, expected answers, or access to the other snapshot. Each produced a
simulated next response and action plan; no nested agents, implementation,
tracker writes, or device actions were run.

| Case | A: upstream response | B: candidate response | Observation |
| --- | --- | --- | --- |
| R1: no blockers, missing output contract | Starts A, asks for B's output decision | Starts A, keeps B unready separately from blockers | Both preserve the material gap |
| R2: corrected comment and prototype | Keeps logs, excludes tentative cloud cleanup | Same; explicitly distinguishes host tests from acceptance-path evidence | Both recover the supplied correction |
| R3: invalidated clock premise | Holds B, informs active C, continues D | Same, with recorded readiness reassessment | Both avoid propagating a known false premise |
| R4: skipped physical test | Allows parser-only B, blocks device-dependent C, keeps PR draft | Same, removes premature closing keywords and keeps missing cold boots explicit | Neither claims device acceptance |
| R5: open issue after verified integration | Starts B; A stays open for PR merge | Same, separates internal dependencies from tracker closure | Both avoid a false tracker transition |
| R6: review fix, deferred scope, untracked evidence | Fixes A, excludes deferred B, preserves evidence before cleanup | Same, explicitly retains the pre-work-to-final diff | Both preserve scope and recoverability |
| R7: advice-only routing and follow-up | Recommends implement-spec without executing or clearing; recommends retro | Same; explicitly describes retro as user-invoked | Neither turns advice into execution |

No candidate regression was observed in these responses, and no comparative
behavioral superiority was demonstrated. These fixtures supply the relevant
facts directly and request bounded next actions. They do not test live source
retrieval, concurrent edits, actual worktrees, transport failures, device
behavior, or repeated-run/cross-model reliability. The candidate makes these
contracts explicit in source; this evaluation alone cannot prove that doing so
improves real-world reliability.

## Structural checks and review

- 37 Skill packages, exactly 27 promoted plugin entries, and 33 selected by the
  maintainer helper's directory filter. The latter is source selection, not an
  installer run. Promoted and bucket indexes and required docs match membership.
- All 37 frontmatters and UI metadata parsed as YAML; paired invocation policy
  passed for all 22 user-invoked packages. Core `quick_validate.py` checks passed
  on disposable copies after separately checking and removing the documented
  Claude-specific `disable-model-invocation` and existing `argument-hint` fields
  from those copies. The generic validator's whitelist does not accept them;
  no source metadata was removed to satisfy it.
- Local Markdown targets resolve, except the unchanged setup-ts-deep-modules
  example `./src/packages/README.md`, which points into the consuming project.
  Retired links remain only in the archived page; old glossary names remain
  only in migration/history records and the explicitly pinned historical link.
- Nine preserved contract files match fork main byte-for-byte after normalizing
  line endings, including installation instructions and Wayfinder P001 capture.
  `diagnosing-bugs` has exactly one line changed, for the glossary filename.
- Bash syntax passed for both repository helper scripts. Plugin version check
  passed at `1.2.3`. Conflict-marker, active-old-name, and whitespace checks
  passed. No installer or link helper mutation was run.
- `claude plugin validate . --strict` could not run because Claude CLI is not
  installed/discoverable in this environment. The membership and version checks
  above do not stand in for the official validator.

Two independent reviewers examined `f592378...2c1cfc5`, one for Standards and
one for Spec, without editing the candidate. Standards found one low-priority
docs convention issue: retro's trigger choices belonged in a table. Spec found
one substantive documentation defect inherited from upstream's mechanical
rename: domain-modeling's FAQ compared GLOSSARY with itself and still described
the rename as unsettled. Both were corrected; the FAQ now explains deliberate
project migration and the absence of old-name aliases. Neither reviewer found
another substantive skill-contract issue. Focused readback verified the fixes;
these reviews do not supply the unavailable official plugin validation.
