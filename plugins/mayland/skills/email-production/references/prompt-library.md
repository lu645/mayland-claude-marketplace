# Prompt library

Load this reference only when saving, revising, or explicitly reusing a prompt. A new commission starts from the current request; never retrieve an old prompt as an implicit creative recipe. A historical source may be resolved and reused only when the user selected it. Its visual material still requires exact customer approval before it can be inspiration.

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

In a new compose or the first free-node `apply_email_batch`, explicitly disclose the original
`rawAssignment` as `agentInput.userPrompt` and
the effective concrete `preparedExecutionIntent` as `agentInput.productionInstruction`, alongside
the existing version/model/document disclosures. Keep later confirmed corrections in the effective
instruction, not as a fabricated replacement of the user's original request. No credentials,
unrelated conversation, hidden host instructions or fabricated model settings belong in either.
Include updated disclosures when substantive creative instructions change; ordinary technical
edits do not need another identical disclosure. Both build paths record supplied agent inputs.
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
unambiguous target. User-selected source-prompt, brand, product, eligible reference and approved-Learning lookups may
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
