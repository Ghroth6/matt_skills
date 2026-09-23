# Personal workflow replay cases

These are synthetic, anonymized source fixtures for instruction-level replays.
They are not live tracker tasks or permission to mutate external systems.
Treat each case as a fresh request. Use only its named Skill package and raw
fixtures. State the next actions and draft the requested artifact in your
response; identify source reads by fixture name. Do not run implementation,
tests, tracker writes, device actions, or nested agents. Report what the
provided instructions cause you to do, including any limitation or conflict.
Keep each response focused, at most 220 words. There is no target answer here.

## R1: Implement a corrected task

Skill: engineering/implement.
User: "Implement lab/tools#65. The source and test seams below are ready.
Choose ordinary code organization yourself. Work locally; no push or device
access. Explain any material missing information."

Sources available through the fixture reader:
- Ticket body: "Deliver a resource-statistics method for supplied ELF/map
  files. Produce module totals and attributable detail; validate against an
  existing toolchain sample. Formal baseline and budgets are later work.
  See comment C2 and design D1."
- Comment C1 (older): "Freeze the firmware baseline before starting."
- Comment C2 (latest, owner): "C1 is superseded. Deliver the method first;
  generated samples are method validation, not the formal resource baseline.
  Shared allocations must not be counted twice."
- D1: "Use the existing parser seam. The accepted prototype P1 demonstrates
  a separate 'unattributed' row; keep that behavior."
- P1: sample output has A=20, shared=5, unattributed=2, total=27.
- Parent map index: includes D1, unrelated meeting notes Z1, and migration Z2.
- Z1/Z2: unavailable.

Respond with the implementation scope, source reads, and next step.

## R2: Convert a discussion into a spec

Skill: engineering/to-spec.
User: "Write the spec locally from our decisions; do not publish yet."
Conversation: log recording supports selecting types and starting a task.
Owner correction: stopping must select task IDs per device, keeping older
unselected tasks running. Export retains the newest file of each selected
category, even if its filename is old. Directory structure agreed:
batch/device/category. The service seam and its tests were already confirmed.
Auto-deletion policy is undecided; users have not chosen age/count precedence.
Later remote upload is just an idea. Prototype P2 shows per-device stop selection.
Tracker config: ready-for-agent means material product choices settled;
needs-info means a required answer is missing. Blocking links are separate.

Draft scope, representative acceptance examples, source references, and status.

## R3: Slice a partially known plan

Skill: engineering/to-tickets.
User: "Draft tickets only. Split what is ready and show what still needs a
decision. We can implement the established path first."
Spec: local reset removes authentication and Wi-Fi records, reboots, and
verifies the cleared state. This path and acceptance are agreed. Ethernet and
static-IP cleanup depend on another team's API and ownership decision. A
statistics parser can be built independently from recorded samples; whole
device peaks need later scenarios. UI and service for reset need to work
together to demonstrate the slice. Host parser checks already pass on the base.
Tracker vocabulary is the same as R2; every draft has no existing blocker ID.

Draft the smallest useful tickets/questions, acceptance, readiness, dependencies.

## R4: A grilling round

Skill: productivity/grilling.
User: "Grill this deletion feature. Batch directory layout and UTF-8 are
already agreed. You may choose reversible helper naming and JSON formatting.
I have not decided whether pinned batches can ever be auto-deleted. There is
no need to decide future cloud synchronization."
Facts: local storage can identify pinned batches and a configurable age limit.
No external facts need investigation.

Give the next response and explain when this interview would be complete.

## R5: Walking a map at a boundary

Skill: engineering/wayfinder.
Map M: planning only; no execution override. Decision A is resolved, its
comment saved and read back. B is the next related unclaimed question. C is
an independent blocked question. B needs the user's product decision.
Current user turn in run 1: "Thanks, A is clear."
Current user turn in run 2 (a separate run): "A is clear. Continue B here;
keep this planning only."

Give the next action for each run, including tracker state reads and stopping.

## R6: Slow hardware diagnosis

Skill: engineering/diagnosing-bugs.
User: "Diagnose why reset leaves the old Wi-Fi entry after reboot. You may
inspect local code and propose a patch. I can run the board; don't flash it."
Raw observation H1: operator executes Reset, device restarts after four minutes,
then a query returns the old Wi-Fi entry. Same procedure reproduced twice.
Raw log H2: delete success, reboot request, startup, old Wi-Fi entry present.
Host test T1: mock delete returns success; test passes. No real storage is used.
Relevant code is available for read-only inspection. Board access is manual.

Give next diagnostic actions and what can be claimed from current evidence.

## R7: A short explanation request

Skill: engineering/diagnosing-bugs.
User: "What does 'connection refused' generally mean? Give a short explanation;
I'm not asking you to debug a project or change anything."
No repository or service is supplied.

Respond to the user.

## R8: Handoff a partial verification

Skill: productivity/handoff.
User: "Hand this to the next agent for GUI verification; draft the document."
Current task: select which recording tasks to stop. Commit abc123 implements
the service; 12 parser tests pass. GUI has not been launched. Issue I8 current
body requires keeping other tasks running. Owner correction C8 rejects the old
'stop all' design. Screenshot P8 is a design prototype, not execution evidence.
Next agent has the same repo at commit abc123. Remote push was not authorized.

Draft the handoff, including specific source pointers and the next action.

## R9: Related phases in one task

Skill: engineering/ask-matt, including PHASE-BOUNDARIES.md.
User: "We just agreed the small parser change and its checks. Should I open a
new task before implementing? The UI task also still needs a separate design.
Tell me the next step; do not create anything."
The discussion is coherent, sources saved, no known context pressure. The host
does not expose a remaining-token estimate.

Recommend how to proceed and what would make a different boundary useful.

## R10: A fully specified local slice

Skill: engineering/to-tickets.
User: "Draft one implementation ticket for the agreed parser extension. Keep
this local; the breakdown is already agreed."
Accepted output contract: parse CSV columns module,bytes; emit JSON totals by
module plus grand_total. Input fixture: A,2; A,3; B,4. Expected output:
{"modules":{"A":5,"B":4},"grand_total":9}. Reject a negative byte count
with INVALID_BYTES. A base-commit run sums only the first row for each module,
returning A=2, B=4, grand_total=6. The public CLI seam and JSON keys are agreed.
No dependencies or pending decisions. Preserve unrelated base tests.
Tracker vocabulary is the same as R2.

Draft the ticket and its readiness; state whether you need another user answer.
