# The canonical install block

Use these blocks for this fork's `README.md` and new installation instructions. Change them here first, then propagate. Retain the host-specific plugin routes and the editable-file route through npx.

## Installation sources and updates

Every install below reads `Ghroth6/matt_skills`. The marketplace name is `ghroth6`; the plugin name remains `mattpocock-skills`. The marketplace's relative `source: "./"` selects the plugin in this fork. Keep these identifiers consistent with `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`.

The Claude official marketplace distributes upstream, not this fork. Do not present `claude-plugins-official` as a fork installation route. Historical release notes and ADRs retain their original upstream context.

Lead with each host's plugin route where available, and retain npx for users who want editable files. Choose one route per agent to avoid loading duplicate skills. Listing an installation option does not select or migrate an existing local installation.

| Agent | Route | Updating |
| --- | --- | --- |
| Claude Code | `mattpocock-skills@ghroth6` | Enable marketplace auto-update once, or update manually |
| Codex | `mattpocock-skills@ghroth6` | Host-managed refresh; explicit marketplace refresh command below |
| Copilot CLI | `mattpocock-skills@ghroth6` | Opt into session-start updates in user settings, or update manually |
| VS Code | Install Plugin from Source | Automatic updates follow `extensions.autoUpdate`; manual update also available |
| Gemini CLI | `gemini skills install` | Re-run the two install commands |
| Other agents or editable files | npx / skills.sh | Run `update`; re-run `add` to pick up new skills |

The release workflow runs `npm run version` to synchronize `package.json` and the plugin version. Publish version changes through that workflow so hosts that cache by version can recognize releases. A source merge alone is not evidence that installed copies have updated.

Command forms and update controls were checked against the linked official documentation on 2026-11-11. Fork installation and automatic-update behavior have not been exercised on devices.

## Claude Code

<canonical-block name="claude-code">

```bash
claude plugin marketplace add Ghroth6/matt_skills
claude plugin install mattpocock-skills@ghroth6
```

For automatic updates, open `/plugin`, select **Marketplaces**, choose `ghroth6`, and enable auto-update. Custom marketplaces have auto-update off by default. To update manually, run `claude plugin update mattpocock-skills@ghroth6`.

The Claude official marketplace provides the upstream version, not this fork.

</canonical-block>

Source: [Claude Code plugin installation and updates](https://code.claude.com/docs/en/discover-plugins).

## Codex

<canonical-block name="codex">

```bash
codex plugin marketplace add Ghroth6/matt_skills
codex plugin add mattpocock-skills@ghroth6
```

To explicitly refresh this marketplace, run `codex plugin marketplace upgrade ghroth6`. Start a new session after installation or an update to use the refreshed skills.

</canonical-block>

Sources: [Codex plugin commands](https://learn.chatgpt.com/docs/developer-commands#codex-plugin) and [plugin packaging and marketplace refresh](https://developers.openai.com/plugins/build/plugins).

## GitHub Copilot CLI

<canonical-block name="copilot">

```bash
copilot plugin marketplace add Ghroth6/matt_skills
copilot plugin install mattpocock-skills@ghroth6
```

For automatic updates, merge this entry into `extraKnownMarketplaces` in your user settings, preserving other entries:

```json
{
  "extraKnownMarketplaces": {
    "ghroth6": { "source": { "source": "github", "repo": "Ghroth6/matt_skills" }, "autoUpdate": true }
  }
}
```

This opt-in applies to interactive and `-p` sessions. For a manual update, run `copilot plugin update mattpocock-skills`.

</canonical-block>

Source: [Copilot CLI plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference).

## VS Code

<canonical-block name="vscode">

Run **Chat: Install Plugin from Source** and enter `https://github.com/Ghroth6/matt_skills`.

Automatic plugin updates follow `extensions.autoUpdate`. To update manually, run **Chat: Update Plugins**.

</canonical-block>

Source: [VS Code agent plugins](https://code.visualstudio.com/docs/agent-customization/agent-plugins).

## Gemini CLI

<canonical-block name="gemini">

```bash
gemini skills install https://github.com/Ghroth6/matt_skills.git --path skills/engineering
gemini skills install https://github.com/Ghroth6/matt_skills.git --path skills/productivity
```

Re-run both commands to update. These paths select the two promoted skill buckets.

</canonical-block>

Source: [Gemini CLI skill commands](https://geminicli.com/docs/cli/skills/#from-the-terminal).

## Other agents, or editable files (npx / skills.sh)

<canonical-block name="other-agents">

```bash
npx skills@latest add Ghroth6/matt_skills
```

Pick the skills and agents you want, including `setup-matt-pocock-skills`. To preselect an agent, append `-a <agent>`.

To install globally for Codex without choosing an agent interactively:

```bash
npx skills@latest add Ghroth6/matt_skills --global --agent codex
```

For only the 27 published skills, select the **Mattpocock Skills** group and leave **Other** unselected. The published set is listed in [`.claude-plugin/plugin.json`](https://github.com/Ghroth6/matt_skills/blob/main/.claude-plugin/plugin.json).

This route installs editable files and works with Claude Code too. To update, run `npx skills@latest update`; re-run `add` to pick up newly added skills.

</canonical-block>

Installation does not require cloning this repository first. The Codex-specific npx command is an optional shortcut; keep the general command available.

## Single-skill instructions

Use this form wherever one skill is named on its own. Pages under `docs/` carry no install commands because ai-hero renders the install widget; see [writing-docs.md](./writing-docs.md).

<canonical-block name="skills-sh-one-skill">

```bash
npx skills@latest add Ghroth6/matt_skills --skill=<name>
```

```bash
npx skills@latest update <name>
```

</canonical-block>

Use `skills@latest` in new installation commands.
