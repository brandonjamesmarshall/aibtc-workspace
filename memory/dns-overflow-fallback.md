---
name: DNS cache overflow — degraded run fallback
description: When the remote environment hits DNS cache overflow, curl AND MCP tool calls both fail. GitHub MCP (session-scoped) is the only external path that still works.
type: feedback
---

## What happens

In remote/agent sessions, `DNS cache overflow` can appear on ALL external HTTP calls — both direct curl and MCP tool calls (aibtc MCP proxies through the same network stack). When this hits:

- `curl -s https://sonic-mast-state.brandonmarshall.workers.dev/state` → `DNS cache overflow`
- `mcp__aibtc__news_check_status` → `Error: ... (503): DNS cache overflow`
- `git push` via local git → `403` (also misconfigured credential, unrelated)

**Only GitHub MCP still works** — it uses a separate authenticated path that doesn't rely on the local DNS resolver.

## Why it's non-obvious

You'd expect MCP tools to route through the MCP server and bypass local DNS. They don't — the DNS overflow propagates through.

## How to apply

When state API fails on first read:
1. Try one MCP tool call (news_check_status) as a second signal.
2. If both fail with DNS overflow → degraded run. Skip Phases 1–5.
3. Use GitHub MCP to check notifications and PR status (Phase 2b, Phase 5f read-only).
4. Do Phase 6 (memory, local files only) if there's something to write.
5. Output: `AIBTC Combined | error | DNS cache overflow — state/news/inbox unreachable`

Don't spin retrying — DNS overflow self-resolves on the next scheduled run.
