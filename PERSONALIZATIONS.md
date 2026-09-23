# Personalizations

This fork keeps selected workflow customizations of `mattpocock/skills`.
The owner maintains original Skills and independent research separately;
changes to Matt-derived Skills belong here.

## Maintenance policy

- Keep downstream differences small and preserve upstream package structure.
- Before changing a Skill, read its relevant entries below. `Proposed` records
  a design target, not an implemented behavior or an instruction to implement it.
- When reconciling upstream, compare the affected Skill and its supporting
  instructions against each entry's underlying problem. Preserve implemented
  differences while the problem remains; mark an entry `Superseded` with the
  replacement evidence when upstream or another solution covers it.
- Record the implementing commit or pull request and behavioral validation
  before changing an entry to `Implemented`. Follow the existing repository
  rules for any accompanying docs, routing, or packaging changes.
- Treat this fork's reviewed `main` as the installation source. Review upstream
  updates on a separate branch before integrating them into that version.
- Track maintenance work in [Ghroth6/skills Issues](https://github.com/Ghroth6/skills/issues).
  Start a `codex/*` branch from current `main`, commit and push the change, and
  open a PR here with `Closes Ghroth6/skills#<issue-number>`. The owner decides
  when to merge; installations update separately on each computer.
- For an upstream review, fetch and inspect the new commits and affected
  skills against this registry. Report what to adopt, adapt, or defer and why.
  Integrate accepted updates on the review branch, verify affected behavior
  and references, then use the same PR workflow. A scheduled check produces
  findings for that decision; merge and installation remain explicit actions.
- Use observed failures to prioritize standard-skill improvements. For personal
  or experimental skills, choose use as-is, adaptation, leaving uninstalled, or
  retirement. Before removal, check callers, router entries, docs, and package
  references; record the decision here so upstream updates can be reconciled.

The initialization change introduced this policy and its instruction pointer
without changing Skill behavior. Entries below track subsequent implementations.
`Candidate` means a local implementation awaiting behavioral and owner review;
it is not a released or installed change.

## Baseline

Reviewed on 2026-09-22 for [maintenance issue #37](https://github.com/Ghroth6/skills/issues/37):

- Previous upstream base: [`6654f6b`](https://github.com/mattpocock/skills/commit/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76).
- Fork before integration: [`7e435cc`](https://github.com/Ghroth6/matt_skills/commit/7e435cca796613837de8d40d93ad3e8056d6fd71).
- Integrated upstream snapshot on the review branch: [`c55ee46`](https://github.com/mattpocock/skills/commit/c55ee46073ed923f86ce59a5eb3b6d895095d1b7),
  covering 15 upstream-only commits and nine changed files.
- **Adopt:** `retro` prioritizes deterministic checks for mechanical mistakes;
  `pr` supplies an experimental PR body reference; the maintainer link script
  excludes `deprecated/` and `misc/` while retaining `in-progress/`.
- **Adapt:** resolve the `CLAUDE.md` installation conflict by documenting the
  new exclusions while preserving this fork's `skills` installation route.
  Align the experimental index and pending `pr` changeset with the current
  Skill bodies. Add the optional `pr` route to `ask-matt` and its docs, as the
  repository's routing rule requires. Reconcile these small documentation
  differences again when upstream updates the same descriptions or router.
- **Preserve/defer:** P001 remains implemented; upstream has not changed
  Wayfinder or replaced incremental capture. P002 and P003 remain proposed.
  `pr` and `retro` stay experimental and outside promoted plugin packaging.
  The owner decides when to merge the review PR; installed copies update
  separately after that decision.

**Validation:** Plugin version, Bash syntax, Markdown references, and whitespace
checks passed. Running only the link script's selection expression on the
integrated tree selected 34 Skills instead of 38, excluding the four `misc/`
Skills while retaining `pr` and `retro`. All 38 Skills' YAML and invocation
policies match the repository contract; the plugin still contains exactly
the 25 promoted Skills. Wayfinder files, P001-P003 entries, fork installation
docs, and plugin manifests match the pre-merge fork. This is structural and
selection validation, not a new behavioral replay of the experimental Skills;
the installer was not run.

## P001: Wayfinder incremental capture

**Status:** Implemented.

**Problem:** During long exploration, user corrections, constraints, rationale,
and unresolved questions can be lost before the first map is created.

**Upstream behavior:** [Chart the map](skills/engineering/wayfinder/SKILL.md#chart-the-map)
names the destination and explores the frontier before creating the map and
its decision tickets. Domain modeling can already capture settled language
and architecture decisions during discussion. The remaining gap is a reliable
capture and recovery path for important information outside those artifacts.

**Desired behavior:** Preserve important semantic changes during exploration,
including before a map exists. A fresh session can find the current goal,
constraints, corrections, rationale, and open questions through durable
artifacts and their references. Keep confirmed decisions distinct from
tentative ideas and agent proposals.

**Rationale:** A final summary cannot reliably recover information already
lost from the conversation. Capture should preserve the meaning and reasons
needed to continue, while keeping each meaning in one authoritative place.

**Implementation:** [Incremental capture](skills/engineering/wayfinder/incremental-capture.md)
preserves material changes before the next charting round. Reuse the effort
issue for information without an existing authoritative home; create an
ordinary issue only when needed and authorized. Read back the saved content
and expose that issue as the continuation entry. Absorbed information becomes
references to its proper home. This adds no independent Skill or Host hook.

**Validation:** The implemented instructions were evaluated at
[`2c3f165`](https://github.com/Ghroth6/matt_skills/commit/2c3f165e04e7ff9f8c104e2b542ce5a5f078b976).
In one synthetic replay per arm, both baseline and candidate preserved the
important meaning when an effort issue already existed. Without an existing
issue, baseline saved only a glossary; candidate created an effort issue from
which a fresh reader recovered scope, corrections, rationale, and unknowns.
A stale initial-state sentence in the recovery fixture was removed for both
arms before that comparison. Candidate boundary checks found no write for
an unchanged short discussion and an explicit unsaved gap under read-only
authorization. Invocation metadata is unchanged from upstream.

**Limits:** These are small instruction-level replays, not an automatic
compaction or cross-Host reliability benchmark. Multi-round behavior, source
absorption, concurrent edits, and transport-level tracker failures still need
field evidence. The rule works within the configured tracker's authorization.

**Related upstream issues:** [#716](https://github.com/mattpocock/skills/issues/716)
concerns session boundaries; [#944](https://github.com/mattpocock/skills/issues/944)
reports map growth and lost content. Both are adjacent evidence, not an
accepted upstream implementation of pre-map capture.

## P002: Planning confidence horizon

**Status:** Implemented; owner accepted on 2026-09-23.

**Problem:** Exploration can turn into a large implementation roadmap whose
later steps depend on assumptions that earlier work has not validated.

**Upstream behavior at the starting baseline:** [Wayfinder guidance](docs/engineering/wayfinder.md)
already recommends bounded destinations and prototypes. Its Skill separates
decision tickets from fog. [to-spec](skills/engineering/to-spec/SKILL.md)
requested extensive user stories, and
[to-tickets](skills/engineering/to-tickets/SKILL.md) slices the supplied work.

**Desired behavior:** Detail implementation only where the current evidence
supports it, and revisit future work when a completed slice changes that
evidence. Preserve goals, constraints, decisions, and acceptance examples as
the contract. A precise unanswered question may be a decision ticket even
when blocked; that does not make its implementation ready.

**Rationale:** A plausible route is a revisable hypothesis. Planning should
keep unknowns visible instead of silently turning them into commitments.

**Open design:** Determine where an additional readiness check changes actual
behavior beyond the existing bounded-destination and fog guidance.

**Candidate:** `wayfinder`, `to-spec`, and `to-tickets` distinguish precise
decision questions, evidence-supported implementation, readiness, and dependency
completion. Spec length is driven by agreed behavior and acceptance examples.
Generated work is not automatically ready. The existing tracker vocabulary
expresses a material gap without introducing a new workflow state.

**Related upstream evidence:** The waterfall failure report and response in
[Wayfinder's documentation](docs/engineering/wayfinder.md). No separate
upstream issue is asserted as acceptance of this personalization.

## P003: Cross-artifact fidelity

**Status:** Implemented; owner accepted on 2026-09-23.

**Problem:** Important meaning and evidence can disappear across conversation,
map, specification, implementation issues, and implementation.

**Upstream behavior at the starting baseline:** Wayfinder links decision details from an index;
`to-spec` and `to-tickets` allow decision-rich prototype snippets. The baseline
[implement](skills/engineering/implement/SKILL.md) entrypoint does not
explicitly require loading related decisions, comments, and prototype assets.

**Desired behavior:** At each conversion, locate the important requirements,
user corrections, exclusions, and acceptance examples in the resulting
artifact or its relevant source references. Implementation can retrieve that
evidence in a fresh session without guessing missing product intent.

**Rationale:** References preserve access to primary evidence across stages;
repeated prose summaries can lose constraints even when each looks coherent.

**Open design:** Establish bounded source loading and a useful fidelity check
without requiring every agent to read the entire project history.

**Candidate:** `to-spec`, `to-tickets`, `implement`, and `handoff` preserve
material corrections, exclusions, rationale, and acceptance examples through
specific source references. Implementation reads the current task/comments and
expands only relevant references; unavailable unrelated history does not block
work. Close-out compares observable evidence with the current contract and
records unverified boundaries. Its review receives a diff containing the work;
a local checkpoint accommodates the review skill's commit-range interface.

**Related upstream issue:** [#892](https://github.com/mattpocock/skills/issues/892)
reports missing ticket and Wayfinder evidence. Its proposed implementation
has not been adopted by this fork.

## P004: Outcome-based session boundaries

**Status:** Implemented; owner accepted on 2026-09-23.

**Problem:** Fixed context thresholds and mandatory switches can discard useful
reasoning, while a single visible session may already contain host compactions.

**Candidate:** `ask-matt` and its phase reference favor coherent related phases
and fresh context for independent outcomes, with saved sources as the recovery
entry. Wayfinder retains one-ticket stopping by default. Explicit user-requested
continuation saves the resolution and rechecks blockers/claims before one next
decision. Planning remains planning unless the user authorizes execution;
agent-written map Notes cannot grant that permission.

**Upstream difference:** This is a downstream exception, not adoption of
[issue #716](https://github.com/mattpocock/skills/issues/716), which asks for
stronger stopping. User-invoked metadata and session-creation authorization stay
unchanged.

## P005: Scoped grilling with delegated implementation choices

**Status:** Implemented; owner accepted on 2026-09-23.

**Problem:** Repeating settled questions or escalating delegated reversible
details spends human attention without resolving product uncertainty.

**Candidate:** `grilling` bounds its tree to the agreed decision, reuses settled
answers, and states significant delegated defaults. Material behavior, scope,
data consequences, external commitments, and hard-to-reverse tradeoffs remain
human decisions. Shared understanding and user confirmation remain the stop
condition; there is no numeric question cap or automatic plan execution.

**Upstream difference:** A targeted local adaptation, not an accepted fix for
[issue #1112](https://github.com/mattpocock/skills/issues/1112). It preserves the
maintainer's shared-understanding position in
[issue #487](https://github.com/mattpocock/skills/issues/487).

## P006: Proportionate diagnosis with real-device evidence

**Status:** Implemented; owner accepted on 2026-09-23.

**Problem:** A mandatory fast agent-only repro can cause irrelevant mocks or
block useful inspection when the actual failure needs slow equipment/manual work.

**Candidate:** `diagnosing-bugs` starts with a useful inspection and reserves its
full loop for difficult defects. Provisional hypotheses may construct the loop;
slow structured human runs can supply real failure evidence. Missing access
keeps verification incomplete. Host substitutes alone cannot establish a device
fix, and no exception grants device or production-write permission.

**Upstream difference:** The lighter-first direction has a maintainer response
in [issue #578](https://github.com/mattpocock/skills/issues/578). The concrete
hardware and verification rules are downstream choices, not upstream approval.

## Candidate validation and future reconciliation

The [local scope](docs/research/personal-workflow-candidate.md),
[upstream review](docs/research/personal-workflow-upstream-review-20260923.md), and
[replay fixtures](docs/research/personal-workflow-replay-cases.md) define this
candidate. The [validation report](docs/research/personal-workflow-validation-20260923.md)
records behavioral results separately from owner acceptance.

On an upstream update, compare affected skills, human docs, and router entries
against P001-P006. Retire a local patch when upstream solves its actual problem.
Check both overlapping text and silent semantic contradictions; a clean merge
does not prove compatibility. Keep project facts in project configuration and
these reusable workflow differences in source. Publish the reviewed fork before
updating installed copies from it; do not edit installations as another source.

## Accepted workflow revision (2026-09-23)

The owner accepted P002-P006 after reviewing the behavior and local validation.
Implementation commits: `4af6247` and `820eb77`. The
[validation report](docs/research/personal-workflow-validation-20260923.md)
records the synthetic comparisons, structural checks, independent review
corrections, and remaining field-validation limits. Acceptance approves this
workflow for use; it does not establish long-term or cross-model reliability.

Delivery is tracked by [maintenance issue #38](https://github.com/Ghroth6/skills/issues/38).
Installed copies are updated from reviewed `main` after the delivery PR merges.