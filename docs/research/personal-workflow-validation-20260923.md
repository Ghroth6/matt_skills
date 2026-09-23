# Personal workflow candidate: local validation

Date: 2026-09-23. Owner acceptance, remote publication, and installation are
pending. This report evaluates the local candidate, not field reliability.

## Versions and scope

- Before: fork `ca1a9516c8066cbaa4a5374a6d3ed6f1fc087ca0`.
- Source candidate: `4af6247cd9536df86127dacd1a2e4bbe174e38c8` on
  `codex/personal-workflow-fidelity`.
- Inspected upstream: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7`.
- Eight existing packages changed: `ask-matt`, `wayfinder`, `to-spec`,
  `to-tickets`, `implement`, `diagnosing-bugs`, `grilling`, and `handoff`.
  Their human docs and personalization registry changed with them.
- P001 capture, invocation bindings, package membership, install commands,
  license, `tdd`, and `code-review` remain unchanged.

The [scope](personal-workflow-candidate.md) and
[upstream review](personal-workflow-upstream-review-20260923.md) explain the
requirements and deliberate downstream differences.

## Instruction replays

Two agents received the same [synthetic fixtures](personal-workflow-replay-cases.md)
and separate instruction snapshots. A read only the baseline; B read only the
candidate. Neither received expected answers or the other arm's response. Both
inherited the parent runtime; this is not a Sol-versus-Astra comparison. Each
case requested a next response or local draft, with no actual implementation,
tracker writes, device operation, or nested agents. The prompts supplied source
contents directly, so they do not test live evidence retrieval.

Ten cases include two separate R5 authorization variants. R10 was added after
examining R3 as a positive control for a fully specified, ready implementation.
Both agents received that same addition. Consequently this is exploratory
evaluation, not a preregistered benchmark. There is one response per arm and
condition, without repeated-run statistics.

| Case | Baseline A | Candidate B | Interpretation |
| --- | --- | --- | --- |
| R1: corrected implementation | Preserves latest correction, prototype behavior, and local-only scope | Same, with bounded source recovery | No observed regression; no demonstrated comparative gain |
| R2: conversation to spec | Preserves selective stop and unresolved retention policy | Same, retaining acceptance examples and exclusions | Both handle supplied evidence; live retrieval remains untested |
| R3: partially known plan | Labels the parser ready using broad expected-statistics acceptance | Keeps its missing output contract visible as needs-info; reset slice remains ready | More conservative readiness on an underspecified result; recover existing evidence before another interview |
| R4: delegated choices | Chooses ordinary details, asks the material pinning question | Same, leaves future cloud work outside scope | Both preserve human control without repeated settled questions |
| R5: stop/continue | Stops by default; explicit user instruction overrides one-ticket rule | Stops by default; records the explicit continuation path | No extra autonomous queue draining in either response |
| R6: slow equipment | Requires a fast, already-run command before theories; manual repro cannot satisfy the gate | Accepts recorded real-device repro, offers provisional discriminating hypotheses, keeps verification open | Clearest observed benefit; no evidence that an actual bug was fixed |
| R7: simple explanation | Direct answer | Direct answer | User scope already controls both; no demonstrated trigger advantage |
| R8: handoff | Separates parser results, prototype, and missing GUI acceptance | Same, with source and verification pointers | No unsupported GUI-success claim in either response |
| R9: coherent continuation | Recommends continuing parser work in the same task | Same, using context coherence and recoverable decisions | Both support continuation; no need to characterize the baseline as always forcing switches |
| R10: complete contract | One ready ticket, no further approval | One ready ticket, no further approval | The new readiness rule did not create an extra gate in this control |

Raw responses: [A](personal-workflow-replay-a.md),
[B](personal-workflow-replay-b.md). Their proposed actions are not execution
evidence. R5 and R8 correctly expose missing fixture pointers rather than invent
real tracker links. Multi-round interviews, automatic compaction, concurrent
source changes, transport failures, and real device verification were not run.

## Structural and integration checks

Checks ran against the complete package set and changed Markdown, not only the
eight modified entrypoints:

- All 38 Skill headers and `agents/openai.yaml` files parse; names match folders.
- All 22 explicit-only policies match their frontmatter and baseline bindings.
- Plugin membership remains exactly the 25 promoted packages.
- Required human-doc sections, absolute human-doc links, and 18 local Markdown
  references pass. Changed prose contains no em dash. Existing external links
  were not all rechecked for availability.
- License, manifests, install block, README, P001, TDD, and review instructions
  match the baseline after normalizing checkout line endings.
- `node scripts/sync-plugin-version.mjs --check` passes at version `1.2.3`.
- `git diff --check ca1a951...HEAD` passes.
- All 38 candidate entrypoints and the phase-boundaries reference initially
  matched the replay snapshot after line-ending normalization. Review then
  corrected one router sentence about checkpoint/review order; R9 was repeated
  against the final router. The other seven modified packages retain the exact
  replayed instructions.
- A separate temporary clone at the candidate accepts
  `git merge --no-commit --ff-only c55ee46073ed923f86ce59a5eb3b6d895095d1b7`
  with `Already up to date`, leaving a clean tree. The pinned upstream is already
  an ancestor; this proves current integration only, not future merge safety.

The generic `skill-creator` validator rejects 22 packages in both baseline and
candidate because its allowed frontmatter set excludes this repository's
`disable-model-invocation` (and, where present, `argument-hint`). The rejection
map is unchanged. A host-aware YAML and binding check passes; supported invocation
metadata was not removed to satisfy the generic validator. Therefore this is
not a claim that every available validator returned success.

## Independent review

Standards and Spec reviews ran separately against `ca1a951...4af6247`.

### Standards

Three findings: the Wayfinder FAQ still described agent-written Notes granting
execution permission; the router still said review precedes any commit; several
newly revised choice branches used paragraphs instead of the required lists.
All were corrected. The independent follow-up found zero remaining Standards
findings and no new actionable smell heuristics.

### Spec

No substantive missing requirement, scope creep, or incorrect implementation
was found. One minor consistency finding overlapped the router's commit/review
ordering and was corrected. Independent follow-up confirmed zero remaining
Spec findings in the corrections.

The final-source R9 replay still recommends continuing the agreed parser work
in the same task, now also accurately describing checkpoint-based review. All
final package and Markdown checks pass with the generic-validator limitation
described above.

## Owner review and publication boundary

The local evidence supports trying this candidate. It does not establish
long-term productivity gains, equivalent behavior across models, or acceptance
by the owner. The three most useful owner checks are:

1. Are sources preserved through spec, tickets, and implementation without
   repeatedly loading unrelated history or reopening settled decisions?
2. Do coherent phases continue naturally, while material decisions and
   independent deliverables retain their appropriate boundaries?
3. Does device work advance with honest provisional reasoning and actual
   evidence, without substituting host tests for board or GUI acceptance?

Keep P002-P006 as Candidate until that joint review. Only then proceed with the
authorized personal-repository delivery workflow and installation from the
reviewed fork. No installation was performed during this validation.
