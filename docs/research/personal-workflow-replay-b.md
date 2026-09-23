# Offline instruction replay B

Read set: `personal-workflow-replay-cases.md`; candidate package root `C:/Users/kaihong/AppData/Local/Temp/matt-workflow-eval-20260923/candidate/skills`. Each case below is independent. These are actual replay responses, not execution reports. No implementation, tests, tracker operations, devices, nested agents, or workflow side effects were performed.

## R1

I will implement the resource-statistics method at the existing parser seam: module totals, attributable detail, shared allocations counted once, and a separate unattributed row. P1's example must retain A=20, shared=5, unattributed=2, total=27. Validation includes an existing toolchain sample; generated samples demonstrate the method only. Formal baseline freezing and budgets are later work. C2 supersedes C1, so baseline freezing does not gate this method.

Sources read: `engineering/implement/SKILL.md`; R1 ticket body, C1, C2, D1, P1, parent map index. Z1/Z2 do not affect the stated scope and need not be recovered.

Next: inspect the supplied parser/test seams and toolchain sample, establish current behavior, then implement through agreed behavior checks. Ordinary code organization is delegated. In real execution, run focused checks, regular typechecking, final suite, and review against the pre-work revision before local closeout/commit. No push or device activity.

Limitations: this fixture does not supply the ticket title, actual source/test files, or toolchain sample contents. Those reads remain pending; the contract itself is sufficiently clear to begin authorized local inspection. TDD, code review, checks, and commit are proposed steps only in this offline replay.

## R2

**Problem/Solution:** Users need selective recording, stopping, and export without interrupting recordings they did not select.

**User stories:** As an operator, I can select recording types and start a task; stop selected task IDs per device while others continue; export the newest file in each selected category under `batch/device/category`.

**Acceptance:** Device A has tasks A1/A2 and device B has B1/B2. Selecting A2 and B1 stops exactly those tasks; A1/B2 continue. For a selected category, a file with an older-looking filename but newer underlying file recency is retained over an older file with a newer-looking filename. Filename ordering must not decide newest.

**Implementation/testing decisions:** Reuse the already confirmed service seam and its tests; add externally observable checks for these examples. P2 informs per-device selection, not execution evidence.

**Out of scope:** Remote upload remains an idea. Auto-deletion is unresolved; do not invent age/count precedence.

**Status:** Local draft only. The recording/stop/export slice is decision-complete (`ready-for-agent`); any scope including auto-deletion is `needs-info` pending its policy. Readiness and blocking links are separate.

Sources read: `engineering/to-spec/SKILL.md`; R2 conversation, owner correction, directory agreement, confirmed seam, P2, tracker configuration. Actual repo/glossary/ADR and test files are unavailable here; exploration and publication were not performed. No new seam interview is needed.

## R3

Sources read: `engineering/to-tickets/SKILL.md`; R3 spec, base-test observation, and stated R2 tracker vocabulary.

1. **Reset authentication and Wi-Fi locally.** Deliver one UI-to-service reset slice that clears both record sets, reboots, and independently queries the cleared state. Acceptance: selecting reset reaches that whole path; any surviving record or absent reboot refutes completion. **Ready-for-agent; blocked by: None.** Exclude Ethernet/static-IP cleanup.
2. **Produce resource statistics from recorded samples.** Deliver an independently verifiable parser result. Acceptance: agreed recorded inputs produce the specified statistics, with a new check exposing the new behavior's present absence; retain passing host parser regressions. **Needs-info:** the fixture establishes independence but omits the output contract and expected sample results needed to make acceptance concrete. **Blocked by: None.** Recover existing sample expectations before asking for new product decisions; whole-device peaks are excluded.
3. **Decide Ethernet/static-IP cleanup ownership and API.** **Needs-info; blocked by: None recorded.** Obtain the owning team's API/ownership decision and define cleared-state observations before specifying implementation. No invented blocker ID.

