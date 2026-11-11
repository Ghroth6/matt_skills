# Contributing

This fork tracks [mattpocock/skills](https://github.com/mattpocock/skills) and carries small local fixes. The maintainer's request or a linked issue defines the work.

## Maintenance

- Merge upstream history, then preserve or reapply the agreed fork patches. Keep a merge commit when integrating upstream so future syncs retain the common ancestry.
- Make each local fix on a branch and submit it through a pull request. Keep changes limited to the request, with checks appropriate to the affected files.
- Keep fork installation commands and repository metadata pointed at `Ghroth6/matt_skills`. Preserve upstream attribution, historical links, and reusable Skill behavior unless the requested fix changes them.
- GitHub issue forms, automatic triage, stale-issue closure, and release automation are not used here. When syncing upstream, keep these workflows and forms absent rather than reintroducing them.
- `SCOPE.md` and `.out-of-scope/` retain upstream policy as reference; they do not replace the maintainer's decisions for this fork.
- Repository maintenance does not update installed Skill copies. Installation and device migration are separate tasks.

## Local checks

Run `git diff --check` and `node scripts/sync-plugin-version.mjs --check`. After changing a plugin manifest, also run `claude plugin validate . --strict`. Validate changed scripts and Skill behavior as appropriate to the patch.

## Versions

Routine upstream syncs and local fixes use Git commits and pull requests as their record; they do not require a changeset, release PR, or tag. Existing Changesets files and tooling remain as merge/reference material, not a required fork workflow.

Keep `package.json` and `.claude-plugin/plugin.json` at the same version. A separate distribution task can decide whether to bump the version; if needed, edit the package version and run `node scripts/sync-plugin-version.mjs` before checking and committing both files.
