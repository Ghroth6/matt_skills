---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Keep the tree within the agreed decision or deliverable. Reuse answers already
settled in the conversation or relevant sources. Ask about material product
behavior, scope, data consequences, external commitments, and hard-to-reverse
tradeoffs. When the user has delegated ordinary reversible implementation
choices, make those choices and briefly state significant assumptions instead
of turning them into interview questions. An uncertain product requirement is
not an implementation default. Leave unrelated future branches explicitly for
later rather than expanding this interview to cover the whole product.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round: number each question and give your recommended answer. Then wait for the user's answers before the next round.

Format a round like so:

```
❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>

---

❓ **Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>
```

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The material, non-delegated _decisions_ are the user's: put each to them and wait.

The interview is done when the in-scope frontier is empty: material decisions
are settled, delegated choices are stated, and deferred questions are visible.
Keep the shared-understanding criterion, with no numeric question cap. Do not
act on the resulting plan until the user confirms it; an existing explicit
confirmation remains valid unless a material change reopens it.
