# claudian

Saves notes into the Obsidian vault `田中雄一郎OS保管庫`. The rules below exist
because of how that vault is actually stored — the code alone does not explain
them.

## Auto-detection looks at exactly one location

`~/田中雄一郎OS保管庫`, and nowhere else. **Do not add fallback candidates.**
Copies and backups carrying the same name exist on disk (`TANAKA-BRAIN/`,
`_旧Vaultバックアップ/`, duplicates restored from the Trash); every one of them
would match a broader search, and the wrong one winning is silent — notes land
in a folder nobody reads. A vault elsewhere is named explicitly: `--vault`,
`CLAUDIAN_VAULT_ROOT`, or `vaultRoot` in `~/.claudian/config.json`.

## Fail loudly; never create the vault root implicitly

If the vault is missing, stop with an error. Creating the directory (or writing
into a lookalike) produces a successful-looking save that nobody can find later.
`--create-vault` is the only way to create it, and the skill must not pass it on
its own.

## The folder mapping is data, not code

Aliases resolve in layers: built-in defaults < `~/.claudian/config.json` <
`<vault>/.claudian.json`. The vault-local file wins so that a reorganisation
travels with the vault to every machine instead of being copied by hand. Do not
hardcode new folder names in the script — `--scan-folders --write` regenerates
the mapping from the vault's real structure, and `null` disables an alias whose
folder is gone.

## Contracts worth keeping

- Dates come from local time, not UTC: a note saved at 07:00 JST belongs to that
  day, not the previous one.
- A same-day note with the same title is never overwritten — it becomes `_2`,
  `_3`, and so on.
- stdout carries the saved filename and nothing else; the skill and the
  `/claudian:save` command parse it. Diagnostics go to stderr.
