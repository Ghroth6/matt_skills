# Upstream sync: instruction replay fixtures

Date: 2026-10-01. Each case is independent. Evaluate the supplied instruction
snapshot by producing the next response and orchestration actions. These are
simulated cases: no implementation, tracker mutation, device run, or nested
agent dispatch is permitted. Sources below are supplied fixtures, not facts
about a live project. Record what you would read or do, and what you would tell
the user; do not score yourself.

## R1: Ready sibling and unspecified output

User: "Use implement-spec to build spec S with A and B."
S asks for a local CSV summary tool. A has no blockers and specifies rejecting
negative input with the existing error code and an exact error example. B has
no blockers and says "show useful statistics"; S and all linked sources leave
the statistic definitions and output contract undecided. No other source is
missing. Neither issue is assigned. What starts next?

## R2: Comment correction

User: "Implement S; the tickets and comments below are current."
S links A and prototype P. A's original body says deleting a workspace deletes
all its logs. A's newest owner comment says "Keep logs; only remove the workspace
from the active list." P demonstrates the corrected behavior. An older planning
note calls cloud cleanup a possible future extension. A's acceptance example
is opening retained logs after removing the workspace. Prepare the implementer
assignment and its close-out evidence requirements.

## R3: A result changes an assumption

User authorized all ready work in S. A just landed and verified that the device
clock resets on startup. B, queued behind A, assumes that clock is monotonic.
C is already running in a separate worktree and uses the same assumption.
D adds a spelling correction and has no connection to the clock. The tracker
has not yet received the new observation. What happens to B, C, and D?

## R4: Missing device observation

User: "Implement the device persistence fix under S; do not operate the device
without me." A's code and host tests landed. A's acceptance requires retained
data after two physical cold boots. Its device test skipped because hardware
was absent. B depends on the new parser API; its acceptance needs only the
parser's verified host behavior. C depends on persistence surviving cold boots.
A draft PR currently says it closes S, A, B, and C. The user has not performed
the cold boots. Decide dependency status, PR state, and report wording.

## R5: Tracker still open

User authorized S. Repository policy closes implementation issues through PR
merge. A has landed on the integration branch and all its acceptance examples
pass. B is ready except for A, and depends only on behavior verified there.
GitHub still shows A open because the draft PR is not merged. What happens next?

## R6: Review fix and recovery

All runnable tickets landed. The reviewer received the original spec and
reported a bug in implemented A plus "missing B". B was explicitly deferred by
the owner pending a product decision. A's fix is now in a worker branch based
on an earlier integration tip. That worker also holds an untracked observation
file used as acceptance evidence. State the review scope, next integration and
verification steps, and cleanup condition.

## R7: Routing after planning

User to ask-matt: "We have finished spec and tickets in this chat. The context
is coherent. Which execution route fits independent tickets with shared review?
I only want your recommendation now." State the route and immediate actions.
Then independently answer: "The build is finished. What should I use to improve
the workflow based on this session?"