Keep whole-device peak measurement as a deferred question: which scenarios and observations define a peak? It does not block the local reset or parser method.

Does this granularity and separation of dependencies fit? These remain drafts; no publishing, parent edits, testing, or implementation occurred. Existing host checks do not prove board reset acceptance.

## R4

❓ **Q1 : Pinned-batch protection:** May automatic deletion ever remove a pinned batch, including when it exceeds the configured age limit?

➡️ I recommend that pinned batches remain excluded from automatic deletion until explicitly unpinned. This is a product/data-retention decision, so I will wait for your answer rather than make it an implementation default.

Batch layout and UTF-8 remain settled. I will choose descriptive helper names and consistently formatted JSON within your delegated discretion. Future cloud synchronization is deferred outside this interview.

After your answer, I will examine only the in-scope decisions it creates. If pinned deletion is allowed, its triggering conditions need agreement; those questions depend on your first answer. The interview is complete when the in-scope frontier is empty, delegated choices are stated, and deferred matters are visible. I then summarize the plan for confirmation before acting; an already explicit confirmation remains valid unless a material change reopens it.

Sources read: `productivity/grilling/SKILL.md`; R4 user instructions and local-storage facts. No external fact investigation is needed. The unresolved pinned-deletion choice is the present constraint. This replay does not conduct subsequent rounds or implement deletion.

## R5

Sources read: `engineering/wayfinder/SKILL.md`; R5 Map M and the separate current user turns. Actual map/ticket titles, URLs, tracker configuration, and B's question text are absent; labels M/A/B/C below identify fixtures, not recovered titles.

**Run 1:** A is resolved and its saved comment was read back. Return its resolution/continuation pointer and identify B as the next related decision, then stop. “Thanks, A is clear” does not explicitly request continuing B. Do not claim B or work C. The fixture establishes A's comment readback but does not establish its closed state or the map's saved context pointer; real closeout should read/check those before reporting them complete. No new ticket work is authorized by this acknowledgement.

**Run 2:** Continue one related decision, B, under the explicit planning-only request. First re-read the affected map, A's saved resolution/context pointer, B's full question and relevant sources, and current blockers/claims; concurrent changes could alter its availability. If B remains open, unblocked and unclaimed, claim it before work. Use the grilling/domain-modeling workflow to put B's material product question to the user, then wait; never supply the user's decision. After resolution, save/read back the resolution and continuation entry, then stop. Do not drain the queue or implement. All tracker actions remain hypothetical in this replay.

## R6

H1 and H2 show the reported failure twice: Reset, four minutes to restart, then an old Wi-Fi entry. T1 proves only that the mocked deletion-success path passes; it does not test persistent storage or reboot behavior. Root cause and any fix remain unverified.

First inspect the reset/delete/reboot/startup/readback path, with relevant CONTEXT/ADRs if present. Preserve the operator loop, recording board/build identity, initial record, reset steps, timestamps, post-startup query and redacted logs. Red means the old entry remains; green requires it absent after the original reboot sequence. Necessary board latency stays explicit.

Provisional ranked hypotheses to distinguish:

1. Deletion is acknowledged before persistence; durable state still contains the entry when reboot is requested.
2. Startup restores a second saved copy; the entry disappears before restart and returns during startup.
3. Reset deletes a different storage namespace from the queried one; store identities differ.
4. Readback is stale; an independent persisted-state read disagrees with the query.

Choose targeted observations after inspection, changing one variable at a time. The operator can repeat the structured board procedure; I will not flash. Propose a patch only when source evidence supports it, plus a regression seam reaching the actual persistence pattern. Original-scenario board evidence remains required for verified-fix claims.

Sources read: `engineering/diagnosing-bugs/SKILL.md`; H1, H2, T1, access constraints. Code inspection and probes remain pending.

## R7

“Connection refused” generally means the destination actively rejected the connection. Common reasons are that no service is listening on that port, the service is stopped or bound to another interface, or a firewall explicitly rejects it. It differs from a timeout, where no usable response arrives.

