# Creative review

Run this after the warning repair and Mayland Score checks and before `complete_agent_run`.
The technical checks prove the email works; this review asks whether a customer would be
impressed by it at first sight. It asks questions about the result. It does not prescribe a
layout, a section order or an effect, and it applies to every Brand in the same way.

## Evidence

Judge the final revision, not a plan. Inspect `get_email_preview_image` with
renderMode=delivery at 600px and 390px and the editable canvas, with readable detail crops of
every region you judge. Open the bound references again with `get_reference_email`, and the
other emails of the same campaign with `list_emails` for that campaignId and their preview images.
A passing compile, a finished image job or a clean warning list is not an answer to any question.

## Eight questions

Answer each with pass or fail and the crop (x, y, width, height) that shows it.

1. **Brand recognition.** Would someone who knows the Brand's site recognise the email without
   the logo? Check colour roles, display font, the logo treatment and, when the Brand has one,
   its signature motif.
2. **Hierarchy.** Does each screen have one element that clearly leads, and is the reading path
   from it to the action obvious? Is the hero headline set at a display size rather than body
   scale?
3. **Panel consistency.** Do cards, panels and buttons share the Brand's radius, border and shadow
   values, and does every text use one of the campaign's text styles?
4. **Layer placement.** Does any text or button cover a face, a hand or the product? Are overlaps
   deliberate and aligned, is anything cropped, and do edges sit on the spacing grid?
5. **Image variety.** Does each image do a different job (scene, product in use, detail, people,
   proof)? Is the same packshot repeated where a scene or a detail would say more?
6. **Substance.** Does the email use at least one proof element from Brand Intelligence (rating,
   a verbatim review, the story, a trust fact) when the Brand has one? Is every sentence
   specific to this Brand and message, without filler?
7. **Reference ideas.** Is every line of the idea ledger visible in the result, and is the email
   more than a copy of any single reference?
8. **Uniqueness.** Does the email differ visibly from the other emails of the campaign in its
   hero treatment and module mix?

## Repair and record

Repair every failed answer on the canvas, render again and re-answer the questions that failed.
Stop after two repair rounds and report honestly what still fails and why.

Record the final answers in `creativeReview` of `complete_agent_run`: one entry per question
(1 to 8) with pass or fail, the evidence crop (renderMode, viewportWidth, x, y, width, height)
and a note on what you saw or changed. The run does not complete without all eight. The
idea-ledger stays a `documentInputs` entry of your agentInput; the review does not go there.
