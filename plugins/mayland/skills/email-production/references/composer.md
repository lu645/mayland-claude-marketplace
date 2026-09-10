# Optional legacy composer

Load only after choosing a compatible template for this assignment or when the user explicitly requested a template or recorded-plan reproduction. These blocks are an implementation option, never the default creative direction. Prefer freely designed Mayledit nodes when the blocks constrain the idea. Empty optional fields are valid; do not fill every field merely because it exists.

4. Choose the build path that serves the concept. Use `apply_email_batch` with validated nodes
   and Auto Layout to compose freely, or optionally use `compose_email_from_plan` when its
   blocks fit your design. Library blocks and styles are optional, editable starting points.
   Neither path establishes visual quality by itself. You choose the section order, geometry,
   spacing, typography and image placement.

   Compose replaces the whole document and regenerates element IDs; do not recompose over
   manual refinements without deliberately rebuilding them. A compose requires a BRAND context
   pack with `brand.facts`; product packs supply product facts. Optional missing displayFont
   or designDna does not require another approval: disclose consequential defaults and proceed
   with explicit choices rather than inventing Brand facts.

   Every new compose and the first free-node `apply_email_batch` must include `agentInput`:
   `userPrompt` (the original production request),
   `productionInstruction` (the effective instruction you used), `promptVersion` (your instruction
   revision), `pluginVersion`, `model`, `provider`, `generationSettings`, `documentInputs`
   (names and exact text of any additional documents used), `jobIds` (all image/research jobs
   used for this production, including failed/retried attempts), and `unavailableInputs`.
   Update this disclosure when substantive creative instructions change. Routine geometry repairs,
   polling and unchanged retries do not require another copy of the same disclosure. A batch's
   optional `agentInput` uses the same disclosure contract as compose and is recorded in Run details.
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

   For an uncertain compose transport result, retry the SAME idempotency key and payload to
   resolve whether it committed before making another mutation. A deterministic error needs
   corrected input. Free composition is a normal supported path, but not a way to bypass
   validation, locks, uncertain writes or other safety boundaries.

   The following fields and block keys document the optional composer, not required layout
   anatomy. Choose its options deliberately and inspect the output; omitted values use defaults.

   Submit real values only: no placeholder font data, incomplete Base64 chunks or empty palette
   keys. A schema rejection identifies an invalid request; correct the reported field against
   the current tool schema instead of inventing aliases or working around validation.

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
   | product_card | `productName`, `tagline`, `body`, `price`, `productUrl`, `cta`, `chips`; the title is not `headline` |
   | lifestyle_circle | `captionHeadline`, `captionBody`; not `headline` or `body` |
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

   A hero with `logoCapsule` set to true draws the brand logo in a white rounded capsule
   anchored to the hero photo's top edge. Use it only when that treatment suits the design. It only works where a cover photo exists to anchor to: the
   full_bleed, editorial_split and classic variants with a scene photo. Impact and statement
   ignore it, and so does a hero whose slot carries a `product_asset` packshot (those are
   contained, and the chip would cover the product).

   A hero draws its scene from its own `imageSlot`, never from `backdrop:hero`: that slot is
   the section background art behind everything. A hero with no `imageSlot` falls back to a
   bare band. An `imageClass` of `product_asset` on the hero slot forces the editorial split,
   which is right for a packshot and wrong for a scene. Inspect the actual chosen variant and supply the corresponding keys; do not duplicate
   headlines merely to fill multiple slots.
