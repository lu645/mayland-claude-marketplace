---
name: email-production
description: Produce and revise brand-safe Mayland emails through the connected release.
---

# Email Production

Use this plugin to create, iterate, and complete one Mayland email run at a time.

- Always start from a fresh brand context pack before mutating production content.
- Never assume stale local context is still valid after an interruption.
- Use `/reset` when you switch emails, after a reconnect, or when Mayland reports stale context.
- `complete_agent_run` is the only Claude path that can create a final Email Version.
