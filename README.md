# agent-codebase-explorer

A read-only codebase-search subagent for Claude Code, Codex, and OpenCode. Hand it a search brief; it returns a capped report of where things live.

## What it does

Given a self-contained brief ("where is X", "what references Y", "how is Z wired"), it greps and globs the tree, follows the trail through definitions and call sites, and returns a tight report: what it found (with `path:line`), what it ruled out, and any open questions. It never edits, runs builds, or makes decisions.

It carries only Read, Grep, Glob, and Bash (no MCP/connector tools). That least-privilege tool set is deliberate: an agent that advertises no connector schema cannot be taken down by a malformed one, so it stays spawnable when broader agents do not.

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
