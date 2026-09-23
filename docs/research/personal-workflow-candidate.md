# Personal workflow candidate

Status: owner accepted on 2026-09-23 after local validation and joint review.
Proceed with personal-repository delivery and this device update under the
previously agreed workflow. Field-reliability limits remain unchanged.

## Baseline and purpose

Fork baseline: `ca1a9516c8066cbaa4a5374a6d3ed6f1fc087ca0`.
Upstream baseline: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7`.

Complete the proposed P002 planning confidence horizon and P003 cross-artifact
fidelity. Add narrow downstream adaptations for session boundaries, delegated
implementation choices, and diagnosis on slow or human-operated equipment.
The goal is recoverable intent and observable completion with less unnecessary
ceremony. Model names, device identities, and private project details do not
belong in the reusable instructions.

## Required behavior

- Preserve P001 incremental capture, the distinction between planning and
  execution, user-invoked policies, and existing scope/authorization boundaries.
- Resolve current requirements from the task and relevant source references.
  Carry corrections, exclusions, rationale, and acceptance examples through
  spec, tickets, implementation, and handoff. Load only sources that affect the
  current work, not the entire parent tree or project history.
- Keep tentative future implementation visible as tentative. Readiness needs
  clear scope, a checkable outcome, and settled material decisions; dependency
  completion alone is insufficient. Preserve configured tracker roles and
  labels, including its distinction between blocked and needs-info work.
- Use acceptance examples that distinguish the requested behavior from the
  current defect or omission. Avoid making a long user-story list a goal.
- Continue related phases when their context is useful. Prefer fresh context
  for independent deliverables. Keep Wayfinder's one-ticket default; an
  explicit user request may continue related decision work after saving its
  resolution and rechecking the frontier. This does not authorize execution,
  unattended queue draining, or creating a new session.
- Ask the user for material decisions; exercise already delegated discretion
  for ordinary reversible implementation details and report significant choices.
- Keep a real feedback loop for diagnosis. Allow bounded inspection to create
  that loop, slow equipment and structured human observations when appropriate.
  A substitute test does not prove the original failure fixed. Missing access
  limits verification rather than granting permission or fabricating success.

## Scope and compatibility

Change existing Skill packages, their human docs, and the router. Keep the
current directory layout, invocation metadata, license, install commands, and
plugin membership. Do not add a universal workflow engine or new Skill.
Keep code-review's two-axis policy and TDD's existing contract unchanged.

Research findings distinguish maintainer statements from community proposals.
Upstream compatibility means retaining its core concepts and recording explicit
downstream differences, not claiming upstream endorsement or conflict-free merges.

## Evaluation

Compare the baseline and candidate on the same synthetic prompts and source
fixtures, including misleading historical summaries, incomplete scope,
explicit-only invocation boundaries, hardware access constraints, and session
continuation with and without user authorization. Inspect resulting decisions
and artifacts, not wording or headings. Repeat a failed case after correction.

Check package frontmatter, invocation parity, Markdown references, router/docs
consistency, whitespace, unchanged packaging, and an isolated merge against
the pinned upstream. Independent reviews assess standards and this scope.
These checks establish local candidate quality; they do not establish field
reliability, Sol/Astra equivalence, owner acceptance, or device installation.
