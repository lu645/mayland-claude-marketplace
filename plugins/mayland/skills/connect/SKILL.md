---
name: connect
description: Connect this Claude user to one deployment-scoped Mayland MCP release.
---

# Connect

Connect Claude Desktop or Claude Code to Mayland through the attested remote MCP release.

- Start from Mayland's `Connect Claude Code` action. It prepares a short-lived private connect intent before opening the Desktop Code workspace.
- Add or update the credential-free Mayland marketplace repository at user scope, then install or update `mayland`.
- Inspect the exact plugin-scoped server with `claude mcp get plugin:mayland:<deployment-server-name>`.
- Run `claude mcp login --no-browser` in a pseudo-terminal and keep its callback listener alive. On macOS use `script -q /dev/null claude mcp login --no-browser 'plugin:mayland:<deployment-server-name>'`; on Linux or WSL use `script -q -e -c "claude mcp login --no-browser 'plugin:mayland:<deployment-server-name>'" /dev/null`.
- Capture the emitted Mayland `/api/oauth/authorize` URL and open it immediately with `open` on macOS or `xdg-open`/`wslview` on Linux or WSL. The setup session opens the emitted OAuth URL; the signed-in Mayland browser redirects the private connect intent back to the waiting localhost callback.
- After the browser returns, verify that the exact plugin-scoped server is connected.
- If the pseudo-terminal launcher is unavailable or the intent expired, report the exact failure and direct the user back to Connect Claude Code for a fresh handoff. Do not switch to an unqualified server name.
- Never print, request, or explain setup credentials. Mayland does not require a code to be pasted into the browser.
- Use the exact `claude mcp add --transport http --scope user <name> <url>` command only as a support-provided fallback.
- `/reset` first invokes `/clear`, then requests a fresh Mayland brand context pack.
