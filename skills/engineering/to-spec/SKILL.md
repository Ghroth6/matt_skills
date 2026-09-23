---
name: to-spec
description: "Turn the current conversation into a spec and publish it to the project issue tracker: no interview, just synthesis of what you've already discussed."
disable-model-invocation: true
---

This skill takes the current conversation context and codebase understanding and produces a spec. Do NOT interview the user; just synthesize what you already know.

The issue tracker and triage label vocabulary should have been provided to you. If not, tell the user to run `/setup-matt-pocock-skills`.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the spec, and respect any ADRs in the area you're touching. Read a supplied issue's body and comments, and follow decision or prototype references that affect this scope. Keep confirmed requirements, user corrections, exclusions, and acceptance examples traceable to their relevant sources. Expand references only to resolve meaning needed here, rather than loading the whole project history.

2. Sketch out the seams at which you're going to test the feature. Existing seams should be preferred to new ones. Use the highest seam possible. If new seams are needed, propose them at the highest point you can. The fewer seams across the codebase, the better - the ideal number is one.

Reuse seams the user already agreed. Check a new seam with the user when it
changes what acceptance proves; choose ordinary test placement within an
agreed seam without reopening the decision.

3. Write the spec using the template below. Detail implementation only where
current evidence supports it; distinguish confirmed choices from hypotheses
and unresolved questions. Before publishing, check that material corrections,
exclusions, rationale, and acceptance examples survive in the spec or its
relevant source references. A reference must expose the needed meaning, not
just point at a large map.

Publish within the task's tracker authorization. Use the configured readiness
label only when scope and acceptance are clear and material decisions are
settled; otherwise record the specific gap with the configured non-ready
status. Dependencies and readiness are separate. No extra triage round is
needed merely because this skill generated the artifact.

<spec-template>

## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A numbered list covering the agreed scope. Each user story should be in the format of:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

Include enough stories to cover materially distinct behavior, not a target
length or speculative future work. Add concrete acceptance examples where a
summary could hide a boundary, failure case, or important user interaction.

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Avoid prescribing file paths or code snippets as an implementation recipe that
will go stale. Preserve source references by issue, document path, or revision
when they carry a decision or evidence the next agent needs.

Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it within the relevant decision and note briefly that it came from a prototype. Trim to the decision-rich parts, not a working demo, just the important bits.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)

## Out of Scope

A description of the things that are out of scope for this spec.

## Further Notes

Relevant decision and prototype references, remaining assumptions or questions,
and what observation would make later work ready to specify. When a completed
slice invalidates a premise, revisit the affected plan before treating it as
an implementation commitment.

</spec-template>
