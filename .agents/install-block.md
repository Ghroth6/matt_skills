# The canonical install block

Use these blocks for this fork's `README.md` and new installation instructions. Change them here first, then propagate. Keep the README categories **Codex, and other agents** and **For tinkerers**.

[skills.sh](https://skills.sh) installs editable skill files directly from this repository.

## Codex, and other agents

<canonical-block name="skills-sh-whole-set">

```bash
npx skills@latest add Ghroth6/matt_skills
```

Pick the skills you want, and which coding agents to install them on. **The installer lets you choose which skills to take, so make sure `setup-matt-pocock-skills` is one of them.**

To install globally for Codex without choosing an agent interactively:

```bash
npx skills@latest add Ghroth6/matt_skills --global --agent codex
```

For only the 27 published skills, select the **Mattpocock Skills** group and leave **Other** unselected. The published set is listed in [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json).

</canonical-block>

The Codex-specific command is an optional shortcut; keep the general command available. Installation does not require cloning this repository first.

## For tinkerers

<canonical-block name="skills-sh-tinkerers">

Use the same installer, on any agent, including Claude Code:

```bash
npx skills@latest add Ghroth6/matt_skills
```

It writes the skills into your repo as ordinary files you own and can edit. Nothing updates behind your back; pull my latest changes when you want them with `npx skills update`.

</canonical-block>

## Single-skill instructions

Use this form wherever one skill is named on its own:

<canonical-block name="skills-sh-one-skill">

```bash
npx skills@latest add Ghroth6/matt_skills --skill=<name>
```

```bash
npx skills@latest update <name>
```

</canonical-block>

Use `skills@latest` in new installation commands. Pages under `docs/` carry no install commands because ai-hero renders the install widget; see [writing-docs.md](./writing-docs.md).

## Marketplace metadata

The Claude Code official marketplace installs upstream, so it is not an installation route for this fork's README. `.claude-plugin/marketplace.json` remains upstream's direct-repository fallback metadata; it does not change the documented skills.sh route above. Historical release notes and ADRs describe their original context.
