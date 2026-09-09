---
name: email-production
description: Produce and revise brand-safe Mayland emails through the connected release.
---

# Email Production

Build one Mayland email at a time. Mayledit is your canvas and you drive it through MCP the
same way you would drive a design tool: read the document, place nodes, compile, look at the
result, fix what is wrong.

This skill carries the craft. It carries no brand values. Every colour, font, phrase, claim,
product fact and rule of address comes from the connected Mayland release. If a brand value is
missing, say so and stop. Never substitute a plausible one.

## Prompt library - preserve the assignment before production

This workflow applies to a single email, a campaign, or several campaigns for one brand.
The email-by-email build loop below does not create a separate prompt line for each tool or mail.
Prompts preserve reusable production instructions; the catalog preserves verified brand facts,
and Learnings keep their existing independent proposal and approval flow.

### Prepare the assignment before saving

For a normal new commission, automatically prepare the user's original business request before
saving V1 and before producing the email. The external agent explicitly carries `rawAssignment`
(the user's original production request, not a chat transcript) into this workflow. MCP sees only
the fields actually submitted to its tools; it does not listen to the rest of the conversation.
Do not replace the original request with your interpretation or manufacture missing user wishes.
If an explicitly requested briefing is still `briefingStatus=collecting`, remain in that ongoing
briefing and its existing prompt line; loading this guide does not authorize production. Proceed
only when it hands off ready, or stop when cancelled. An ordinary request without briefing state
does not start this interview path.

Use read-only lookups of the existing target brand, relevant products, suitable references and
approved Learnings to resolve what is already known. Reuse verified context already returned in
this assignment when still current. Do not launch a website/product scraper, save new catalog
facts, create images or mutate an email merely to prepare the instruction. Separate sourced facts
from the user's explicit choices; a reference image is design inspiration, not proof of an offer.

Structure a concise `preparedExecutionIntent` in the agent's working context:

- Goal: what this assignment should accomplish, without inventing another campaign objective.
- Content: the selected, verified products/facts and requested message, including the required length.
- Design: the requested mood/composition within the target brand's design system and binding Learnings.
- CTA: the action and verified destination supported by the request and brand context; never invent
  an offer, discount, urgency, price, claim or unsupported destination to fill an empty slot.
- Constraints: preserve every explicit restriction, omission, language choice and user correction.

Unknown information stays unknown. Ask only a targeted question when missing or ambiguous brand,
product, campaign or necessary content would materially change the result. A clearly identified
target is not another confirmation step. Do not turn an understandable request into a compulsory
interview, an Enhance command, a prompt editor or a request to copy and resubmit an improved prompt.
The normal workflow never activates `/mayland:briefing` automatically. Missing optional inspiration
does not block an otherwise supported instruction; do not fill it with fictional facts.

Keep two distinct representations: `preparedExecutionIntent` retains concrete, authorized target
facts and tool-returned identity bindings; `generalizedBody` is a coherent reusable instruction
for the Prompt library, preserving useful goals/design/constraints while letting a later target
provide its own facts. Generalizing must not erase a requested product category or restriction.
Neither representation is a generic rewriter for technical MCP arguments: copy tool-returned IDs,
locks, revisions, idempotency keys and structured mutations verbatim through their normal contracts.
These working-context labels are not new MCP fields, persisted secret documents or new tools.

For a new assignment, use the prepared `generalizedBody` as create_prompt's body under the Save
the first version rules below. After its confirmed save receipt and any necessary targeted answer,
continue directly into email creation. A brief description of the intended result is enough in
chat. Do not wait for an extra approval, pasteback or resubmit. Creating a draft is not authorization
to send, publish, sign off or launch a campaign.

When an explicit briefing hands off `briefingStatus=ready`, reuse `rawAssignment`, confirmed
requirements, verified target/product/campaign/source bindings and its existing `promptIdentity`
with requestKey, currentVersionId and last save receipt. Do not create another V1, repeat the
interview or save an identical revision merely because this skill started. If the briefing already
saved its latest consolidated requirements, continue from that receipt. Otherwise save only the
outstanding substantive iteration on the same line before production. A cancelled briefing stops
production; it does not silently delete or trash the prompt already saved. An interrupted ordinary
assignment likewise resumes its existing line; uncertainty about identity is not permission to
mint a duplicate. Read-only requests still do not create any line or email.

At compose time explicitly disclose the original `rawAssignment` as `agentInput.userPrompt` and
the effective concrete `preparedExecutionIntent` as `agentInput.productionInstruction`, alongside
the existing version/model/document disclosures. Keep later confirmed corrections in the effective
instruction, not as a fabricated replacement of the user's original request. No credentials,
unrelated conversation, hidden host instructions or fabricated model settings belong in either.
Recorded-plan replay is different: it restores its saved inputs and must not receive a freshly
rewritten plan or new agentInput. Respect the existing input size limits; never silently truncate
and claim the original request was captured completely.

Worked example: "Mach für Glycowohl eine Magnesiummail, bisschen winterlich, wenig Text, Produkt
soll auffallen." If the authorized catalog identifies one matching magnesium product, prepare a
short product email with a winter mood inside that brand's design rules, the selected product as
the focal point, concise verified facts and an appropriate CTA to its verified page. The reusable
body keeps the winter mood, brevity and magnesium-product focus; the execution context retains the
actual Glycowohl/product bindings. Do not add a winter discount, a medical promise or a deadline.
If two magnesium products match, ask which product; do not pick one to avoid asking. If the user
also said "no emojis", keep that restriction in both representations.

### Save the first version

First distinguish a new commission from resuming a tracked assignment and from read-only work.
Read-only inspection or export does not create a prompt line. When continuing an existing line,
resolve its retained P-ID, keep the assignment's requestKey and use the iteration workflow for new
feedback. A restarted skill or reconnected session is not a new commission. If the previous line
cannot be identified reliably, clarify that identity rather than guessing or duplicating it.

Before production research, campaign creation, copy work, image jobs, or email/document mutations,
resolve the requested brand with read-only tools and, for a new assignment, save Version 1 with `create_prompt`.
Ask for a missing or genuinely ambiguous brand; never ask the user to reconfirm an explicit,
unambiguous target. Source-prompt, brand, product, reference and approved-Learning lookups may
precede this first save to prepare the instruction from existing evidence. No Context Pack
is required by the prompt-library tools. Continue into Step 0 only after a successful save receipt.

Supply `brandId`, `scope`, `title`, `body`, `requestKey` and `operationKey`. Set scope to EMAIL for
one email, CAMPAIGN for one campaign, or MULTI_CAMPAIGN for several campaigns of the same brand.
Choose one requestKey for the whole brand-bound assignment and keep it through every campaign,
tool call, document revision, interruption and retry. A distinct new assignment gets a new
requestKey even when its wording is identical. Use one operationKey for this first save and
another stable operationKey for each later substantive iteration. Preserve both keys in the
working context; never derive a new key merely because a request timed out.

Write a directly reusable, coherent body from the user's actual objective and supported instructions.
Keep useful composition, audience, tone, length and workflow constraints. Generalize brand names,
specific products, offers, prices and dates into roles the next target's own authorized context
can fill. Do not carry an original brand's promotion into another brand, invent facts, strengthen
claims, add supposed user preferences, or save hidden system instructions, credentials or unrelated
chat messages. Keep the original request and the current target's concrete facts in the production
context, so generalizing the library text never changes the actual assignment. Explicit restrictions
remain binding. Preparation and saving belong to the normal production workflow; they do not
introduce a separate briefing interview or another user-facing prompt-enhancement step.

Keep the returned prompt `id`, `code`, `brandId`, `scope` and `currentVersionId`, together with the
returned version `id` and `version`. Only that receipt proves the P-ID and Version 1 exist.
If saving fails or times out, explain the unsaved state and retry the exact payload with the same
requestKey and operationKey. Never report a successful save, invent a P-ID, create a duplicate line,
or begin production while the first save remains unconfirmed. PROMPT_OPERATION_CONFLICT means
the key was already used with different content; inspect the existing assignment rather than
silently minting a replacement key. A library save never authorizes sending or publishing.

### Consolidate each substantive iteration

For each later user-directed substantive iteration, automatically call `revise_prompt` on the same
promptId with its last confirmed `expectedVersionId`, a stable `operationKey`, and a complete
replacement `title` and `body`. Save before applying that iteration's production changes. No
additional user approval is needed for each prompt version. Keep the still-valid earlier details
and incorporate the new instructions into one directly usable brief; do not append a chat transcript
or a list of corrections. For example, "more emojis" followed by "no emojis" leaves only "no emojis"
in the current body. The earlier preference survives in immutable version history.

Technical retries, polling, compiler repairs and document revisions are not automatically substantive
iterations and must not create prompt versions. A retry of an uncertain save uses the same keys,
expectedVersionId and body; never infer failure from a timeout and submit a duplicate update.
After a successful revision, replace the working currentVersionId with the returned version id.

On PROMPT_VERSION_CONFLICT, stop the stale write and use `resolve_prompt` to read the current line.
Preserve any intervening manual edits. If the current body already contains the intended iteration,
do not write it again. Otherwise reconcile only changes whose intent is clear, and base the
consolidated update on the freshly returned version. Ask the user only when their manual change
and the requested iteration conflict materially; never silently overwrite it or force an old body.
An explicit version conflict commits no receipt, so the reconciled write keeps that iteration's
operationKey with its new expectedVersionId and body. This is different from an uncertain transport
failure, which must retry the original payload unchanged.
TRASHED means the line is not active: do not revive it, use it as a template, or replace it with a
new line silently. Restore only when the user requests restoration.
Use `set_prompt_status` for that explicit lifecycle request with both the current expectedVersionId
and `expectedUpdatedAt`, copied verbatim from the prompt's returned updatedAt. Never round or invent
that timestamp; a newer trash/restore decision must not be overwritten by stale state.

### Read and reuse without changing the source

The /mayland P-1234 workflow uses `resolve_prompt` with `code` to retrieve one exact version.
Read-only lookup, showing the text, copying it, and `list_prompt_versions` never create a prompt
line or start production. Keep the returned version id pinned; never reinterpret it as "whatever
is latest" later. If the user selected a historical version, pass its `versionId` when resolving.
Report an inaccessible, missing or trashed source instead of guessing its text or choosing another.

When the user actually commissions new work from that source, use `create_prompt` for the target
brand with a new requestKey and operationKey and the exact pinned `sourceVersionId`. The new line
gets its own P-ID; never use revise_prompt on the source to represent reuse. Preserve the source's
generalized intent while using the target brand's own facts, products, references and approved
Learnings. A later source edit must not change an assignment that has already started.

For one request covering several target brands, make one separate assignment and prompt line per
brand, all pointing to the same pinned sourceVersionId. Do not request extra confirmation merely
for this internal split. Several campaigns of one brand still use one MULTI_CAMPAIGN line. Route
later feedback only to the explicitly affected brand's line; it must not mutate another target's
line or the source. Brand ownership metadata never means "may only be reused for this brand";
normal workspace and brand permissions remain binding for each target.

The same split works with a prompt copied from the UI. Use its supplied source P-ID/version when
available and resolve that exact source through MCP. If only plain text was copied, keep it as the
new assignment's generalized input; do not invent source provenance. Clarify source identity only
if the user requires attribution that cannot be established from the provided text.
The UI's readable source footer contains the P-ID and numeric version. Resolve that P-ID, use
`list_prompt_versions` on its returned promptId to find the matching version number, then resolve
that exact versionId. Never substitute the source's latest version when the copied number differs.
If no matching version is available, report that fact rather than inventing its identifier.

### Client feedback and observed edits

`list_client_review_feedback` reads comments for the correct email and released version; reading a
client comment alone never changes a prompt or creates a version. Only an explicit user instruction
to adopt that feedback enters the substantive-iteration workflow. Do not import all comments into
the prompt library. A manual editor change is not proof of a feedback reason: if an authorized
iteration summarizes observed edits, describe only the changes actually demonstrated by the saved
document, without inventing motivation. Learning proposals remain separate and never replace,
delete or automatically rewrite prompt versions.

### Prompt-tool request examples

These examples show contract shapes, not reusable identifiers. Replace every id and key with the
actual target, saved receipt and once-chosen assignment keys. The body is the complete generalized
instruction. A second target uses a different requestKey and operationKey but the same sourceVersionId.

```json
{"tool":"resolve_prompt","arguments":{"code":"P-1234"}}
```

```json
{"tool":"create_prompt","arguments":{"brandId":"11111111-1111-4111-8111-111111111111","scope":"MULTI_CAMPAIGN","title":"Concise product campaigns","body":"Create concise product campaigns using the target brand's verified product facts and design language. Give the product a clear focal point and use one primary call to action. Do not invent offers or health claims.","requestKey":"assignment-a-brand-a","operationKey":"assignment-a-brand-a-v1"}}
```

```json
{"tool":"revise_prompt","arguments":{"promptId":"22222222-2222-4222-8222-222222222222","expectedVersionId":"33333333-3333-4333-8333-333333333333","operationKey":"assignment-a-brand-a-iteration-2","title":"Concise product campaigns","body":"Create concise product campaigns using the target brand's verified product facts and design language. Give the product a clear focal point and use one primary call to action. Use no emojis. Do not invent offers or health claims."}}
```

```json
{"tool":"create_prompt","arguments":{"brandId":"44444444-4444-4444-8444-444444444444","scope":"EMAIL","title":"Concise product email","body":"Create a concise product email using the target brand's verified product facts and design language. Give the product a clear focal point and use one primary call to action. Use no emojis. Do not invent offers or health claims.","requestKey":"assignment-b-brand-b","operationKey":"assignment-b-brand-b-v1","sourceVersionId":"55555555-5555-4555-8555-555555555555"}}
```

```json
{"tool":"create_prompt","arguments":{"brandId":"66666666-6666-4666-8666-666666666666","scope":"EMAIL","title":"Concise product email","body":"Create a concise product email using the target brand's verified product facts and design language. Give the product a clear focal point and use one primary call to action. Use no emojis. Do not invent offers or health claims.","requestKey":"assignment-b-brand-c","operationKey":"assignment-b-brand-c-v1","sourceVersionId":"55555555-5555-4555-8555-555555555555"}}
```

Only for an explicit request to move this line to the trash, using its current returned timestamp:

```json
{"tool":"set_prompt_status","arguments":{"promptId":"22222222-2222-4222-8222-222222222222","expectedVersionId":"33333333-3333-4333-8333-333333333333","expectedUpdatedAt":"2026-09-10T08:00:00.123456+00:00","status":"TRASHED","operationKey":"assignment-a-brand-a-trash"}}
```

## Step 0 - Load the identity after saving Version 1 (mandatory)

Before you design anything:

1. `list_campaigns` for the brand, and settle where this mail belongs before minting the production pack.
   Every email lives on exactly one campaign board. Reuse an explicit, validated campaign selection
   from the user's request or briefing handoff without asking again. If the user explicitly supplied
   a new campaign name, check for an existing matching board first and, if absent, call
   `create_campaign` with that name without another naming question. Use its returned ID.
   Ask which board only when that decision is missing or genuinely ambiguous; show the available
   boards then. If none fits and no new name was supplied, ask for that name. Never guess the board and never silently let
   the mail fall into Unassigned. A campaign is a board that holds emails, which is a different
   thing from a campaign goal: goals are reusable briefing intents and hold nothing.
2. `get_brand_context` for a fresh context pack. Re-read it after any interruption.
3. `list_products` and `get_product_context` for the products the mail actually promotes.
4. Discover both collections with `list_reference_emails`: use `scope=BRAND` with the target
   `brandId` for Brand Emails, and explicit `scope=WORKSPACE` without a Brand for Swipe File.
   Follow `nextCursor` while searching the library; the three-reference limit belongs to one
   run's selection, not to the gallery. Then `get_reference_email` for suitable candidates and
   inspect the returned preview image block, or open its signed `imageUrl`. See the reference
   selection rules below. Keep the collections distinct; shared inspiration never overwrites
   the target Brand's reference information.
5. `list_approved_learnings` for what this brand has already agreed to. These carry the design
   corrections earlier reviews produced and they bind exactly like the profile does.

Settle any outstanding campaign ambiguity before you mint the final production pack. A pack goes
stale while you talk; already answered campaign decisions must not trigger the same question again.

Every id you pass (emails, runs, packs, assets) is copied verbatim from a tool result in this
conversation, never reconstructed from memory. On `CONTEXT_PACK_RUN_MISMATCH`, call `get_email_wip`
and use its `activeAgentRunId` exactly; do not retry with a guessed id.

When any tool result carries a `PLUGIN_UPDATE_RECOMMENDED` warning, run the two plugin update
commands (`claude plugin marketplace update mayland`, then `claude plugin update mayland@mayland --scope user`),
finish the current step, and tell the user to start a new conversation so the updated plugin loads.

Read the brand profile as a design brief, not as decoration:
- `designTokens.colors` hands you the palette already sorted into roles: `bg` and `surface` for
  grounds, `band` with `onBand` for the full-width bands, `ink` and `muted` for type, `accent`
  with `accentInk` for the buttons and the signal moments. Use the roles rather than picking
  from `palette` by eye, and keep the accent for what should be loud. `accentInk` is the only
  colour that goes on top of the accent.
- Band colours follow the reference register: the deep `band` tone carries the full-width
  statement bands and the light `surface` tint carries the supporting surfaces, exactly as the
  `designTokens.colors` roles name them. Never invert the pair; a mail that sets its statement
  bands on the light tint and spends the deep tone on side surfaces reads as a different brand.
- When the brand's reference newsletters open with a trust or preheader bar above the hero, the
  plan opens the same way: preheader_trust_bar is the first block, and every item in it is a
  catalog fact (the furniture benefits, guarantee or shipping lines), never a line written for
  the occasion.
- `brandMarks` lists the marks you may place inside the mail, each with the background it is cut
  for. Prefer the entry flagged `isWordmark` in the header, fall back to `isLogo`, and never put
  a mark cut for a light ground onto a dark band.
- `displayFont`, `letterSpacing`, `imageryStyle` and `designTokens.form` set the type, picture
  and shape register: edge style, density, button shape and fill, section rhythm.
- `visualSummary` describes the layout system, the module vocabulary and the button treatment.
- `voiceSummary` and `tone` set the register and the form of address.
- `noGo` is binding. A mail that breaks one of these is wrong even if it looks good.
- `furniture` holds the footer, the legal links and the service benefits. Use it verbatim.
- `mandatoryStatements` are the lines this brand is legally required to carry. Every one of them
  has to appear in the mail, worded exactly as given.
- Product `truth` and `benefits` are the only claims you may make.

## What you take from a reference and what you leave

An explicit user selection takes precedence over automatic alternatives. Resolve the exact
user-chosen references from tool results, including choices retained from the briefing or Prompt
handoff; never substitute a similarly titled entry or silently replace them with the rotation.
Without an explicit selection, choose suitable ready references from either collection yourself.
Select at most three in total across Brand Emails and Swipe File. If the user requests more,
ask which three to use rather than silently dropping a requested source.

Check processing state and actual image access for every selected reference before design.
PENDING, PROCESSING, FAILED, inactive entries or missing/unreadable images are not usable visual
inspiration. Name the unavailable source and the gap; never claim visual inspection from a title,
tags, extracted text or a tool's success status alone. Retry a signed image URL by fetching fresh
detail when it expires. If an explicit reference remains unavailable, ask whether to wait or
proceed without it. Missing optional automatic inspiration permits an honest original concept.

After `create_email`, read `get_email_wip` and reuse its non-null `activeAgentRunId`. If it has
no active run, call `create_bulk_agent_run_group` with the fresh `contextPackId` and
`contextPackHash`, a stable `idempotencyKey`, and `emails` containing this one `emailId` and
its `brief`. Despite its name, the tool supports a single email and acquires its run's lock.
Use that email's returned `childRuns` entry for the exact `agentRunId` and `fencingToken`.
Retry an uncertain start with the same payload and key; do not create another group or run.
Use the verified active run as `agentRunId` for `select_run_references`; never invent an ID.
Supply the fresh context pack binding, the exact ordered `referenceEmailIds` and a stable
`idempotencyKey`. Set `selectionSource=USER` for explicit choices or `AUTOMATIC` for your choices.
Do this before composing or editing the design. Retain the returned `selectionReceipt` id,
selectionSource and ordered sources with their scope, Brand assignment, contentHash and
snapshotAssetId in the assignment context. Only a successful receipt proves durable binding;
an uncertain call retries the same payload and key. Do not invent receipt IDs or image-viewing
proof. A server receipt records the selected source, not whether the host actually displayed it.
A replay of a historical selection may lack `selectionReceipt`. Report that provenance gap;
do not fabricate a receipt or claim the older selection has the new source history. For a new
production operation, require the new receipt before design; a missing receipt needs investigation.
On `REFERENCE_USER_SELECTION_REQUIRED`, preserve the user's choice; do not relabel an automatic
replacement as USER to bypass it. A later explicit change needs a new selection operation and
receipt, preserving the earlier history. Run selections supplement the production context;
never mutate or substitute the target Brand's identity pack with Swipe File contents.

Reference emails are the calibre bar, and reaching it visually is the job. Study one until you can
name why it reads well, then build that same reading experience with this brand's own material.

**Open the reference image before you build anything.** Most references are captures of a sent
mail, so every bit of craft sits in the picture: inspect the image block returned by
`get_reference_email`, or open the signed `imageUrl` from that same result when no image block is
present. A reference you have not looked at teaches you nothing, and building from its title and
tags alone is how mails end up generic. While you look
at it, name for yourself the band count down the page, where the density changes, which modules
repeat, how far the type sizes sit apart, and how the button is treated. Those are the numbers you
build against, and `layoutSignature` on the sibling mails is what you compare them to.

Take the craft: the layout system and its column logic, the rhythm of the bands down the page and
where they change density, the module vocabulary the mail draws from, the type hierarchy and how
far the sizes are apart, the button treatment, and the way the page breathes between blocks.

Leave everything that belongs to the mail it was made for: its copy, its offers, its prices,
percentages and other numbers, its images and its brand marks. Those are not craft, they are that
sender's content, and none of it is true for this brand unless the brand kit says so.
Colours, fonts, logos, products, prices and binding claims always come from the target Brand and
confirmed assignment. A Swipe File palette or foreign logo is not catalog evidence. Record the
transferable layout idea (for example, its product-table rhythm) in the effective production
instruction while retaining the source receipt separately from the reusable Prompt body.

Structural quotation stays a resemblance, never a copy. Two mails may share the same rhythm and
still read as different mails, and inside one campaign the variation rule below still applies.

Never invent a price, an availability, a discount, a review or a statistic. If the mail needs a
fact the brand kit does not contain, ask for it.

## When something is missing

Report gaps before building, in exactly three lines: what is missing and what it is needed for,
what the user should deliver in what form, and what you can do instead in the meantime. One
report for all gaps, not one conversation per gap. Run this check between Step 0 and the first
build call: enough imagery for the planned mails, a claim source for every planned section,
identity fields the design depends on.

## Substance the pack carries beyond the profile

- Product context `sections` carry researched pain points with sources. Awareness and story
  openers draw the problem from there instead of inventing one.
- The brand `notes` field carries a labelled pool of researched CTA imperatives. Button copy
  comes from that pool, each mail using a different entry; never invent a generic label.
- `list_assets` types every motif: hero scenes for hero grounds, cutouts for poster moments and
  colour heroes, hand interactions and details for body sections, variants for tickers. Pick by
  role instead of reusing the packshot everywhere.

## The canvas

One flat frame, 600px wide, named as the email frame. Every element is a child of that frame.
Do not add further sections: the compiler reads the first section only, so anything you place
outside it is silently dropped. Visual bands are full-bleed rectangles at x=0, w=600.

Scale, in document pixels at 600px width:

| Element | Size |
|---|---|
| XXL punchline | 58-128, never below 56 |
| Kicker, caps | 18-23 |
| Sub | 21-29 |
| Hero CTA | 427x82, text ~39 |
| Body CTA | 533x82 |
| Final headline | 50-56 |
| Section headings | 20-23 |
| Body text | ~17, never below 16 |
| Stat numbers | ~50 |
| Cards | 500 wide |
| Spacing kicker to punch | 11 |
| Spacing punch to punch | 11 |
| Spacing stack to sub | 22 |

Vertical space has exactly three values and no others: 11 inside a group, 22 between elements,
44 between blocks. Compose from the plan and the builder holds this for you. When you place or
move a node by hand afterwards, keep it: a 12 or an 18 anywhere on the page is what makes a mail
look assembled rather than designed, and it is the first thing a client sees.

A shaped section edge is drawn into the space above the seam, so a send that uses one gives every
block boundary a step of its own for it: 44 stays clear above the crest and the crest takes the
next 22. The builder does this for you. Do not hand-place one tighter.

Marks carry a ground. `brandMarks` says which background each one is cut for, and an image entry
in the plan says the same with a ground field. A mark cut for a dark ground placed on a light band is
invisible, and nothing downstream can see that it happened, so pass it: the builder falls back to
the wordmark when the two disagree rather than drawing white on white.

The impact hero puts the mark on the surfaceTint band when the plan carries one; without a tint
it sits on the photo under a dark scrim. Pick the mark for THAT ground: dark-ground mark
(usually the white cutout wordmark) when there is no tint or the tint is dark, the colored
cutout with a light ground when the tint is light. Every other hero draws the mark on a light
surface and takes the colored cutout. Prefer transparent cutouts over marks with a baked
background plate: the plate reads as a sticker on any ground that is not exactly its own.

Autoscale: make the punchline as large as the column allows, shrink in 8% steps if it displaces
the sub, and stop at the floor. Multi-line headlines never sit at 100% line height, use 110% or
more. Single-line punchlines may use 100-104%.

Corner radius, button shape and letter spacing are brand properties. Read them from the profile
rather than choosing a house default.

## The element vocabulary

`insert_node` accepts text, image, icon and shape; legacy button nodes are read/export-only.
Every operation and nested definition uses a strict schema: unknown or misspelled fields are rejected.
Use complete examples from `get_mayledit_capabilities` and the tool schema.

- Text: `text`, `tag` (h1, h2 or p), `color`, `size`, `weight`, `align`, `lh`, `ls`, `italic`,
  `underline`, `transform` for casing, `valign`, and `accentColor` for the accent runs below.
- Legacy button nodes may be read, moved, or repaired for an existing document, but never create
  a new one. For a new CTA use the Shape + Text recipe from `linked_shape_text_cta`.
- Image: `src`, `alt`, `label`, `fit` (cover, contain or fill), `radius`, and an optional `crop`
  region in source fractions.
- Icon: search with `search_email_icons`, then import the chosen library/id with
  `import_email_icon`. Insert the returned `sourceSvg` and immutable Mayland CDN `src` together
  with `color`, `background`, `padding`, `radius`, `href`, `decorative` and `alt`. Imported icons
  default to decorative; when an icon carries meaning, set `decorative` false and write an alt
  that names that meaning. Recipient HTML never references Iconstack.
- Shape: `shape` is one of rect, rounded, circle, ellipse, line, triangle, diamond, pentagon,
  hexagon, star, arrow or freeform. `fill`, `radius`, `opacity` 0..1, `stroke` with `strokeW`
  and `dash`, an optional `gradient` of `{from, to, angle}` in CSS degrees, and for freeform a
  `path` of SVG data in a 0..100 viewBox that scales with the element box. A Shape also accepts
  an optional validated `href` and a bounded Drop Shadow through `shadow` with `x`, `y`, `blur`
  and `color`. Empty links never emit anchors.
- Every element carries `rotation` in degrees. Rotated text and buttons are baked to an image at
  compile so the tilt survives email clients; they stop being live text, so keep tilts for
  badges, stickers and cutouts, never for body copy.

Gradient, stroked, translucent and freeform shapes ship as baked SVG and skip the dark-mode
colour rewrite, so check the preview against a dark ground when you lean on them.

Inside text, `**` markers bold a phrase and `==` markers set it in the element's `accentColor`.
The accent run is for the one word a headline turns on; without `accentColor` on the element the
markers degrade to plain text.

## Transitions between bands

Flat edges between bands read as a spreadsheet. Between two bands whose colours differ, place a
named transition: a full-width freeform shape spanning the seam, around 46px tall, filled with
the arriving band's colour, above the leaving band's imagery and below any text. One transition
style per mail, varied across the campaign:

| Name | Path in the 0..100 viewBox |
|---|---|
| wave | M0,100 L0,45 C18,18 34,72 50,45 C66,18 82,72 100,45 L100,100 Z |
| scallop | M0,100 L0,60 Q12.5,20 25,60 Q37.5,20 50,60 Q62.5,20 75,60 Q87.5,20 100,60 L100,100 Z |
| s_curve | M0,100 L0,55 C30,10 70,90 100,40 L100,100 Z |
| diagonal | M0,100 L0,70 L100,20 L100,100 Z |
| arc | M0,100 L0,58 Q50,8 100,58 L100,100 Z |
| step | M0,100 L0,70 L33,70 L33,25 L67,25 L67,70 L100,70 L100,100 Z |
| torn | M0,100 L0,44 L5,76 L10,44 L15,76 L20,44 L25,76 L30,44 L35,76 L40,44 L45,76 L50,44 L55,76 L60,44 L65,76 L70,44 L75,76 L80,44 L85,76 L90,44 L95,76 L100,44 L100,100 Z |

A soft fade is the seventh option: a full-width `gradient` rectangle from the leaving colour to
the arriving one. The variation rule below includes the transition: neighbouring mails in a
campaign do not share one.

## Depth and energy

A premium page has layers. Flat rectangles stacked edge to edge are the look the client called
cheap, so every mail carries at least one depth device:

- Cutouts and badge shapes rotate up to 10 degrees either way; band strips 3 to 4 degrees.
- Card stacks offset: the second card sits about 60px lower and slightly aside.
- A lift shadow is a near-black copy of the shape, offset a few pixels, `opacity` 0.13, one z
  below its subject.
- The product cutout sits on the highest z of its section, and text never runs beneath it.
- Overlap is a tool on grounds and shapes. The legibility rules stand: nothing overlaps type,
  buttons or word endings.

## Gradient art direction

Build hero and closing grounds from the pack's own colours, never from invented ones: an urgency
ground runs from the darkest palette tone into `band`, a fresh ground from the lightest tint into
white, a premium ground from `band` into a near-black of it. Use the role colours as the stops
and keep one gradient family per mail.

## Hero anatomy

Top to bottom: logo, badge pill naming the occasion in caps, kicker line, XXL punchline with
exactly one word in the accent colour, sub of two to three lines, the primary CTA, then a
micro-trust capsule. Background is a scene image with the subject off-centre so type has room,
plus an overlay that guarantees legibility, plus a transition shape into the body.

Four headline styles. Use exactly one per mail and vary across a campaign: a single giant word
after a mini kicker; two or three stacked caps lines each filling the width; a caps line paired
with an italic accent line; or a size mix of small, giant and medium lines.

For a colour hero without a photo: full-bleed brand colour, text left, text column at most
350px, product cutout right, and the cutout never touches the text column.

## Body

Transition, then the sections, drawn from a varied library: alternating image and text
rows, a three-up number band, a stacked stat, an icon promise grid, a framed code box, a
marker-highlighted statement, a two-column comparison, a product picks grid, a single large
review panel, verified buyer cards, a before and after, or a dark icon band. Then a second CTA
carrying the same call as the first, a closing headline with a short sign-off line, and the
brand's own service and footer furniture.

Some section types the library does not ship as blocks are composable from primitives:

- Chat bubbles: alternating rounded rects with a small triangle tail, question left, answer right.
- Gauge: a half ellipse over a band, the score as a stat number at its centre.
- Highlighter: a statement line with a `backgroundColor` on the text element as the marker sweep.
- Q and A cards: an objection as a quoted card, the answer as body text beneath it.
- Stat stack: the numbers of a stat row stacked vertically with hairline rules between them.
- Dark icon band: a `band`-coloured strip with two rows of three icon tiles and caps labels.
- Colour ticker: variant chips as a single row of small rounded rects in the variant colours.

### How many sections

The reference sets the length, not a number in this file. Count the sections in the reference
you were given and build at least that many. With no reference, six to ten is the working range
for a promotional mail: a mail that ends after three sections is a fragment, and it reads as one
next to a real brand mail.

Length is a symptom, not the goal. Each section has to earn its place with something the reader
did not already have: a different argument, a different proof, a different way of looking. Three
paraphrases of the same claim are worse than one section. When you run out of substance, that is
the signal to fetch more from the product context, not to stop early.

Check the finished mail against the reference with `get_email_preview_image`: if yours is half
as tall, you left the argument unfinished.

Variation is a hard rule: each mail in a campaign needs a combination of transition, hero
background, headline style and sections that its neighbours do not have.

## Copy

The kicker sets a concrete scene, the punchline pays it off. Provoke the next line. One thought
per sentence, no nested clauses. Lead with the reader's benefit, not with the brand.

Register rules only. Never copy a sample sentence from anywhere, including this file. Write in
the brand's language and form of address. Keep caps for headlines and CTAs, never for body text.
Never use em dashes.

Text elements carry inline bold: wrap a phrase in `**` markers and it compiles to bold in the
mail. Use it in running body text for the one phrase the paragraph exists for, at most once per
paragraph, so a skimming reader still gets the point. Headlines, kickers, CTAs and fine print
already carry their own weight, so leave the markers out of them.

State any offer with its size, its validity window and where it applies. Push conditions and
exclusions into the fine print, never into the selling text.

Subject under 45 characters, preheader continues the thought instead of repeating it. Offer
three to five subject and preheader pairs across different angles: a curiosity loop, the hero
scene, a number, honest urgency, and the direct benefit. No caps spam, no spam triggers, and at
most one emoji if the brand voice allows one.

Match the register to the funnel stage. Awareness leads with the problem and teaches without
pressing an offer. Consideration compares and proves. Offer stages lead with the offer and use
only urgency that is actually true.

## Build in Mayledit

Imagery first, then compose, then refine. Sessions expire after fifteen minutes and locks and
agent runs are bound to them, so never let a pending image job sit between two batches.

### Shared libraries

Call `get_mayledit_capabilities` with category set to libraries for version 1.12.0 library metadata.
Call `list_mayledit_library` with `emailId` for Campaign and Brand visibility, or `brandId`
for Brand visibility. Global means the current workspace. Only block and text_style kinds
are shared by these tools. Heading 1, Heading 2, Body, Caption and Eyebrow are default templates;
they become persistent items only after saving.

Use `save_mayledit_library_item` with a fresh `contextPackId`/`contextPackHash`, a stable
`idempotencyKey`, `kind`, `scope`, `name`, and a complete strict definition to create an item.
Block definitions require id, name, version set to 1, and elements normalized to origin 0,0.
Text style definitions require id, name, scope, tag, font, weight, size, italic, underline,
lineHeight, letterSpacing, transform, align, and color. Supply `id` and `expectedVersion` plus `name`, `scope`, or
`definition` to rename, move, or update. Campaign/Brand bindings derive from tenant-owned
`emailId`/`brandId`; never supply `campaignId` or `organizationId`. Global mutations require
a workspace admin. Reuse the returned item version on the next change.

For `delete_mayledit_library_item`, request a confirmation challenge with action
`delete_mayledit_library_item`, entityType set to mayledit_library_item, the item id, its version
as `expectedRevision`, and the complete delete payload without `confirmationToken`.
Then call delete with that payload and the returned token. Retries reuse the same idempotency key.

### Capability contract

Call `get_mayledit_capabilities` before the first mutation. Its versioned response is the
authority for the fixed frame, element and shape kinds, mutable properties, operation arguments,
batch limits and exporters. Do not infer a field from Figma or from an older conversation. Query
only the needed category on a refresh, and use one `apply_email_batch` for related changes.

The facts below are release-generated and contract-tested against that runtime response:

elementKinds: text, button, image, icon, shape
shapeKinds: rect, rounded, circle, ellipse, triangle, diamond, pentagon, hexagon, polygon, star, line, arrow, freeform
operations: set_document_metadata, set_frame_state, update_frame, insert_node, update_node, group_nodes, ungroup_nodes, duplicate_nodes, move_nodes, align_nodes, distribute_nodes, upsert_reusable_block, instantiate_reusable_block, detach_reusable_block, upsert_text_style, bind_text_style, set_text_style_overrides, reset_text_style_overrides, detach_text_style, upsert_saved_style, apply_saved_style, upsert_custom_font, remove_node, create_export_region, rename_export_region, create_component, update_component, create_component_variant, instantiate_component, set_instance_variant, set_instance_property, set_instance_override, swap_instance, reset_instance_overrides, detach_instance, bind_variable, unbind_variable, create_variable, update_variable, remove_variable, move_node, reorder_nodes, set_auto_layout, remove_auto_layout
exporters: delivery_preview, compatible_html, png, pdf, svg, pen, figma_json, klaviyo
recipes: linked_shape_text_cta

Preview displays the compiled delivery HTML. The editor has no separate Design preview.
An immutable Version keeps its exact approved artifact; a WIP preview compiles the saved current
WIP. Mobile preview uses a real 390px viewport. Client chrome in a browser is not a native
Apple/Gmail/Outlook rendering guarantee; use Client Lab evidence for client compatibility.

Create every new CTA from the `linked_shape_text_cta` recipe returned by capability discovery:
one rounded Shape background and one Text label share the same `groupId` and the same validated
`href`. Mayledit compiles that Shape + Text pair back into one live semantic email CTA, including
the Outlook fallback. Move and resize those two nodes as a group, and never include either member
in `set_auto_layout`; the operation rejects full and partial CTA-pair selections so the intentional
overlap and semantic link cannot be flattened. Do not insert a new legacy button node. A Shape + Text CTA can be saved as a
Reusable Block at Campaign, Brand, or Global scope; use the scope the user named and never promote
it silently.

The Email frame is always exactly 600px wide and there is exactly one. `update_frame` may change
only its name, background and height. Grow height when editing makes the mail longer; never try to
change width or add another section. `set_frame_state` controls root Lock and Eye. A hidden root
cannot preview, export or publish.

Components and Variables are ordinary typed batch operations. Create or update a Component,
define variants and exposed properties, instantiate it, then use instance operations for variant,
property, override, swap, reset or detach. Use typed Variable operations and bindings instead of
copying the same design value into every instance. The compiler resolves both systems to ordinary
email nodes; unresolved definitions, cycles and invalid bindings fail closed.

The Canvas shows design geometry; Preview and `compatible_html` use the compiled delivery
artifact used for sending and Klaviyo. Inspect the delivery result after visual refinement;
Canvas appearance does not waive a delivery warning. Klaviyo publication itself is a human UI action: leave
the approved artifact for the operator's `Submit to Klaviyo` confirmation and never invent an
account, template id, template name or create/update intent through MCP.

### Executable Canvas actions in Claude Code and Codex

These are protocol-level workflows for either client connected to the Mayland MCP server.
Use the same fresh Context Pack, email lock, fencing token and expected WIP revision for
`apply_email_batch`. Client-specific plugin installation commands apply only to that client;
Codex follows the same tool contracts and this skill's production workflow.

- Remove a link or effect with `update_node`, unsetProperties set to ["href", "shadow"], and
  an empty patch object. Optional crop, gradient and group membership can also be unset. Never send null
  as deletion, unset a required field, or patch and unset the same field.
- Group with `group_nodes`; use `move_nodes` for a shared delta and `ungroup_nodes` to detach
  membership. `duplicate_nodes` accepts explicit nodeIds, a fresh idPrefix and dx/dy; it creates
  fresh groups and detaches reusable/component metadata like Canvas duplicate-in-place. Include
  complete groups. `align_nodes` and `distribute_nodes` use Canvas bounds and rounding; managed
  Auto Layout children must be laid out using `set_auto_layout`. Include complete touched Auto
  Layout trees for group, ungroup, move or duplicate. Locked nodes must first be unlocked; use
  component instance operations for linked component edits.
- Set a shared group URL by updating every member's `href` in one `apply_email_batch`.
  For ordinary nodes use `update_node`; clear optional links with unsetProperties set to ["href"].
  For component members use `set_instance_override` with `sectionId`, `instanceId`,
  `sourceElementId`, and a patch containing the new href. To clear a component member's
  link persistently, set href to an empty string in the patch. This preserves unrelated overrides; do not reset
  or detach the whole instance. Use one operation per member, including all selected group members.
  Each batch entry is the operation object itself, for example:

  ```json
  {"type":"set_instance_override","sectionId":"frame","instanceId":"card-instance","sourceElementId":"caption","patch":{"href":""}}
  ```
- To use a catalog block, pass its returned definition to `upsert_reusable_block`, then call
  `instantiate_reusable_block` with definitionId, fresh instanceId and x/y. Upserting an existing
  definition updates complete linked instances at their existing origins; structural changes
  require detaching incompatible instances first with `detach_reusable_block`.
- To use a catalog text style, pass its definition to `upsert_text_style`, then `bind_text_style`.
  Use `set_text_style_overrides`, `reset_text_style_overrides`, and `detach_text_style` for local
  edits. A style upsert propagates to bound nodes and preserves their explicit overrides. These
  document operations do not change the shared catalog; save that separately when requested.
- `upsert_saved_style` and `apply_saved_style` handle document-local per-kind presets.
  `upsert_custom_font` registers the validated font source; reference it with a safe fallback stack.
- Export through `export_email_document` with emailId, exactly one stored revisionId or versionId,
  and format png, pdf, svg, pen or figma_json. For a named region, supply regionId and png/svg;
  the region must permit that format. Use the returned signed downloadUrl before expiresAt and
  inspect fidelity warnings. For delivery HTML use `compile_email_wip`'s canonical previewUrl.
  For recipient preview imagery use `get_email_preview_image` after compile with its revisionId.

Capability canvasActions maps document actions to these commands. Pan, zoom, selection,
clipboard and panel opening are transient client controls, not persisted email operations.

1. Run ALL image work before you touch the document: `create_image_edit_job` to cut packshots
   out of their background when no CUTOUT motif exists, `create_image_generation_job` for hero
   scenes and glow art, prompted with the pack's palette and `imageryStyle`. For every new
   generation or edit call, supply `assetName`: a concise descriptive library name you choose
   for the result, such as “Amber bottle on linen” or “Citrus serum transparent cutout” (3–100
   characters). Describe its subject and visual treatment; never copy the prompt, a job ID,
   or a generic filename. New requests require at least two words; historical queued jobs remain valid.
   For an email placement, also supply targetSize with width and height from the planned slot's CSS
   dimensions. For an opaque banner, include `targetSize.backgroundColor` as the actual planned
   slot's solid #RRGGBB background, never a guessed color. Delivery then pads opaque images in
   that color and compresses them as JPEG when smaller. Genuine cutouts retain transparency;
   without a known solid background, ratio mismatches keep transparent padding. Inspect the result before placement;
   explicit user-directed crops remain an editor decision.
   Poll `get_image_job`;
   `get_completed_image_asset` returns the public `url` an email image element uses. Image
   generation runs through Mayland so the organization's configured model, its policy and its
   audit trail all apply. Never call an image provider directly. When a cutout job fails with
   `IMAGE_EDIT_UNFAITHFUL` the model redrew the packaging: use the original packshot on a light
   card instead of retrying blindly.
2. `create_email` with the brand, the campaign the user picked in Step 0, the title and the
   brief. Omitting the campaign drops the mail onto the brand's Unassigned board, which is a
   fallback and not a decision you are allowed to make for the user. Leave `copyRevisionIds`,
   `referenceEmailIds` and `campaignGoalId` out: the context pack's stored selection binds
   automatically, and an explicitly passed set is only accepted when it matches the pack
   exactly.
3. `acquire_email_lock` before mutating, and heartbeat it while you work.
4. `compose_email_from_plan` is the floor, not the fallback: hand it the palette roles from
   `designTokens.colors`, the brand fonts, one transition, one headline style, the furniture,
   and the block list with variants, with the finished image URLs bound to their slots. Band
   rhythm, crest transitions and the hero composition come out of it by construction. It
   replaces the whole document, so compose FIRST: a recompose regenerates element ids and
   orphans every tweak made since. Bind `compose_email_from_plan` to the BRAND context pack:
   the brand profile in that pack drives the typography defaults, while product packs serve
   the copy and product tools.

   Before composing, check the Brand Context Pack: its `brand.facts` is required (a product
   pack alone is insufficient). Missing displayFont or designDna is optional: tell the user
   which explicit plan fonts/design choices will be used, or which standard defaults remain,
   before starting the compose. Do not invent missing brand facts. The run-details export
   preserves the actual plan, brand context and server release for future attempts.

   Every new compose must include `agentInput`: `userPrompt` (the original production request),
   `productionInstruction` (the effective instruction you used), `promptVersion` (your instruction
   revision), `pluginVersion`, `model`, `provider`, `generationSettings`, `documentInputs`
   (names and exact text of any additional documents used), `jobIds` (all image/research jobs
   used for this production, including failed/retried attempts), and `unavailableInputs`.
   When starting any image or research job for an existing email, always pass `emailRun`
   with its `emailId` and `agentRunId`. The server verifies ownership and records that link
   immediately after enqueue, so failures before the first compose remain visible in Run details.
   Omit this binding only for standalone brand research/assets before an email exists.
   Use null for unavailable model/provider/settings/plugin version and name every unavailable
   effective input. Never guess your model, expose credentials, or claim to know hidden host
   instructions. Only include the production request and authorized source documents, not unrelated
   chat history. This contract records disclosed inputs; it is not an exact replay of Claude or Codex.

   For a requested recorded-plan reproduction, read the source email's run protocol and call
   `compose_email_from_plan` with `replaySource` containing the source `emailId` and `requestId` instead of `plan`.
   Acquire the target email's normal lock/run and use its current `expectedWipRevision`, a fresh
   idempotency key and the same effective Brand Context Pack content. The server loads the recorded
   plan and disclosed agent inputs, checks its version and context hash, then uses the normal
   compose/receipt path. If context or version changed or the snapshot is incomplete, report the
   explicit mismatch; do not describe a new generation as reproduction. An uncertain replay retry
   uses the same idempotency key. Compare two members' emails with
   /api/emails/{emailId}/run-protocol?format=json&compareEmailId={otherEmailId} in the same organization.

   When a compose call dies at the transport (timeout, dropped connection), call it AGAIN with
   the SAME idempotency key: the gateway either replays the recorded result or completes the
   write, and a fresh key would only conflict. What you must never do is give up on the composer
   and assemble the document by hand with `apply_email_batch`: a hand-built document loses the
   band rhythm, the transitions, the melt and the palette guards, and ships as a visibly weaker
   mail. If compose still fails after retries, stop and report the failure instead of building
   around it.

   Five plan-level fields set the register of the whole mail and are easy to miss, because the
   mail still compiles without them and simply comes out in the default:

   | Field | Values | What it decides |
   |---|---|---|
   | `typography` | centered, editorial | Whether headings, logo and buttons are centred or set flush left. Editorial is the modern magazine register. Not to be confused with `designTokens.typography` in the brand pack, which names fonts. |
   | `density` | compact, regular, airy | Scales the vertical rhythm. Compact for retail, airy for editorial. |
   | `buttonShape` | rect, rounded, pill | Read it from the brand form tokens, never pick a house default. |
   | `buttonFill` | filled, outline | Outline keeps ink on the ground instead of a solid block. |
   | `tileStyle` | Brand form token | The treatment of the tiles in the grids. |

   Every block reads its own content keys and silently draws nothing for a key it does not
   know, so a hero that looks right in the plan can compile to an empty band with a lone
   button. Spell them exactly:

   | Block | Keys it reads |
   |---|---|
   | brand_hero, variant impact | `pill`, `kicker`, `punchline`, `punchline2`, `sub`, `trustLine`, `cta` |
   | brand_hero, variant full_bleed | `pill`, `kicker`, `punchline`, `punchline2`, `sub`, `trustLine`, `cta`, `logoCapsule` |
   | brand_hero, variant editorial_split, classic | `eyebrow`, `headline`, `subhead`, `cta`, `logoCapsule` |
   | brand_hero, variant statement | `eyebrow`, `headline`, `subhead`, `cta` |
   | story_intro, story_photo | `headline`, `body`, plus `eyebrow` or `signature` |
   | feature_education | `eyebrow`, `headline`, `body`, `bullets`, `cta` |
   | icon_grid | `headline`, `items` with `value` as the tile line and `label` as its caption |
   | timeline | `headline`, `steps` with `headline` and `body` |
   | stat_row | `stats` with `value` and `label` |
   | data_viz | `headline`, `bars` with `value` as TEXT and `height` as a 0..1 fraction, or variant threshold with `rows` |
   | vs_duel | `headline`, `leftTitle`, `left`, `rightTitle`, `right` |
   | annotated_product | `headline`, `callouts` with `label`, plus `imageSlot` |
   | review_panel | `quote`, `author`, `source` |
   | cta_band | `headline`, `subhead`, `cta` |
   | footer | `navLinks`, `address`, `finePrint`, plus the brand `furniture` |

   Most blocks come in more than one shape, and a block sent without a `variant` takes the first
   one every time, which is how a whole campaign ends up in one register. Choose it:

   | Block | Variants |
   |---|---|
   | brand_hero | classic, impact, full_bleed, statement, editorial_split |
   | story_intro | panel, band |
   | lifestyle_circle | circle, full, side |
   | feature_education | standard, stat, stat_band |
   | product_card | light, band, split |
   | cta_band | band, accent |
   | stat_row | tint, dark |
   | icon_grid | tiles, list |
   | data_viz | bars, threshold |

   The stat variants both promise a figure, not prose: stat sets a short number beside its
   explanation, stat_band gives it the full width on an accent surface. A sentence in that slot
   is rejected.

   A hero with `logoCapsule` set to true draws the brand logo natively in a white rounded capsule
   anchored to the hero photo's top edge, so never build that capsule by hand out of
   `apply_email_batch` shapes. It only works where a cover photo exists to anchor to: the
   full_bleed, editorial_split and classic variants with a scene photo. Impact and statement
   ignore it, and so does a hero whose slot carries a `product_asset` packshot (those are
   contained, and the chip would cover the product).

   A hero draws its scene from its own `imageSlot`, never from `backdrop:hero`: that slot is
   the section background art behind everything. A hero with no `imageSlot` falls back to a
   bare band. An `imageClass` of `product_asset` on the hero slot forces the editorial split,
   which is right for a packshot and wrong for a scene. Carry both key sets on every hero so
   the mail composes whichever variant the builder settles on.
5. Refine with `apply_email_batch` in stages, applied back to back within seconds: first the
   depth pass (rotated badges, offset cards, lift shadows, cutout on top), then accent words and
   copy fixes, then any recipe section the block library does not cover. Use
   `set_document_metadata` for name, subject and language, `update_frame` for frame height,
   name or background, `insert_node`, `update_node`,
   `move_node`, `reorder_nodes`, `set_auto_layout` and `remove_auto_layout`. Use Auto Layout for
   live copy stacks whose height or order may change: pass one `groupId`, the exact ordered
   `nodeIds`, `direction`, `gap`, `paddingX`, `paddingY`, `align`, and the group's `x`/`y` origin.
   For responsive stacks, add `widthMode` as hug or fixed. A fixed layout also accepts `width`,
   `justify` as start, center, end, or space-between and `childWidth` as fixed or fill.
   Horizontal fixed-width layouts may set `wrap` and `rowGap`; wrap cannot be combined with fill.
   It materializes normal email geometry, so do not use it for intentional overlaps or decorative
   compositions. In particular, exclude both nodes of every `linked_shape_text_cta`; full and
   partial CTA-pair selections fail closed. Feed each returned newWipRevision into the next batch, and
   `get_email_wip` when you lost track. Staged batches are also what makes the build watchable
   on the board.
6. `compile_email_wip` and inspect its diagnostics. Repair blocking issues in the source WIP before
   handing the result to the user. Reuse truthful existing asset descriptions; unknown content needs
   an accurate description, not a generic filename or a decorative flag. Checkpoint and compile again.
   `complete_agent_run` requires the exact current WIP's bound artifact with no blocking errors;
   EMAIL_AGENT_DELIVERY_NOT_READY and EMAIL_AGENT_DELIVERY_BLOCKED mean preparation is not finished.
7. `get_email_preview_image` returns the rendered mail as an image. First read the whole preview
   once for flow. Then download the `imageUrl` immediately (the link expires in ten minutes) and
   crop the hero and every section at native resolution, with sips or ImageMagick, and look at
   each crop. A 600 by 4000 preview viewed whole is downsampled and hides exactly the defects a
   client sees first: collisions, clipped lines, type on busy ground, cropped subjects. Never
   approve a mail from metadata alone. If the connected release does not offer the tool yet, say
   plainly that you could not see the result instead of calling it good.
8. Fix what you found, then compile and look again. Only `complete_agent_run` creates a final
   version.

Keep elements inside the frame. An element placed fully outside it is dropped at compile with no
visible error, so check geometry when something you placed does not appear.

For a frosted panel over a photo, place a rounded rect in an rgba of the ground colour over the
image; for a shaped window, a ground-coloured strokeless freeform over the photo. Both keep the
text itself live.

## Before you call it done

- You have looked at the rendered preview image AND at native-resolution crops of the hero and
  every section, not only at the compile result.
- Every band change carries a named transition or a soft fade, and the mail carries at least one
  depth device.
- Kicker, punchline, sub, button and capsule read as separate steps.
- Button text is fully visible and nothing overlaps it.
- No type sits behind product imagery, including word endings.
- Exactly one accent word, in a colour from the brand palette.
- Every text is legible on mobile, body at 16px or more.
- Body contrast at least 4.5:1, headline contrast at least 7:1.
- The first CTA sits within the top 800px.
- Prices and dates are formatted for the brand's language.
- Nothing on the page is a claim the brand kit does not support.
- No `noGo` rule is broken.

## After every review

A correction that stays in the conversation is gone on the next run. Learnings are the channel
that carries design corrections across runs, which makes this step part of the work and not an
afterthought.

1. Read the review in full: `list_client_review_feedback` for a released version, `get_qa_review_status`
   for the QA findings, and whatever the user told you in the conversation.
2. For user-authorized corrections, first save the consolidated prompt iteration as described
   above, then fix the mail, compile and look at the preview again. Client comments read without
   an instruction to adopt them do not authorize prompt changes or a new production iteration.
3. Then call `propose_learning` once for every design decision the review rejected. This is
   mandatory, including when the fix looks obvious to you. `heading` names the decision, `body`
   states the rule so it holds for the next mail instead of describing this one repair, `evidence`
   points at the email, the version and the comment it came from. `type` is BRAND for a rule about
   this brand's design, PRODUCT when it only holds for one product, AGENCY_PLAYBOOK when it holds
   regardless of brand.
4. Rejections of copy, of imagery and of layout all belong here. A learning is proposed, not
   applied: a human approves it, and from then on it reaches every run through
   `list_approved_learnings`. Do not wait for that approval.
5. Leave out typos, broken assets and anything the compiler already catches. Learnings are for
   taste decisions that would otherwise be argued again on the next mail.

`propose_learning` binds to the current context pack, so refresh the pack before proposing when it
has gone stale.

## Write back what you had to work out yourself

The pack supplies the next run's verified brand knowledge; the prompt line separately preserves
the reusable assignment. Whenever the pack left you a gap and you filled it
from another source, sampling the real CTA color out of a reference newsletter's pixels, naming
the display typeface, deriving a register rule, collecting the brand's button imperatives, or
researching a product's regulatory footnote text, that finding MUST be written back before the
mail is done, or the next user rebuilds the same knowledge badly. Facts about the brand or a
product go into the catalog with `upsert_brand_catalog` (palette color with its role explained,
display font, design DNA, button-label pool, product truth, pain points, footnotes in exact
wording). Rules of taste go through `propose_learning`. If you notice the gap but cannot fill it,
name it explicitly in your final summary so a human can. Never finish a session whose best
insights exist only in the conversation.

## Session hygiene

- Always start from a fresh context pack before mutating production content.
- Never assume stale local context is still valid after an interruption.
- Use `/reset` when you switch emails, after a reconnect, or when Mayland reports stale context.
- On `CONTEXT_PACK_STALE`, fetch a fresh context pack and re-read the brand before continuing.
- `complete_agent_run` is the only Claude path that can create a final Email Version.
