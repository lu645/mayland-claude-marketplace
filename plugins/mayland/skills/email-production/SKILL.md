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

1. `list_campaigns` for the brand, and settle where this mail belongs before anything else.
   Every email lives on exactly one campaign board. Show the user the boards you found and ask
   which one this mail belongs to. If none of them fits, offer to open a new board and call
   `create_campaign` only after the user names it. Never guess the board and never silently let
   the mail fall into Unassigned. A campaign is a board that holds emails, which is a different
   thing from a campaign goal: goals are reusable briefing intents and hold nothing.
2. `get_brand_context` for a fresh context pack. Re-read it after any interruption.
3. `list_products` and `get_product_context` for the products the mail actually promotes.
4. `list_reference_emails`, then `get_reference_email` for the ones that match the occasion, and
   open every reference image before you build. See the reference section below.
5. `list_approved_learnings` for what this brand has already agreed to. These carry the design
   corrections earlier reviews produced and they bind exactly like the profile does.

Settle the campaign before you mint the pack. A pack goes stale while you talk, and the board
question is a conversation with the user, not a lookup.

Read the brand profile as a design brief, not as decoration:

- `designTokens.colors` hands you the palette already sorted into roles: `bg` and `surface` for
  grounds, `band` with `onBand` for the full-width bands, `ink` and `muted` for type, `accent`
  with `accentInk` for the buttons and the signal moments. Use the roles rather than picking
  from `palette` by eye, and keep the accent for what should be loud. `accentInk` is the only
  colour that goes on top of the accent.
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

Reference emails are the calibre bar, and reaching it visually is the job. Study one until you can
name why it reads well, then build that same reading experience with this brand's own material.

**Open the reference image before you build anything.** Most references are captures of a sent
mail, so `plainText` and `headings` come back empty and every bit of craft sits in the picture:
download each `imageUrls` entry and read it as an image. A reference you have not looked at teaches
you nothing, and building from its title and tags alone is how mails end up generic. While you look
at it, name for yourself the band count down the page, where the density changes, which modules
repeat, how far the type sizes sit apart, and how the button is treated. Those are the numbers you
build against, and `layoutSignature` on the sibling mails is what you compare them to.

Take the craft: the layout system and its column logic, the rhythm of the bands down the page and
where they change density, the module vocabulary the mail draws from, the type hierarchy and how
far the sizes are apart, the button treatment, and the way the page breathes between blocks.

Leave everything that belongs to the mail it was made for: its copy, its offers, its prices,
percentages and other numbers, its images and its brand marks. Those are not craft, they are that
sender's content, and none of it is true for this brand unless the brand kit says so.

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
| Spacing kicker to punch | 14 |
| Spacing punch to punch | 5 |
| Spacing stack to sub | 9 or more |

Autoscale: make the punchline as large as the column allows, shrink in 8% steps if it displaces
the sub, and stop at the floor. Multi-line headlines never sit at 100% line height, use 110% or
more. Single-line punchlines may use 100-104%.

Corner radius, button shape and letter spacing are brand properties. Read them from the profile
rather than choosing a house default.

## The element vocabulary

`insert_node` accepts four kinds, and each carries more than the obvious fields. The schema is
loose: a misspelled field is stored and silently ignored, so spell exactly.

- Text: `text`, `tag` (h1, h2 or p), `color`, `size`, `weight`, `align`, `lh`, `ls`, `italic`,
  `underline`, `transform` for casing, `valign`, and `accentColor` for the accent runs below.
- Button: `label`, `href`, `fill`, `color`, `radius`, `size`, `weight`, `letterSpacing`, `font`.
- Image: `src`, `alt`, `label`, `fit` (cover, contain or fill), `radius`, and an optional `crop`
  region in source fractions.
- Shape: `shape` is one of rect, rounded, circle, ellipse, line, triangle, diamond, pentagon,
  hexagon, star, arrow or freeform. `fill`, `radius`, `opacity` 0..1, `stroke` with `strokeW`
  and `dash`, an optional `gradient` of `{from, to, angle}` in CSS degrees, and for freeform a
  `path` of SVG data in a 0..100 viewBox that scales with the element box.
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
| step | M0,100 L0,55 L20,55 L20,30 L55,30 L55,60 L80,60 L80,38 L100,38 L100,100 Z |

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

Transition, then two to four sections drawn from a varied library: alternating image and text
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

1. Run ALL image work before you touch the document: `create_image_edit_job` to cut packshots
   out of their background when no CUTOUT motif exists, `create_image_generation_job` for hero
   scenes and glow art, prompted with the pack's palette and `imageryStyle`. Poll `get_image_job`;
   `get_completed_image_asset` returns the public `url` an email image element uses. Image
   generation runs through Mayland so the organization's configured model, its policy and its
   audit trail all apply. Never call an image provider directly.
2. `create_email` with the brand, the campaign the user picked in Step 0, the title and the
   brief. Omitting the campaign drops the mail onto the brand's Unassigned board, which is a
   fallback and not a decision you are allowed to make for the user.
3. `acquire_email_lock` before mutating, and heartbeat it while you work.
4. `compose_email_from_plan` is the floor, not the fallback: hand it the palette roles from
   `designTokens.colors`, the brand fonts, one transition, one headline style, the furniture,
   and the block list with variants, with the finished image URLs bound to their slots. Band
   rhythm, crest transitions and the hero composition come out of it by construction. It
   replaces the whole document, so compose FIRST: a recompose regenerates element ids and
   orphans every tweak made since.
5. Refine with `apply_email_batch` in stages, applied back to back within seconds: first the
   depth pass (rotated badges, offset cards, lift shadows, cutout on top), then accent words and
   copy fixes, then any recipe section the block library does not cover. Use
   `set_document_metadata` for name, subject and language, `insert_node`, `update_node`,
   `move_node` and `reorder_nodes`. Feed each returned newWipRevision into the next batch, and
   `get_email_wip` when you lost track. Staged batches are also what makes the build watchable
   on the board.
6. `compile_email_wip` and read every warning it returns. Warnings are the build talking to you.
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
2. Fix the mail first, then compile and look at the preview again.
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

## Session hygiene

- Always start from a fresh context pack before mutating production content.
- Never assume stale local context is still valid after an interruption.
- Use `/reset` when you switch emails, after a reconnect, or when Mayland reports stale context.
- On `CONTEXT_PACK_STALE`, fetch a fresh context pack and re-read the brand before continuing.
- `complete_agent_run` is the only Claude path that can create a final Email Version.
