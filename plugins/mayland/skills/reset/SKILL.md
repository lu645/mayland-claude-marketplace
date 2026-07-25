---
name: reset
description: Clear local Claude context and load a fresh Mayland Brand Context Pack.
---

# Reset

Reset the local working context before continuing Mayland production work.

1. Invoke `/clear` to discard stale local conversation context.
2. Call `get_brand_context` for the active Brand.
3. Use the returned `contextPackId` and `contextPackHash` on every subsequent mutation.
4. Stop and reconnect through `/mcp` if a fresh Brand Context Pack cannot be loaded.
