Codex CLI (Node 20+)

Usage
- Install Node 20+.
- From repo root, run: `node tools/codex-cli/bin/codex.js --help`
- Optionally add to PATH by `npm link` inside `tools/codex-cli` (not required).

Architecture
- See `vessel_narrative_system_final/docs/SYSTEM_DIAGRAM_API_REFERENCE.md` for a Mermaid diagram and command mapping across modules (Garden/Echo/Limnus/Kira) and the Echo‑Community‑Toolkit stego bridge.

Commands
- Echo
  - `codex echo mode <squirrel|fox|paradox|mix>`
  - `codex echo status`
  - `codex echo say <message>`
  - `codex echo calibrate`

- Garden
  - `codex garden start`
  - `codex garden next`
  - `codex garden ledger`
  - `codex garden log`

- Limnus (LSB via Echo-Community-Toolkit)
  - `codex limnus init`
  - `codex limnus state`
  - `codex limnus update <alpha=..|beta+=..|gamma-=..|decay=N|consolidate=N|cache="text">`
  - `codex limnus cache "text" [-l L1|L2|L3]`
  - `codex limnus recall <keyword> [-l L1|L2|L3] [--since ISO] [--until ISO]`
  - `codex limnus memories [--layer L1|L2|L3] [--since ISO] [--until ISO] [--limit N] [--json]`
  - `codex limnus export-memories [-o file] [--layer L1|L2|L3] [--since ISO] [--until ISO]`
  - `codex limnus import-memories -i file [--replace]`
  - `codex limnus export-ledger [-o file]`
  - `codex limnus import-ledger -i file [--replace] [--rehash]`
  - `codex limnus rehash-ledger [--dry-run] [--file path] [-o out.json]`
    - Reindexes, relinks prev_hash, recomputes hashes for payload blocks.
    - With `--dry-run` (or `-n`) prints proposed changes without saving.
    - Provide `--file`/`-f` to rehash an alternate ledger JSON.
    - With `-o`/`--output` in dry-run, writes the normalized ledger JSON to the given path without altering the source.
  - `codex limnus commit-block '<json-or-text>'`
  - `codex limnus view-ledger [--file path]`
  - `codex limnus encode-ledger [-i <ledger.json>] [--file path] -c <cover.png> -o <out.png> [--size 512]`
  - `codex limnus decode-ledger [-i <image.png>] [--file path]`
  - `codex limnus verify-ledger [-i <image.png>] [--file path]`

- Kira
  - `codex kira validate`
  - `codex kira sync`

State & Integration
- State is written to `vessel_narrative_system_final/state/` to interoperate with the Python CLI.
- LSB encode/decode uses the Python toolkit by spawning `python3` and importing from `Echo-Community-Toolkit/src`.
