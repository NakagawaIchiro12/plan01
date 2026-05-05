# CLAUDE.md

Guidance for AI assistants (Claude Code and similar tools) working in this repository.

## What this project is

A small **single-page web app** for a shop owner to manage part-time staff
(パート) schedules on his phone. The owner receives schedules and time-off
requests from staff via LINE (text or images) and wants to see "who is
coming on which day" at a glance.

Goal: minimum viable, runs on a phone with no server.

## Repository Layout

```
/
├── index.html   the entire app (HTML + CSS + vanilla JS in one file)
├── CLAUDE.md
└── ...
```

There is no build step, no package manager, no framework, no dependencies.
Keep it that way unless explicitly asked otherwise — the whole point is
"open in mobile Safari/Chrome and it just works".

## How to run / try it

- Open `index.html` directly in a browser (file:// works) or serve the
  directory: `python3 -m http.server 8000`, then visit
  `http://<host>:8000/` on the phone.
- Data is persisted to `localStorage` under key `part-calendar-v1`.
- For app-like use on iOS/Android: open the page and choose
  "Add to Home Screen".

## App architecture

All state lives in a single `state` object:

```js
state = {
  staff: [{ id, name }],
  days:  { "YYYY-MM-DD": { working: [staffId], off: [staffId], memo: string } }
}
```

Persisted via `localStorage` (`STORAGE_KEY = "part-calendar-v1"`). The UI
re-renders fully from `state` on every change (`render()` rebuilds the
calendar grid). Modals are simple `display:flex` toggles.

Key functions in `index.html`:

- `render()` – rebuilds the month grid from `state`.
- `openDayModal(k)` – per-day editor: per-staff segmented control
  (―/出/休) + free-text memo (used for ad-hoc requests like
  "たきたさんはこの日休み").
- `parsePasteText(text, year, month)` – best-effort parser for LINE
  text. Recognizes `M/D`, `M月D日`, `D日`, ranges (`-`, `〜`), comma-
  separated bare day numbers, and the keywords `休` / `出勤`. Defaults
  to the kind selected in the paste modal. Names are matched as
  substrings of registered staff (longest-first to avoid overlap).
- Backup/restore is plain JSON copy-paste — no server, no file I/O API.

## Conventions

- **Vanilla everything.** No frameworks, no bundler, no npm. If you
  reach for one, stop and ask first.
- **Single file.** Keep HTML, CSS, and JS in `index.html` until it
  becomes painful. Don't pre-split.
- **Mobile first.** All UI must work with touch on a phone screen.
  Buttons need ≥36px height; modals slide up from the bottom; the
  viewport meta tag disables zoom intentionally.
- **Japanese UI.** All user-visible text is Japanese.
- **No external network calls.** App must work offline.
- **Don't over-engineer the parser.** It's intentionally a best-effort
  helper; the per-day editor is the source of truth. When parsing
  fails, surface the unparsed lines so the user can fix manually.
- **Backwards-compatible storage.** If you change the `state` shape,
  bump `STORAGE_KEY` (e.g. `part-calendar-v2`) and migrate, or you'll
  silently corrupt user data on reload.

## Verifying changes

There is no test suite. For any change:

1. Open `index.html` in a desktop browser, exercise the change.
2. Resize the window to a phone width (≤ 400px) and re-check layout.
3. Verify `localStorage` still loads after reload.
4. If the change touches `parsePasteText`, paste a few representative
   LINE-style strings and confirm the parse result.

## Git & Branching

- Active development branch: `claude/add-claude-documentation-JN88I`.
- Push: `git push -u origin <branch>`. Never push to other branches
  without explicit permission.
- Prefer new commits over `--amend`. Never use `--no-verify`.
- Do **not** open pull requests unless the user asks.

## GitHub Integration

- Use the `mcp__github__*` MCP tools — `gh` CLI is not available.
- Tool access is scoped to `NakagawaIchiro12/plan01`.
- Be frugal with PR/issue comments.

## Likely next steps (not yet built)

These were discussed but deferred — implement only when asked:

- Image OCR for handwritten shift photos.
- LINE Bot integration for auto-ingestion.
- Multi-device sync (currently device-local only).
- Per-staff colors in the calendar.
