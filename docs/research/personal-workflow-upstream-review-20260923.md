# Personal workflow changes: upstream compatibility review

Checked: 2026-09-23. Sources were read from public GitHub issue bodies and comments with `gh api`, upstream source files, and this fork's personalization registry. This is a design and maintenance review, not a behavioral benchmark of Astra or Sol.

Upstream `main` at inspection: [`c55ee46073ed923f86ce59a5eb3b6d895095d1b7`](https://github.com/mattpocock/skills/commit/c55ee46073ed923f86ce59a5eb3b6d895095d1b7). Fork starting point: [`ca1a9516c8066cbaa4a5374a6d3ed6f1fc087ca0`](https://github.com/Ghroth6/matt_skills/commit/ca1a9516c8066cbaa4a5374a6d3ed6f1fc087ca0). Issue states below are a dated snapshot. An open community proposal is not evidence that the maintainer accepted or implemented it.

## Conclusion

Personal adaptation is explicitly part of the upstream distribution model. Most of the proposed work strengthens existing purposes: preserve decisions, keep plans within available evidence, and get useful feedback. Two changes need especially careful wording: overriding Wayfinder's session boundary is a deliberate downstream exception, and replacing grilling's shared-understanding stop condition would conflict with a stated maintainer position.

Proceed with small, recorded changes that preserve the underlying disciplines. Do not describe the whole candidate as upstream-approved, and do not treat a clean Git merge as proof of behavioral compatibility.

## What upstream actually permits and encourages

The upstream README describes the skills as small, adaptable, composable, and usable with any model. It expressly invites users to make them their own. It separates a managed, read-only Claude plugin from editable copies installed through `skills.sh`; the latter route is intended for customization. Thus the personal fork is not an illicit or accidental use of the project. These are stated intentions, not evidence that all models behave identically. [README at inspected commit](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/README.md).

The repository carries the MIT license, which permits modification and distribution subject to retaining its copyright and permission notice. This license permission is separate from endorsement of a particular workflow. [License](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/LICENSE).

Matt-authored, closed issue #88 establishes a narrower customization seam: tracker backend, label strings, and domain-document locations belong in user-owned `AGENTS.md` and supporting files. Its rejection of editing installed skill files concerns the managed, symlinked plugin update model. It is not a general prohibition on maintaining a source fork. The current distribution ADR separately distinguishes editable copies from a read-only subscription. [Issue #88](https://github.com/mattpocock/skills/issues/88), [distribution ADR](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/.agents/adr/0002-ship-as-a-claude-code-plugin.md).

**Practical implication:** use project configuration for project facts and personal communication preferences. Change source skills when the desired behavior is a reusable workflow invariant that project configuration cannot reliably express. Keep installed copies as outputs of the reviewed fork, rather than a second editable source.

## Assessing each proposed change

| Candidate | Fit with upstream | Recommended boundary |
| --- | --- | --- |
| P002: planning confidence horizon | Strong fit with bounded destinations, prototypes, and visible unknowns. Upstream docs themselves describe later tickets becoming invalid when earlier discoveries change assumptions. | Separate precise decision questions from implementation readiness. Revisit affected downstream work after new evidence. Do not add a mandatory readiness ceremony to every simple task. |
| P003: cross-artifact fidelity | Strong fit with decisions living once and remaining accessible through links. Community reports identify this exact missing behavior. | Load sources that can affect current scope, constraints, acceptance, or design. Preserve corrections and prototype evidence. Avoid recursively reading all history or copying every source into every artifact. |
| Continue a related Wayfinder ticket in the same session when the user requests it | A deliberate downstream exception. Upstream normally permits only research as the exception to one ticket per session. Generic phase guidance does prefer continuing when the next phase needs current reasoning. | Keep the one-ticket default, save the completed resolution first, and make user-authorized continuation explicit. Do not let an agent write its own map note as permission to implement or keep expanding scope. |
| Bounded grilling and autonomous ordinary choices | Avoiding redundant questions fits the goal. A numeric cap or replacing shared understanding with a mechanical checklist conflicts with maintainer feedback. | Keep shared understanding and human control over consequential choices. Limit the tree to the agreed scope, reuse settled answers, and state reversible defaults. Do not silently resolve disputed product decisions or claim the user confirmed without an answer. |
| Device-friendly and proportional diagnosis | The maintainer supports starting lighter and escalating where necessary. Device-specific relaxation is our extension. Existing text already allows a human-assisted loop, but demands one command, seconds, and its Bash template. | Preserve observation of the actual symptom, falsifiable hypotheses, discriminating evidence, and original-scenario verification. Accept bounded slower or human-assisted device procedures; code reading may help construct the loop. Mark unverified causes and fixes honestly. |

Sources for this assessment: [Wayfinder docs](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/docs/engineering/wayfinder.md), [phase boundaries](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/skills/engineering/ask-matt/PHASE-BOUNDARIES.md), [grilling source](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/skills/productivity/grilling/SKILL.md), [diagnosing source](https://github.com/mattpocock/skills/blob/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/skills/engineering/diagnosing-bugs/SKILL.md), and the dated issue evidence below. The assessment and recommendations are our inference, not quoted maintainer approval.

## Related upstream discussions

| Source and checked status | Evidence | What it does and does not establish |
| --- | --- | --- |
| [#892](https://github.com/mattpocock/skills/issues/892), open | The reporter says `implement` misses ticket comments, Wayfinder decisions, prototypes, and linked artifacts. A second user reports UI differences after prototype evidence was lost. | Direct support for P003's problem. The long proposed evidence-graph implementation is a community solution, with no maintainer acceptance in the inspected comments. Its breadth should not be copied wholesale. |
| [#689](https://github.com/mattpocock/skills/issues/689), open | Decisions and trade-offs disappear when grilling is converted to a spec, causing drift and repeated questions. | Independent adjacent report supporting fidelity checks at conversion, not just implementation startup. No maintainer reply inspected. |
| [#579](https://github.com/mattpocock/skills/issues/579), open | Tracker decisions can be closed while durable domain context is stranded on worktrees or prototype branches. A commenter reports later agents reopening settled decisions. | Supports preserving durable, resolvable source pointers. It does not authorize automatic branch integration or prove a new parallel-work mechanism is necessary for this candidate. |
| [#944](https://github.com/mattpocock/skills/issues/944), open | Reporter describes map growth, lost index content, and tracker limits; suggests budgets and pagination. | A community incident report, not independently reproduced platform behavior. Useful warning against an ever-growing duplicate ledger. Pagination is separate work and is not solved by P003. |
| [#716](https://github.com/mattpocock/skills/issues/716), open | Requests an explicit stop and restart entry after a Wayfinder resolution. | Counter-evidence to unconditional same-session chaining. This request favors stronger stopping, not our proposed user-authorized exception. No maintainer reply inspected. |
| [#1112](https://github.com/mattpocock/skills/issues/1112), open | Requests a third category for sensible defaults alongside facts and user decisions; cites questions about implementation details and already answered matters. | Very close to the proposed question filter. It explicitly avoids a numeric cap. No maintainer acceptance inspected. |
| [#962](https://github.com/mattpocock/skills/issues/962), open | Requests user-facing behavioral choices, with exact engineering mappings recorded afterward. | Useful question-writing guidance, not proof that every technical term must be hidden from an expert. No maintainer reply inspected. |
| [#1071](https://github.com/mattpocock/skills/issues/1071), open | Reports skill bloat, opaque vocabulary, inconsistent routing, and diagnosis firing during ordinary conversation. | Evidence that workflow burden is not unique to this user. It is subjective field feedback with no controlled model comparison or maintainer reply in the inspected thread. |
| [#578](https://github.com/mattpocock/skills/issues/578), open | GPT-5.6-Sol users report excessive invocation and heavy reproduction workflows. | Matt's [owner comment](https://github.com/mattpocock/skills/issues/578#issuecomment-4979112951) suggests lighter diagnosis first, escalating if needed. This is maintainer support for that direction, not a merged fix or a current Astra/Sol benchmark. |
| [#44](https://github.com/mattpocock/skills/issues/44), closed | Discussion of hundreds of grilling questions. Matt tells users that they remain in charge and can steer the conversation. An owner-posted closure rejects numeric limits. | Direct support for natural-language control. The closure explicitly discloses AI-assisted triage, which should not be hidden when characterizing its provenance. |
| [#282](https://github.com/mattpocock/skills/issues/282), closed | Policy issue rejects hard question caps and separates useful exploration from redundant questions. | Supports removing low-value questions rather than introducing a counter. The issue author is a community member; owner statements in #44 independently support the no-cap policy. |
| [#487](https://github.com/mattpocock/skills/issues/487), closed | Proposed alternative stop condition and approximately five high-impact questions. | Matt's [owner reply](https://github.com/mattpocock/skills/issues/487#issuecomment-4924774328) defends shared understanding as an effective stop. Do not portray replacing that stop condition as upstream-aligned. The brief response does not establish rejection of every subproposal in the issue. |

The inspected open issues have no accepted or merged implementation demonstrated by their bodies or comments. This review does not exhaust every issue or pull request in the repository. Source files at the pinned commit remain the behavioral baseline.

## Corrections to the earlier proposal

1. Keep grilling's shared-understanding condition. Clarify the agreed scope and remove unnecessary questions; do not impose a number or automatically conclude when a checklist is filled.
2. Keep Wayfinder's one-ticket default. An explicitly requested continuation is a downstream exception, not the newly discovered upstream recommendation.
3. Preserve the diagnosis feedback requirement. Faster loops are desirable, but a real device's slower bounded observation can be more probative than an instant substitute that cannot reproduce the symptom.
4. Retain existing user-invoked entrypoints and the planning-versus-implementation boundary. Relaxing session choreography must not create permission to publish, merge, deploy, erase data, or start product implementation.
5. Do not maintain separate Astra and Sol variants yet. #578 concerns GPT-5.6-Sol, and the reports here do not establish current model-specific behavior. Evaluate the same candidate under named actual runtimes before deciding whether a model-specific exception is needed.

## Update compatibility and maintenance advice

Upstream updates can conflict in two ways. Git can flag overlapping lines, but a merge without conflicts can still introduce contradictory instructions, stale routing, or mismatched docs. This is an inference from the shared files being edited, not a claim that future conflicts are guaranteed.

Use the fork's existing [personalization registry](https://github.com/Ghroth6/matt_skills/blob/ca1a9516c8066cbaa4a5374a6d3ed6f1fc087ca0/PERSONALIZATIONS.md) as the reconciliation checklist:

- Record each behavior, the problem it addresses, its upstream difference, and the validation actually performed. Keep proposed and implemented status distinct.
- Review new upstream commits against the last reviewed upstream SHA, then against each affected personalization. Adopt upstream solutions and retire redundant patches instead of accumulating both.
- Keep skill entrypoints, promoted human docs, and `ask-matt` routing consistent. Preserve package structure and invocation bindings.
- Compare behavioral outcomes as well as text. A source-read rule that forces full project-history loading would satisfy a literal fidelity rule while defeating its purpose.
- Treat installation updates as a separate step after the reviewed fork version is approved. Do not update installations directly from Matt's repository when the intended source is this fork.

Suggested regression cases: accepted correction survives conversation-to-spec-to-ticket; a linked prototype remains findable; unresolved product choices prevent false implementation readiness; a settled answer is not asked again; ordinary reversible choices use stated defaults; a Wayfinder resolution stops by default and continues only within user authorization; an easy diagnostic question receives a proportionate answer; a slow device repro remains valid evidence while a host substitute is not reported as device verification.

Static link/YAML checks can detect packaging problems. Instruction replays can reveal behavioral regressions. Neither proves improved real-device or multi-session performance without field use. Final push and device installation remain separate user-confirmed actions for this work.
