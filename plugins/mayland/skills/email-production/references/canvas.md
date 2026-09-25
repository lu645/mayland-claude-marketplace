# Mayledit mechanics

Consult the relevant section only when the current tool schema/capability examples do not answer
an operation or recovery question. The creative entrypoint covers ordinary production.
These are technical boundaries, not design recipes.

## Campaign identity and run setup

Reuse an explicit, validated campaign selection from the user's request or briefing handoff without
asking again. For an explicitly supplied new name, check existing boards and, if absent, call
`create_campaign` with that name without another naming question. Ask which board only when that
decision is missing or genuinely ambiguous. Never guess the board or silently choose Unassigned.
A campaign board holds emails; a campaign goal does not.

Verify returned Brand ID, name and official site before writes; a display name or URL slug is not
a Brand ID. Get a fresh `get_brand_context` pack, relevant product contexts and
`list_approved_learnings`. On CONTEXT_PACK_RUN_MISMATCH read WIP and use its actual active run.
On stale context or interruption follow reset: an owned stale run must be paused before starting
a replacement against a new pack. Never use the new pack to edit or complete the old run.
For PLUGIN_UPDATE_RECOMMENDED follow connect and reload; a bare MCP reconnect is not an update.

`create_email` requires the chosen campaign, Brand, title and brief. Leave copyRevisionIds,
referenceEmailIds and campaignGoalId omitted unless explicitly supplying the pack's exact selection.
Read `get_email_wip` and reuse its non-null `activeAgentRunId`. With no active run, call
`create_bulk_agent_run_group` with the fresh `contextPackId`/contextPackHash, stable idempotencyKey
and emails containing this emailId/brief. The tool supports a single email and acquires its lock.
Retain that email's child run and fencingToken. Retry an uncertain start with the same payload and key.
Use current expectedWipRevision for writes and feed each returned newWipRevision into the next.
Heartbeat the owned lock while jobs run. Do not interrupt another owner's healthy run.

Copy returned IDs verbatim; current tool schemas govern operations, not host memory. On a reported version mismatch, use Connect Agent for the
current client and recovery's verified setup guidance. Claude reloads its plugin after setup;
other clients reload the workflow and must not install Claude CLI.

In the first free-node batch or new compose, disclose agentInput: original userPrompt, effective
productionInstruction, promptVersion, pluginVersion, model, provider, generationSettings,
documentInputs, jobIds and unavailableInputs. Include authorized sources actually used; exclude
unrelated or hidden host content. Use null for unavailable settings; never guess or silently
truncate. Update substantive changes and bind jobs for an existing email to its emailRun.

## Reference selection and access failures

Existing context references take priority; add Swipe File items (scope=WORKSPACE) found for the
email's purpose; when context.references is empty, workspaceInspiration is supplied automatically.
Use list_reference_emails scope=BRAND with the target brandId to browse further Brand references.
Use inspirationQuery on get_brand_context/get_product_context for a targeted search even with
existing references. Follow nextCursor when searching; the combined five-reference bound applies
to run selection, not the whole library. READY references with missing analysis remain viewable.
workspaceInspiration items are discovery, not visual inspection or a run selection; continue with
list_reference_emails scope=WORKSPACE (no Brand filter) and view candidates with get_reference_email.
An explicit user selection takes precedence over automatic alternatives when eligible.
Check processing state and actual image access: unavailable images cannot be visual inspiration.
Refresh expired signed URLs through get_reference_email; disclose unresolved access.
An unavailable explicit source needs the user's choice to wait or proceed without it.

Bind imported references with `select_run_references` before composing or editing the design,
using the actual active run, fresh context binding and ordered referenceEmailIds.
Set selectionSource=USER for explicit choices, otherwise AUTOMATIC; retain selectionReceipt,
selectionSource, scope, brandId, contentHash and snapshotAssetId. A server receipt records the
selected source, not whether the host actually displayed it. An uncertain call retries unchanged.
REFERENCE_USER_SELECTION_REQUIRED does not authorize an automatic substitute labelled USER.
Older historical receipts may be absent; report that gap, never invent one. A new selection
requires its receipt. Run selections never mutate or substitute the target Brand's identity pack.

