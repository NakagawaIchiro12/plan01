# CLAUDE.md

Guidance for AI assistants (Claude Code and similar tools) working in this repository.

## Current State

This repository is **newly initialized and empty** — no source code, no commits, no
build tooling exists yet. As code is added, this file should be updated to describe
the codebase structure, workflows, and conventions. Treat the sections below as a
scaffold rather than a description of existing code.

- **Repo**: `NakagawaIchiro12/plan01`
- **Default remote**: `origin`
- **Active development branch (this task)**: `claude/add-claude-documentation-JN88I`

## Repository Layout

Not yet established. When code is added, document the top-level layout here, e.g.:

```
/            project root
├── src/     application source
├── tests/   automated tests
└── ...
```

## Development Workflow

No build, test, or lint tooling is configured yet. Once it exists, record the
canonical commands here so assistants can run them without guessing — for example:

- Install dependencies: _TBD_
- Run the app locally: _TBD_
- Run tests: _TBD_
- Lint / format: _TBD_
- Type-check: _TBD_

Until those are defined, ask the user before introducing a build system, package
manager, or framework — those are project-shaping decisions that should not be
made unilaterally.

## Git & Branching

- All work for the current task goes on `claude/add-claude-documentation-JN88I`.
  Do **not** push to other branches without explicit permission.
- Push with `git push -u origin <branch-name>`.
- Prefer new commits over amending. Never use `--no-verify` or skip hooks.
- Do not create pull requests unless the user explicitly asks.

## GitHub Integration

- This environment exposes GitHub tools via the `mcp__github__*` MCP server.
  The `gh` CLI is **not** available — use the MCP tools instead.
- Tool access is scoped to `NakagawaIchiro12/plan01`. Do not target other repos.
- Be frugal with PR/issue comments — only post when genuinely necessary.

## Conventions (to be filled in)

Add language-, framework-, and team-specific conventions here as they are decided:

- Code style / formatter
- Naming conventions
- Commit message style
- Test layout and naming
- Error handling patterns
- Logging / observability
- Security-sensitive areas

## Notes for Assistants

- Prefer editing existing files over creating new ones.
- Don't add speculative abstractions, unused options, or comments that just
  restate what the code does.
- For UI/frontend work, verify behavior in a browser before reporting completion.
- When this file goes out of date relative to the code, update it.
