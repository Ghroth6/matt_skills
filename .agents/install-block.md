# The canonical install block

Use these commands in current fork instructions. Change them here first, then
propagate to `README.md` and any current installation examples. Historical
changelog entries and upstream release records retain their original commands.

## Install for the current user

Codex, Claude Code, and other supported agents use the same `skills` installer.
The source is this fork's reviewed default branch, `main`.

<canonical-block name="skills-sh-whole-set">

```bash
npx skills add Ghroth6/matt_skills -g
```

Select all skills and choose the agents you use. All includes the experimental
and optional buckets. Same-name skills in the same scope are replaced and
their recorded source becomes this fork; no preliminary uninstall is needed.

</canonical-block>

## Update installed copies

<canonical-block name="skills-sh-update">

```bash
npx skills update -g
```

</canonical-block>

This updates all global skills from their recorded sources. Re-run the install
command to refresh only this fork's selected skills or change agents. Each
computer has its own installed copies. This operation does not sync Matt's
upstream changes into the fork; see [PERSONALIZATIONS.md](../PERSONALIZATIONS.md#maintenance-policy).

## One skill

<canonical-block name="skills-sh-one-skill">

```bash
npx skills add Ghroth6/matt_skills --skill <name> -g
```

```bash
npx skills update <name> -g
```

</canonical-block>

Remove an old installed name after a rename or retirement:

```bash
npx skills remove <name> -g
```

## Distribution boundaries

Use the README as this fork's installation entry. The `docs/` pages retain
upstream's rendering format; their install widgets on `aihero.dev` describe
upstream. See [writing-docs.md](./writing-docs.md).

The official `mattpocock-skills` Claude plugin installs upstream. Keep one
installation route per agent. The inherited plugin manifests and package
version remain upstream metadata; this fork's user workflow uses `skills`.