For generated emails use `get_approved_email_reference` with exact emailId/versionId; retain
approval proof. A rejected version is excluded. Do not fall back to ordinary WIP/preview for
inspiration, and never insert a generated-email ID into imported referenceEmailIds.
A rationale describes decisions actually informed by viewed pixels, not a server-certified viewing receipt.

## Asset geometry and fidelity

Use `create_image_edit_job` with verified sourceAssetId. Set `editIntent` to `product-scene`
for a changed setting/pose, or background-removal for a cutout preserving geometry.
Omitting intent uses the legacy cutout comparison, which is unsuitable for a new scene.
`create_image_generation_job` has no source-image input: `productId` alone
does not send product pixels. Inspect real source and result for identity and creative quality;
the Analysis model describes Swipe File references, not product-scene quality.
An edit request attaches only the sourceAssetId image; naming other products does not supply their
appearance. A multi-product scene needs verified pixels for every product (for example a composite of
the originals), otherwise place separately verified assets; never invent products from names.

Supply assetName (descriptive, at least two words, 3–100 characters) and targetSize from the intended
placement's CSS width/height. Only supply `targetSize.backgroundColor` when you intentionally
want an opaque frame. For an unframed photo, omit it; inspect actual delivery ratio and crop.
Different output dimensions require deliberate fit/crop, not accidental transparent gutters.
Prompts state what must stay, quote any text to render and name adjacent edge colors.

For a cutout request background=transparent. Inspect actual alpha and its edges on the planned
ground; reject baked checkerboards, white boxes, halos and changed product details.
IMAGE_TRANSPARENCY_UNSUPPORTED means the provider cannot honor the request;
IMAGE_TRANSPARENCY_MISSING means the result lacks alpha. A PNG extension proves neither.
Preserve the source. Logo edits must preserve exact letters and mark geometry; a crop cannot
remove white within a letter or an opaque plate. Preserve intentional Brand plates.

Use `get_image_job` with waitMs=20000 for a bounded server-side wait. A queued/running result
after that budget is not a failed job. Continue useful work or check again; heartbeat the email
lock between waits. Do not use shell sleep commands or assume a host-specific Monitor tool.
For failed jobs read errorCode and errorMessage when provided. An unchanged invalid request
does not become valid through a new job ID. Respect a known provider rejection; do not repeatedly
rephrase requests to bypass it. Unknown HTTP errors remain unknown rather than a guessed cause.
For the provider error code insufficient_quota, explain a quota/billing issue and ask to check the actually connected
organization/project's billing and limits; the code does not prove a zero account balance.
For the provider error code rate_limit_exceeded, name the rate limit. For an unspecified OpenAI HTTP 429 say:
“OpenAI hat die Bildanfrage gerade abgelehnt. Die genaue Ursache ist aus der Fehlermeldung nicht
erkennbar. Bitte prüfe die Limits der verbundenen OpenAI-Verbindung oder wende dich an den Support.”
Never recommend topping up credit, invent a model restriction, switch models or create replacement
jobs without evidence; keep the job retry policy. Share safe job/connection/model identifiers for
support, never credentials.
Then use `get_completed_image_asset`: it returns the public url,
result image blocks, plus the source image for an edit. View them before placement. Use measured
`delivery` dimensions, not private preview dimensions; inspect the public image when unavailable.
Run image jobs through Mayland, never directly through a provider. Bind emailRun for an existing
email so unsuccessful attempts remain visible. IMAGE_EDIT_UNFAITHFUL reports a fidelity failure,
not a proven diagnosis of which detail changed.

A failed required scene remains missing. Do not silently remove its imageSlot, substitute a
packshot/logo, or call that downgraded draft finished. Correct an identified cause once with a new
key; uncertain transport retries the same payload/key. If repair fails or lacks a justified cause,
preserve useful WIP and report the gap; do not complete until the requirement is fulfilled.

## Fonts and identity fields

