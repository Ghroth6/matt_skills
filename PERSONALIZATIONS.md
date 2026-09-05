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

The initialization change introduced this policy and its instruction pointer
without changing Skill behavior. Entries below track subsequent implementations.

## Baseline

Checked on 2026-09-06:

- Fork base: [`6654f6b`](https://github.com/mattpocock/skills/commit/6654f6b60cd9d5be8b54c6fafe44346dabeb3b76).
- Upstream `main`: [`3cca18b`](https://github.com/mattpocock/skills/commit/3cca18b368ae95cdbdebbff572ccafa662551015).
- The fork is two commits behind this upstream snapshot. Those changes affect
  `scripts/link-skills.sh` and its description in `CLAUDE.md`; the Skill flows
  discussed below are unchanged. This initialization does not integrate them.

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

**Status:** Proposed.

**Problem:** Exploration can turn into a large implementation roadmap whose
later steps depend on assumptions that earlier work has not validated.

**Upstream behavior:** [Wayfinder guidance](docs/engineering/wayfinder.md)
already recommends bounded destinations and prototypes. Its Skill separates
decision tickets from fog. [to-spec](skills/engineering/to-spec/SKILL.md)
still requests extensive user stories, and
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

**Related upstream evidence:** The waterfall failure report and response in
[Wayfinder's documentation](docs/engineering/wayfinder.md). No separate
upstream issue is asserted as acceptance of this personalization.

## P003: Cross-artifact fidelity

**Status:** Proposed.

**Problem:** Important meaning and evidence can disappear across conversation,
map, specification, implementation issues, and implementation.

**Upstream behavior:** Wayfinder links decision details from an index;
`to-spec` and `to-tickets` allow decision-rich prototype snippets. The current
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

**Related upstream issue:** [#892](https://github.com/mattpocock/skills/issues/892)
reports missing ticket and Wayfinder evidence. Its proposed implementation
has not been adopted by this fork.
