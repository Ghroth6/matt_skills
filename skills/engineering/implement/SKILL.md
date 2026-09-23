---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec, ticket, or agreed conversation.

Before editing, read the current task and its acceptance criteria. For a tracker
task, resolve its repository and title, read its body and comments, then follow
the decisions, prototype assets, and parent sections that affect this work.
Expand references only when needed to establish scope, constraints, acceptance,
or the reason for a choice. The rest of the project history is not a prerequisite.

Recover the user's corrections, exclusions, and acceptance examples. Distinguish
current decisions from superseded text and tentative suggestions. Reuse settled
answers without another interview. If a required source is unavailable or a
material conflict remains, explain the affected work and ask only for what is
missing; continue independent authorized work. Readiness is established when
the current deliverable and its completion evidence are clear.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Before close-out, compare the actual behavior and verification evidence with
the acceptance criteria and exclusions, including linked examples. A passing
substitute test does not establish device, GUI, or end-to-end acceptance. State
what was observed and what remains unverified. Refresh source material if the
user reports a change or concurrent updates could alter the current contract.

Once done, call the Skill tool with "code-review". Give the reviewers the relevant
requirements, source references, verification results, and an explicit diff
that includes the implementation. If the review entrypoint requires committed
changes, make a local checkpoint first and review against the pre-work commit;
resolve actionable findings before treating the work as complete.

Commit your work to the current branch.

Report the implemented outcome, verification limits, and commit identity.
Remote publication, tracker transitions, installation, and the next work item
follow the user's authorization and repository workflow.