Read all `designDna.font_families` entries and their `usage`, including additional campaign and
accent families. Use the intended family per element with an email-safe fallback. Report unavailable font errors,
preserve WIP and repair the source before claiming the requested typography rendered.

Read `visualSummary`, `voiceSummary`, `tone`, `noGo`, `imageryStyle` and the target's verified
designTokens. Product truth/benefits remain sourced; furniture and mandatoryStatements retain their
required wording. Navigation labels are not a logo asset.

A named font is not a loaded face. Use trusted sources or inspect the official Brand site's
stylesheet for its actual font URL. Register faces with `upsert_custom_font` using their real
weight and safe fallback stack; do not split Base64 font bytes across chat messages.
The optional composer accepts plan.fonts.faces with name/data/weight and their respective verified
HTTPS font URLs. Confirm the face loads in the rendered preview. Do not label regular as every
weight, bypass source validation, or rewrite Brand typography to disguise a fallback.

## Node operations and semantic links

Get the relevant category from `get_mayledit_capabilities`; its strict definitions and examples
are the authority. Unknown fields fail. The following capability vocabulary is contract-tested:

elementKinds: text, button, image, icon, shape, table
shapeKinds: rect, rounded, circle, ellipse, triangle, diamond, pentagon, hexagon, polygon, star, line, arrow, freeform
operations: set_document_metadata, set_frame_state, update_frame, insert_node, update_node, group_nodes, ungroup_nodes, duplicate_nodes, move_nodes, align_nodes, distribute_nodes, upsert_reusable_block, instantiate_reusable_block, detach_reusable_block, upsert_text_style, bind_text_style, set_text_style_overrides, reset_text_style_overrides, detach_text_style, upsert_saved_style, apply_saved_style, upsert_custom_font, remove_node, create_export_region, rename_export_region, create_component, update_component, create_component_variant, instantiate_component, set_instance_variant, set_instance_property, set_instance_override, swap_instance, reset_instance_overrides, detach_instance, bind_variable, unbind_variable, create_variable, update_variable, remove_variable, move_node, reorder_nodes, set_auto_layout, remove_auto_layout
exporters: delivery_preview, compatible_html, png, pdf, svg, pen, klaviyo
recipes: linked_shape_text_cta

Use one 600px frame; grow height with update_frame. Fully off-frame elements are dropped.
set_frame_state controls root Lock/Eye; a hidden root cannot preview/export.
New CTA nodes use the `linked_shape_text_cta` recipe: Shape + Text with shared groupId and href.
Style them freely, including supported Drop Shadow; never create a legacy button node.
Move/resize the pair together; set_auto_layout takes the pair as one child (either member id).
A reusable CTA may be saved at Campaign, Brand, or Global scope.
opacity works on every kind; text newlines break lines, "• "/"1. " lines render as lists; table
elements carry data tables (fields via get_mayledit_capabilities).

Remove an optional link/effect with update_node, unsetProperties and an empty patch. Change a group URL on every member in one batch; on component
members use set_instance_override (an empty href clears only the link). Group, move or duplicate
complete groups and Auto Layout trees; unlock locked nodes first. Managed Auto Layout children need
layout operations and hold no overlap other than a linked CTA pair.

Inside text, `**` is bold and `==` uses accentColor.
Rotated text is baked into imagery. Translucent, stroked or freeform shapes behind copy bake too and
skip dark-mode rewriting. Bands and cards stay live: `set_auto_layout` background/gradient/radius, a
full-width rect/rounded Shape, or a solid card holding stacked copy and photos. For a one-sided
rounded seam, lay a rounded full-width sheet over the band's end, not a freeform path.
This does not prohibit cards over images or faded heroes: keep requested overlaps and layer order,
and if panel and live text separate on mobile, repair the composition rather than substituting a
gap. Match a fade's direction, color and extent from a source detail crop using supported
gradient/image operations; a hard shape over the image is not a matching fade.

## Optional shared libraries and export

Use list_mayledit_library with emailId for Campaign/Brand visibility or brandId for Brand.
Global means this workspace. Library saves use fresh context/idempotency; updates also require
id/expectedVersion. Use definitions from the capabilities' libraries category, not invented fields.
Global mutations require an admin. Defaults become persistent only after an explicit save.

