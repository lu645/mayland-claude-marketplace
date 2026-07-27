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

## Step 0 - Load the identity first (mandatory)

Before you design anything:

1. `get_brand_context` for a fresh context pack. Re-read it after any interruption.
2. `list_products` and `get_product_context` for the products the mail actually promotes.
3. `list_reference_emails`, then `get_reference_email` for the ones that match the occasion.
4. `list_approved_learnings` for what this brand has already agreed to.

Read the brand profile as a design brief, not as decoration:

- `palette` gives the only colours you may use. Pick one accent and stay with it.
- `displayFont`, `letterSpacing`, `imageryStyle` set the type and picture register.
- `visual` describes the layout system, the module vocabulary and the button treatment.
- `voiceNote` and `tone` set the register and the form of address.
- `nogo` is binding. A mail that breaks one of these is wrong even if it looks good.
- `furniture` holds the footer, the legal links and the service benefits. Use it verbatim.
- Product `truth` and `benefits` are the only claims you may make.

Reference emails set the calibre bar and nothing else. Match their craft level. Never transfer
their copy, their offers, their block order or their brand marks into new work.

Never invent a price, an availability, a discount, a review or a statistic. If the mail needs a
fact the brand kit does not contain, ask for it.

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
| Spacing kicker to punch | 14 |
| Spacing punch to punch | 5 |
| Spacing stack to sub | 9 or more |

Autoscale: make the punchline as large as the column allows, shrink in 8% steps if it displaces
the sub, and stop at the floor. Multi-line headlines never sit at 100% line height, use 110% or
more. Single-line punchlines may use 100-104%.

Corner radius, button shape and letter spacing are brand properties. Read them from the profile
rather than choosing a house default.

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

Transition, then two to four sections drawn from a varied library: alternating image and text
rows, a three-up number band, a stacked stat, an icon promise grid, a framed code box, a
marker-highlighted statement, a two-column comparison, a product picks grid, a single large
review panel, verified buyer cards, a before and after, or a dark icon band. Then a second CTA
carrying the same call as the first, a closing headline with a short sign-off line, and the
brand's own service and footer furniture.

Variation is a hard rule: each mail in a campaign needs a combination of transition, hero
background, headline style and sections that its neighbours do not have.

## Copy

The kicker sets a concrete scene, the punchline pays it off. Provoke the next line. One thought
per sentence, no nested clauses. Lead with the reader's benefit, not with the brand.

Register rules only. Never copy a sample sentence from anywhere, including this file. Write in
the brand's language and form of address. Keep caps for headlines and CTAs, never for body text.
Never use em dashes.

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

1. `create_email` with the brand, the title and the brief. This drafts the document.
2. `acquire_email_lock` before mutating, and heartbeat it while you work.
3. `get_email_wip` to read the current document before every batch.
4. `apply_email_batch` to place work. Use `set_document_metadata` for name, subject and
   language, `insert_node` to add text, button, image and shape elements, `update_node` to patch
   one, `move_node` and `reorder_nodes` for position and depth. Build background bands first,
   then imagery, then type, so stacking order matches what you intend.
5. Generate imagery through `create_image_generation_job` or `create_image_edit_job` and poll
   with `get_image_job`. Image generation runs through Mayland so the organization's configured
   model, its policy and its audit trail all apply. Never call an image provider directly.
6. `compile_email_wip` and read every warning it returns. Warnings are the build talking to you.
7. Look at the compiled result. Do not approve a mail from metadata alone.
8. Fix what you found, then compile again. Only `complete_agent_run` creates a final version.

Keep elements inside the frame. An element placed fully outside it is dropped at compile with no
visible error, so check geometry when something you placed does not appear.

## Before you call it done

- Kicker, punchline, sub, button and capsule read as separate steps.
- Button text is fully visible and nothing overlaps it.
- No type sits behind product imagery, including word endings.
- Exactly one accent word, in a colour from the brand palette.
- Every text is legible on mobile, body at 16px or more.
- Body contrast at least 4.5:1, headline contrast at least 7:1.
- The first CTA sits within the top 800px.
- Prices and dates are formatted for the brand's language.
- Nothing on the page is a claim the brand kit does not support.
- No `nogo` rule is broken.

## Session hygiene

- Always start from a fresh context pack before mutating production content.
- Never assume stale local context is still valid after an interruption.
- Use `/reset` when you switch emails, after a reconnect, or when Mayland reports stale context.
- `complete_agent_run` is the only Claude path that can create a final Email Version.
