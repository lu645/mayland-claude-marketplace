---
name: reset
description: Clear local Claude context and load a fresh Mayland Brand Context Pack.
---

# Reset

Reset the local working context before continuing Mayland production work.

1. Invoke `/clear` to discard stale local conversation context. This does not update or reload the plugin; after an update, use `/reload-plugins` or a new Claude Code session first.
2. Call `get_brand_context` for the active Brand.
3. Use the returned `contextPackId` and `contextPackHash` on every subsequent mutation.
4. If the connection prevents loading a fresh Brand Context Pack, stop and use Mayland's `Connect Agent` action with Claude selected. Run its fresh hash-verified setup command unchanged, as described in `/mayland:connect`. A bare MCP reconnect is not a verified plugin update. Do not bypass a failed setup check.
