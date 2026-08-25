---
name: connect
description: Connect this Claude user to one deployment-scoped Mayland MCP release.
---

# Connect

Connect Claude Desktop or Claude Code to Mayland through the attested remote MCP release.

- Start from Mayland's `Connect Claude Code` action. It prepares a short-lived private connect intent before opening the Desktop Code workspace.
- ALWAYS update first, even when the MCP server already reports Connected: run `claude plugin marketplace update mayland` and `claude plugin update mayland@mayland --scope user` before anything else (add the marketplace at user scope first if it is missing). Report the installed plugin version before and after; when it changed, tell the user to start a new conversation so the update loads.
- Only after the update check: verify the connection, and skip the OAuth steps below when the plugin-scoped server is already Connected.
- Inspect the exact plugin-scoped server with `claude mcp get plugin:mayland:<deployment-server-name>`.
- Run `claude mcp login --no-browser` through the packaged `python3` PTY launcher at `bin/mayland-oauth-login`, using the exact command supplied by the Mayland setup prompt, and keep its callback listener alive. The launcher uses `pty.fork` and works when the parent agent shell is a socket rather than a terminal.
- Keep the launcher's `TIOCSWINSZ`/`COLUMNS` width override so Claude does not hard-wrap the OAuth URL. Do not replace the launcher with `script`, and do not redirect, pipe, or place the login process in command substitution: those forms can close the PTY or callback listener in a socket-backed session.
- Capture the emitted Mayland `/api/oauth/authorize` URL and open it immediately with `open` on macOS or `xdg-open`/`wslview` on Linux or WSL. The setup session opens the emitted OAuth URL; the signed-in Mayland browser redirects the private connect intent back to the waiting localhost callback.
- After the browser returns, verify that the exact plugin-scoped server is connected.
- Keep user-facing output minimal: no command output or technical narration while steps succeed, detail only for the failing step. Close with exactly two short sentences: Claude is connected to Mayland, and the user should start a new conversation because the Mayland tools only load there.
- If Python 3 is unavailable, the pseudo-terminal cannot start, or the intent expired, report the exact failure and direct the user back to Connect Claude Code for a fresh handoff. Do not switch to an unqualified server name.
- Never print, request, or explain setup credentials. Mayland does not require a code to be pasted into the browser.
- Use the exact `claude mcp add --transport http --scope user <name> <url>` command only as a support-provided fallback.
- `/reset` first invokes `/clear`, then requests a fresh Mayland brand context pack.