Library entries and document instances are separate (upsert_reusable_block then
instantiate_reusable_block; upsert_text_style then bind_text_style); local overrides stay local.
Delete needs a confirmation challenge bound to the complete delete payload, item id/version and
action delete_mayledit_library_item, then the same payload with confirmationToken.
Do not bypass confirmation on retry; retain the idempotency key.

export_email_document takes exactly one stored revisionId or versionId. Named-region PNG/SVG
requires a permitted region format; inspect fidelity warnings and use downloadUrl before expiry.
compatible_html and recipient preview use the compiled delivery artifact. Klaviyo publication is
the operator's Publish action in Mayledit; never invent an account/template or publish intent.

## Canvas and delivery evidence

First view the stored document with `get_email_preview_image`, renderMode=canvas, including
detail crops. A text node's declared height does not prove its loaded font and wrapping fit: size
text boxes from the rendered bounds, or use Auto Layout where content should reflow. Delivery rows
can expand around text while canvas nodes still collide, so repair stored geometry and recheck both
surfaces; delivery alone does not resolve an editor defect.

Compile the current WIP with `compile_email_wip`; review all diagnostics using the warning repair
procedure below, not only blocking errors. Compile again after repairs.
`complete_agent_run` requires the exact current WIP's bound artifact with no blocking errors.
EMAIL_AGENT_DELIVERY_NOT_READY/BLOCKED mean production is incomplete, not bypassable warnings.

### Warning repair and Mayland Score

After every creation and user iteration, compile with `compile_email_wip` and review every entry in
`data.warnings` and `data.documentWarnings` (the warnings Mayledit shows), advisory ones included;
successful compilation alone does not complete this pass. Repair the actual document through the
returned element references, then compile and inspect the new revision. Compiler notes on normal
art flattening, geometry packing or hosted temporary images explain output; they are not defects.
Keep meaningful text at least 14px (body copy usually 16px) unless a readable exception is deliberate.

Fix meaningful defects within the assignment: unreadable text, weak contrast, inaccessible actions,
accidental repetition, wrong or missing alt text, broken destinations, missing content and avoidable
HTML size. Preserve Brand identity, verified offers, prices, products, link destinations,
personalization tokens, legal content, unsubscribe behavior and user-frozen copy; never strip
content or compatibility markup to improve a number. Make one deliberate repair pass, recheck, and
stop repeating an unsuccessful repair. Explain intentional or unfixable warnings; an unresolved
blocking error still prevents completion.

`data.maylandScore` is an explainable internal heuristic, not an inbox probability, deliverability
guarantee or performance prediction; a high score does not establish visual or Brand quality.
Report its returned points and reasons, never an invented, translated or stale score: after any
mutation, recompile and verify the score belongs to the final revision/artifact. Before an
iteration, ask only about a concrete material downside the user has not accepted. Requested A/B
alternatives are separate emails, each checked the same way.

### Original messages in Run details

Mayland cannot read host chats. On compose/apply, supply `agentInput.conversation` with a stable
id and the user's prompts verbatim (stable ids, chronological sequence, corrections included); never
substitute instructions, tool output or intermediate answers, and omit unavailable originals.
`complete_agent_run` takes the same conversation and an optional `finalAnswer`: only settled final
wording, presented unchanged.

For `get_email_preview_image`, use renderMode=delivery, compiled revisionId and
request both `viewportWidth` 600 and 390. Check revision/artifact identity against compile.
Canvas pixels are not proof of desktop or mobile delivery; repair a delivery failure rather
than changing renderMode. Inspect the opening and each section with `clip` containing x, y, width
and height in CSS pixels. Bound clips by contentHeight and that viewport's width; mobile
coordinates come from its 390px layout, not the 600px canvas. Detail pixels are returned directly,
including when no `imageUrl` exists. Do not invent URLs or local files for image blocks.
If pixels cannot actually be viewed, report the gap. Neither compile success nor an immutable
version is customer approval; preserve that distinction in every subsequent reference decision.
