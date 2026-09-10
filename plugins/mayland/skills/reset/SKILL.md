---
name: reset
description: Recover Mayland production context while preserving the existing assignment and WIP.
---

# Reset

Recover the existing assignment; a reconnect or context refresh is not a new commission.
Reload the current creative workflow and capabilities; local host memory cannot override them.
Preserve recovery identities, not old layout recipes or unsupported approval claims. Revalidate
any generated-email inspiration through get_approved_email_reference for its exact version;
only customer-approved versions qualify. The current WIP remains available for authorized edits.

1. Before clearing local context, retain an accessible handoff with the saved prompt identity and
   exact version, assignment, Brand and email IDs, current run and pack binding, WIP revision,
   reference selection receipt/ordered sources, job IDs, unresolved findings and uncertain request
   keys. Mayland's saved prompt, WIP, assets and receipts remain authoritative; do not create a
   separate local document or node database. If the handoff cannot survive `/clear`, do not clear
   until these identities can be recovered. Clearing is optional, not a recovery prerequisite.
2. Read `get_email_wip` for the existing email and resolve the retained prompt version. Preserve
   manual changes and use the returned revision, active run, lock and fencing state. Never guess
   an ID or overwrite a newer document with the pre-interruption copy.
3. Call `get_brand_context` for a fresh pack of the same Brand. Do not attach that new binding to
   ordinary edits or completion of a run tied to a different pack. If the existing owned run's
   pack is stale, use `pause_agent_run` with the fresh same-Brand pack and the current run ID,
   fencing token, expected WIP revision and reason. This recovery exception permits pausing;
   it does not permit edits with mixed run/pack bindings. Resolve any uncertain write with its
   original key and payload before changing the recovery sequence.
4. Once the old run is paused and no other active owner prevents continuation, call
   `create_bulk_agent_run_group` with the fresh pack, a stable idempotency key and `emails`
   containing the existing email ID and brief. Use the returned child run and fencing token;
   keep the existing WIP, assets and saved prompt line. Rebind the intended ordered references
   with `select_run_references` and retain the new receipt before design changes. Preserve USER
   selections. If the owned active run remains valid, continue it with its matching binding
   instead of creating another run. Never interrupt another owner's healthy run or bypass a
   takeover confirmation; follow the returned recovery guidance when normal acquisition fails.
5. Re-read relevant Brand facts and verify outstanding assets/jobs and the changed document
   region before continuing. Completion still requires compiling and visually inspecting the
   exact current WIP. Do not repeat image jobs, create another email or mint a prompt Version 1
   merely because the conversation resumed.
6. A context reset does not update the plugin. After an update use `/reload-plugins` or a new
   Claude Code session. If connection fails, use Mayland's `Connect Agent` action with Claude
   selected and its fresh hash-verified setup command as described in `/mayland:connect`.
   A bare MCP reconnect is not a verified plugin update. Do not bypass a failed setup check.
   Other MCP clients use Connect Agent for their own client and reload the current workflow;
   they must not install or run Claude CLI. A reported mismatch triggers this update path;
   matching versions do not. Use the current client, not a Claude-specific fallback.
