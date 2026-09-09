---
name: connect
description: Connect this Claude user to one deployment-scoped Mayland MCP release.
---

# Connect

Connect Claude Desktop or Claude Code to Mayland through the attested remote MCP release.

- Start from Mayland's `Connect Agent` action with Claude selected. It prepares a short-lived private connect intent and a fresh hash-verified setup command.
- ALWAYS run that complete command unchanged, even when MCP already reports Connected. It refreshes the marketplace and plugin, verifies the exact installed version, package contents and deployment, saves Mayland's automatic-update preference, and only then starts OAuth. The explicit update does not depend on host-wide background-update settings; leave those settings unchanged.
- Before running setup, say that you are checking and updating the connection. Do not promise a browser tab before verification has succeeded.
- A bare MCP reconnect or CLI version report does not verify a plugin update. Do not substitute separate update/login commands, skip verification, or execute an older installed helper first. If no fresh setup command is available, direct the user to Connect Agent in Mayland.
- If any setup step fails, stop and report its error. For a version or content mismatch, request a fresh Connect Agent command; do not bypass verification or downgrade/reinstall blindly.
- Inspect the exact plugin-scoped server with `claude mcp get plugin:mayland:<deployment-server-name>`.
- The verified setup command invokes `claude mcp login --no-browser` through the packaged `python3` PTY launcher at `bin/mayland-oauth-login`. Keep that command and its callback listener alive; do not launch a second login. The launcher uses `pty.fork` and works when the parent agent shell is a socket rather than a terminal.
- Keep the launcher's `TIOCSWINSZ`/`COLUMNS` width override so Claude does not hard-wrap the OAuth URL. Do not replace the launcher with `script`, and do not redirect, pipe, or place the login process in command substitution: those forms can close the PTY or callback listener in a socket-backed session.
- The launcher requests opening the emitted OAuth URL with `open` on macOS or `xdg-open`/`wslview` on Linux or WSL. If opening fails, no tab appears, or the wrong browser opens, give the user the printed Mayland `/api/oauth/authorize` URL to open in the browser already signed in to Mayland. Keep the setup command running and do not start a second login; that browser redirects the private connect intent back to the waiting localhost callback.
- After the browser returns, verify that the exact plugin-scoped server is connected.
- Keep user-facing output minimal: no command output or technical narration while steps succeed, detail only for the failing step. Confirm the connection only after setup succeeds. Then require `/reload-plugins` or a new Claude Code session before Mayland work: the installed plugin version is verified, but the current conversation may still have the old version loaded.
- If Python 3 is unavailable, the pseudo-terminal cannot start, or the intent expired, report the exact failure and direct the user back to Connect Agent for a fresh handoff. Do not switch to an unqualified server name.
- Never print, request, or explain setup credentials. Mayland does not require a code to be pasted into the browser.
- `/reset` clears conversation context and requests a fresh Mayland brand context pack; it does not update or reload the plugin.
