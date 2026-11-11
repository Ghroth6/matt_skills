## What it does

`wait-what` is what you type when a message didn't land. The [agent](https://www.aihero.dev/ai-coding-dictionary/agent) then re-pitches what it just said. It adds the context you were missing, uses simple wording in the language you are using, and keeps your project's established terms.

The skill stays short so the [model](https://www.aihero.dev/ai-coding-dictionary/model) can focus on the re-pitch: restore the missing context and make the explanation easier to follow.

## When to reach for it

You invoke it by typing `/wait-what`. The agent will not reach for it on its own, and it shouldn't. Only you know when you stopped following.

Use it the second you notice you're skimming. The agent has drifted into jargon it invented, stacked five acronyms, or explained a decision whose premise you never saw. It fixes the conversation you're already in. To stop the jargon arriving at all, use [grill-with-docs](https://aihero.dev/skills-grill-with-docs), which builds the shared language upfront.

## The name is the mechanism

The leading word is **wait**. "Be concise" is an instruction about the agent's output, and the model obeys it by clipping words and losing you further. **Wait** is about *your* state. It says comprehension failed here. An agent that hears "be brief" writes telegrams. An agent that hears "wait, you lost me" backs up and explains.

That difference is the whole skill. Every popular fix for verbosity names the *output*: `/tldr`, `/no-fluff`, `/talk-normal`. The model over-corrects into a caveman register that is shorter and no clearer. Naming the *listener* asks for both halves at once: fewer words **and** the context you were missing.

The skill says re-pitch **that**, not "that last message". What lost you is usually bigger than one paragraph, so the agent decides how far back to go.

## It plugs into the language you already have

ASD-STE100-style wording supplies the style: short sentences, active voice, and one term per concept. Your project's `GLOSSARY.md` supplies the vocabulary; `GLOSSARY-MAP.md`, when present, points to the glossary for the relevant context.

If neither glossary document exists, the skill uses the project's established terms.

## Common questions

**Will it switch my explanation to English?**

It keeps the language you are using, including English when you are writing in English. Literal ASD-STE100 compliance is possible only in English. In other languages, the skill applies its wording rules as style constraints.

## It's working if

- The re-pitch is **shorter and clearer**, not shorter and blunter.
- It adds the premise you were missing, instead of only deleting words.
- The explanation stays in the language you are using.
- Project nouns replace invented ones, using your glossary or the terms already established in the project.
- You can use it twice in a row, and it does not degrade into terseness.

## Where it fits

You can use `wait-what` at any point, in any conversation, inside any other skill. It repairs one message after the fact. The real cure is a shared language agreed upfront, and that is [grill-with-docs](https://aihero.dev/skills-grill-with-docs): a [grilling](https://www.aihero.dev/ai-coding-dictionary/grilling) session that runs [domain-modeling](https://aihero.dev/skills-domain-modeling) as it goes, so the words you both use land in your `GLOSSARY.md`. If you're unsure which skill fits the moment, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
