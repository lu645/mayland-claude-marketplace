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

## Reference selection and access failures

Browse scope=BRAND and scope=WORKSPACE separately. Follow nextCursor when searching; the combined
three-reference bound applies to run selection, not the whole library. Missing Brand inspiration
does not justify skipping workspace. READY references with missing analysis remain viewable.
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

Supply assetName (descriptive, at least two words, 3–100 characters) and targetSize from the intended
placement's CSS width/height. Only supply `targetSize.backgroundColor` when you intentionally
want an opaque frame. For an unframed photo, omit it; inspect actual delivery ratio and crop.
Different output dimensions require deliberate fit/crop, not accidental transparent gutters.

For a cutout request background=transparent. Inspect actual alpha and its edges on the planned
ground; reject baked checkerboards, white boxes, halos and changed product details.
IMAGE_TRANSPARENCY_UNSUPPORTED means the provider cannot honor the request;
IMAGE_TRANSPARENCY_MISSING means the result lacks alpha. A PNG extension proves neither.
Preserve the source. Logo edits must preserve exact letters and mark geometry; a crop cannot
remove white within a letter or an opaque plate. Preserve intentional Brand plates.

Poll `get_image_job`, then use `get_completed_image_asset`: it returns the public url,
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

elementKinds: text, button, image, icon, shape
shapeKinds: rect, rounded, circle, ellipse, triangle, diamond, pentagon, hexagon, polygon, star, line, arrow, freeform
operations: set_document_metadata, set_frame_state, update_frame, insert_node, update_node, group_nodes, ungroup_nodes, duplicate_nodes, move_nodes, align_nodes, distribute_nodes, upsert_reusable_block, instantiate_reusable_block, detach_reusable_block, upsert_text_style, bind_text_style, set_text_style_overrides, reset_text_style_overrides, detach_text_style, upsert_saved_style, apply_saved_style, upsert_custom_font, remove_node, create_export_region, rename_export_region, create_component, update_component, create_component_variant, instantiate_component, set_instance_variant, set_instance_property, set_instance_override, swap_instance, reset_instance_overrides, detach_instance, bind_variable, unbind_variable, create_variable, update_variable, remove_variable, move_node, reorder_nodes, set_auto_layout, remove_auto_layout
exporters: delivery_preview, compatible_html, png, pdf, svg, pen, figma_json, klaviyo
recipes: linked_shape_text_cta

Use one 600px frame; grow height with update_frame. Fully off-frame elements are dropped.
set_frame_state controls root Lock/Eye; a hidden root cannot preview/export.
New CTA nodes use the `linked_shape_text_cta` recipe: Shape + Text with shared groupId and href.
Style them freely, including supported Drop Shadow; never create a legacy button node.
Move/resize the pair together and exclude both members from set_auto_layout to preserve overlap
and the compiled semantic link. A reusable CTA may be saved at Campaign, Brand, or Global scope.

For ordinary optional fields, update_node with unsetProperties and an empty patch removes a
link/effect; do not send null, remove required fields, or both patch and unset a field.
Change a shared group URL on every member in one batch. For component members use
set_instance_override with sectionId, instanceId, sourceElementId and patch; an empty href clears
the link without resetting unrelated overrides. Use complete groups and touched Auto Layout trees
when grouping, moving or duplicating; locked nodes must be unlocked first.
Managed Auto Layout children require layout operations; intentional overlap does not belong in it.
Components/Variables resolve through typed operations; invalid definitions and cycles fail closed.

Inside text, `**` enables bold and `==` uses accentColor; without that color it is plain text.
Rotated text is baked into imagery and ceases to be live text. Gradients and translucent/freeform
shapes may also be baked and skip dark-mode color rewriting; inspect their recipient rendering.

## Optional shared libraries and export

Use list_mayledit_library with emailId for Campaign/Brand visibility or brandId for Brand.
Global means this workspace. Library saves use fresh context/idempotency; updates also require
id/expectedVersion. Use definitions from the capabilities' libraries category, not invented fields.
Global mutations require an admin. Defaults become persistent only after an explicit save.

Library changes and document instances are separate: upsert_reusable_block then
instantiate_reusable_block imports a block; upsert_text_style then bind_text_style imports a style.
Local overrides remain local; do not silently promote them to the catalog.
Delete needs a confirmation challenge bound to the complete delete payload, item id/version and
action delete_mayledit_library_item, then the same payload with confirmationToken.
Do not bypass confirmation on retry; retain the idempotency key.

export_email_document takes exactly one stored revisionId or versionId. Named-region PNG/SVG
requires a permitted region format; inspect fidelity warnings and use downloadUrl before expiry.
compatible_html and recipient preview use the compiled delivery artifact. Klaviyo publication is
the operator's Submit to Klaviyo action; never invent an account/template or publish intent.

## Delivery evidence and completion failures

Compile the current WIP with `compile_email_wip`; repair blocking diagnostics and compile again.
`complete_agent_run` requires the exact current WIP's bound artifact with no blocking errors.
EMAIL_AGENT_DELIVERY_NOT_READY/BLOCKED mean production is incomplete, not bypassable warnings.

For `get_email_preview_image`, use renderMode=delivery, compiled revisionId and
request both `viewportWidth` 600 and 390. Check revision/artifact identity against compile.
Canvas pixels are not proof of desktop or mobile delivery; repair a delivery failure rather
than changing renderMode. Inspect the opening and each section with `clip` containing x, y, width
and height in CSS pixels. Bound clips by contentHeight and that viewport's width; mobile
coordinates come from its 390px layout, not the 600px canvas. Detail pixels are returned directly,
including when no `imageUrl` exists. Do not invent URLs or local files for image blocks.
A downsampled full-mail image is insufficient to assess tiny text or collisions; view detail.
If pixels cannot actually be viewed, report the gap. Neither compile success nor an immutable
version is customer approval; preserve that distinction in every subsequent reference decision.
