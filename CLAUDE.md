# codex-plugin-cc

Personal fork of `openai/codex-plugin-cc`. The `codex` plugin comes from upstream;
the `claudian` plugin (Obsidian integration) is local to this fork and contains
personal paths and folder names.

## Never open a pull request against the upstream repository

PRs go to `tanakauo/codex-plugin-cc` only. A branch from this fork once ended up
as `openai/codex-plugin-cc#607`, proposing the personal vault layout to a public
OpenAI repository; it had to be closed by hand. When creating a PR, check that
its base is this fork.

## Version metadata

`npm run check-version` validates only `package.json`, `package-lock.json`, and
the **codex** plugin's manifests — it does not look at `claudian`. The claudian
version is maintained by hand and must match in both places:

- `plugins/claudian/.claude-plugin/plugin.json`
- `.claude-plugin/marketplace.json` (the `claudian` entry)
