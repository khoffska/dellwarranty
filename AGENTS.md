# AGENTS.md — dellwarranty

Context for AI coding agents (Claude Code, Codex, opencode, Cursor, …) working in this repo.
Read this first; keep it current.

## What this is
A tiny, parked PowerShell helper that looks up Dell warranty status by service tag.
Last touched 2019-08-01; not part of any active pipeline. Only change it if explicitly asked —
otherwise treat it as a legacy artifact.

## Layout
- `ps.psm1` — the whole tool. Saved with a module extension but it is top-level script code
  (no exported functions): it just runs on import.
- `README.md` — one-paragraph usage note.

## Commands
No build, test, or lint tooling in-repo (and no CI).
To use it: create `serials1.txt` (one service tag per line), `Import-Module ./ps.psm1`, then
enter the file path at the prompt.

## Conventions
- Default branch is `master`. Feature branch → PR; never push directly to `master`.
- Add tests/CI only if the script is ever revived; don't invent tooling now.

## Gotchas
- Windows-only and dead on modern Windows: it drives Internet Explorer via
  `New-Object -ComObject InternetExplorer.Application` (IE11 COM). Port to a headless
  `Invoke-WebRequest`/API call before reusing.
- Only the first 20 tags are read (`Get-Content -TotalCount 20`) — larger serial files are
  silently truncated.
- Opens a visible IE window per tag and `sleep 5` between each; it is not a batch/headless tool.