Source read: `engineering/diagnosing-bugs/SKILL.md` and R7's explanation-only request. No project investigation or changes are needed; no unmet constraint prevents this general explanation.

## R8

# GUI verification handoff : draft

**Goal:** Verify selecting recording tasks to stop, while unselected tasks remain running.

**Starting point:** Same repository at commit `abc123`; the service implementation is there. Repository path and changed-file paths were not provided, so resolve them from the checkout and commit rather than inventing them.

**Required sources:** Issue I8 current body for acceptance; owner correction C8 for rejection of historical “stop all”; commit `abc123` for implementation; P8 for prototype layout only. Exact issue/comment/screenshot locations are missing from this fixture and must be recovered before GUI acceptance.

**Evidence:** Twelve parser tests passed. GUI has never been launched. Neither parser results nor P8 demonstrate GUI execution or selective stop behavior.

**Next action:** Read I8/C8 and inspect `abc123`, launch the GUI, establish multiple recording tasks, select only a subset per device, stop them, and observe selected tasks stopping while other tasks continue. Record setup, IDs, actions, actual outcomes and failures, attaching runtime captures if available. Compare behavior to the source acceptance criteria.

**Suggested skills:** `code-review` for requirements-to-diff inspection if needed; `diagnosing-bugs` if GUI verification reveals a failure.

**Boundary:** No remote push authorized. Verification remains pending.

Sources read: `productivity/handoff/SKILL.md`; R8 current-task, commit, test, I8, C8 and P8 fixtures. The skill's OS-temporary handoff save is not executed: this offline request asks only for the draft within the replay output.

## R9

Continue here for the small parser change. The decision and checks are settled, the sources are saved, and the context remains coherent. Your next step is to invoke `/implement` for that bounded parser deliverable in this task; no new task is necessary just to cross from agreement to implementation.

Keep the UI design as separate unresolved work. A fresh task becomes useful when you take up that independently scoped design with its relevant sources, or when unrelated implementation detail would obscure the current discussion. Refresh the saved decisions if repeated corrections, lost rationale, or conflicting context appear. A handoff is useful when changing harness/directory or transferring work to another person; compaction is a later option when relevant context must be retained but continuing is no longer workable.

The host supplies no remaining-token estimate, so I will not invent a token threshold or claim the context is nearly full. Coherence and recoverable decisions are the evidence available here.

Sources read: `engineering/ask-matt/SKILL.md`, `engineering/ask-matt/PHASE-BOUNDARIES.md`, and R9's saved-sources/context facts. This is routing advice only; I have not created a task, invoked implementation, or changed anything.


## R10

# Aggregate every CSV row into module totals

**What to build:** Extend the public CLI to parse CSV columns `module,bytes` and emit JSON totals by module plus `grand_total`, using the agreed JSON keys.

**Blocked by:** None.

**Status:** `ready-for-agent`. Scope, public seam, output contract, error behavior, and acceptance evidence are settled; there are no dependencies or pending decisions.

**Acceptance criteria:**

- Given rows `A,2`; `A,3`; `B,4`, the CLI emits `{"modules":{"A":5,"B":4},"grand_total":9}`. The recorded base result A=2, B=4, grand_total=6 refutes this criterion and demonstrates the missing aggregation behavior.
- A negative byte count is rejected with `INVALID_BYTES`; successful output accepting that value, or a different error, refutes this criterion.
- Preserve unrelated base tests. A regression in those tests refutes preservation.

**Relevant sources:** R10 accepted output contract, input/expected-output fixture, negative-count rule, base-commit run, agreed CLI seam and JSON keys, and stated tracker vocabulary. Instructions read: `engineering/to-tickets/SKILL.md` from the candidate snapshot.

No further user answer or breakdown approval is needed: you already approved the single-ticket breakdown. This is a local draft only. No implementation, tests, tracker publication, or parent edits were performed; the base-run evidence is supplied fixture evidence rather than a run I executed.
