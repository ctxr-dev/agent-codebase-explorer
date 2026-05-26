# agent-codebase-explorer

A read-only codebase-search subagent for Claude Code, Codex, and OpenCode. Hand it a search brief; it returns a capped report of where things live.

## What it does

Given a self-contained brief ("where is X", "what references Y", "how is Z wired"), it greps and globs the tree, follows the trail through definitions and call sites, and returns a tight report: what it found (with `path:line`), what it ruled out, and any open questions. It never edits, runs builds, or makes decisions.

Its instructions are tool-agnostic: it uses whatever capabilities the environment exposes (the built-in file, search, and shell tools, plus any servers the project provides) and treats them as best-effort. If a capability is missing, unhealthy, or errors, it notes that and falls back rather than halting, so it works across very different setups and never stalls a fan-out because one tool is down. It stays read-only by rule, even where write-capable tools are present.

## When to use it

During the exploration phase of planning, or whenever the main agent needs to locate code without spending its own context on the search. Run two or three in parallel with disjoint scopes for fast, broad fan-out, then fold each report into the plan.

## Install

```bash
npx @ctxr/kit install @ctxr/agent-codebase-explorer
```

`@ctxr/kit` installs the bundle and mirrors it into the host's agent directory; the agent then appears as `agent-codebase-explorer`.

## Releasing

Releases are PR-gated and the publish step is a manual dispatch; the CI workflows (`ci`, `release`, `tag-on-main`, `publish`) carry the details.

## License

MIT
