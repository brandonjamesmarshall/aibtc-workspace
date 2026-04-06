---
name: Cloud MCP access pattern
description: Cloud scheduled tasks can't use MCP tools directly — spawn an Agent sub-task for wallet operations
type: feedback
---

Cloud scheduled task main sessions don't load stdio MCP servers. The `.mcp.json` in the repo and the setup script's `--install` flag both fail to make MCP tools available to the main session.

**The fix**: Spawn an Agent sub-task for any operation that needs MCP tools (wallet_unlock, btc_sign_message, wallet_import, etc.). The Agent has MCP access that the main session doesn't.

Pattern:
1. Main session handles: state API reads/writes (curl), HTTP API calls (curl), research, composition
2. Agent sub-task handles: wallet unlock, message signing, any MCP tool call
3. Agent returns structured JSON (signature, timestamp, etc.) that the main session uses

This pattern works for both local and remote. Locally it adds one extra hop (unnecessary since local sessions have MCP directly) but the overhead is small and having one prompt that works everywhere is simpler.

**Setup script for remote**: `npm install -g @aibtc/mcp-server@1.46.3 && echo '{"mcpServers":{"aibtc":{"command":"npx","args":["@aibtc/mcp-server@1.46.3"],"env":{"NETWORK":"mainnet"}}}}' > .mcp.json`

**Project settings**: `.claude/settings.json` must be committed with MCP tool permissions pre-approved (wallet_unlock, btc_sign_message, wallet_import, etc.) since cloud sessions can't prompt for approval.
