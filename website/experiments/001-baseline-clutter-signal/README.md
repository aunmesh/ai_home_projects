# 001 — Can a stock vision model tell clutter from normal?

**Question:** given a photo of a room, can an off-the-shelf model (no
fine-tuning, no custom rules) produce a clutter signal that roughly agrees
with what Ishita and Asim would say by eye?

**Why this, why now:** everything else in the pipeline — scheduled capture,
day-over-day comparison, phone notifications — is wasted work if the core
detection signal isn't there. This is the cheapest possible test of the
riskiest assumption, before any product code gets written. It also directly
informs episodes 01–02 of the build log (`chores-assistant/`).

## Method

1. **Room:** one room only — the kitchen counter (it's the one both of us
   already complained about, and the one the site copy already promises).
2. **Data:** ~25–30 phone photos taken over 1–2 weeks, across the full range
   from "just cleaned" to "genuinely messy." No staging — real moments.
3. **Ground truth:** Ishita and Asim each independently score every photo
   1–5 for "how messy is this," then reconcile disagreements. This is the
   target the model is being checked against.
4. **Candidates to compare** (same photos, same ground truth):
   - A general-purpose object detector (e.g. YOLO) — score derived from
     object count / density on the counter.
   - A multimodal LLM prompted directly for a 1–5 clutter score with a short
     rubric (e.g. Claude or GPT-4V).
5. **Success criteria** (fixed before looking at results): the better
   candidate's ranking of photos should broadly agree with the human
   ranking — it doesn't need to be exact, it needs to reliably separate
   "tidy" from "messy" and not be fooled by things like a cutting board
   mid-use.

## Data

Raw photos and any model outputs stay local (`experiments/001-.../data/` or
similar), gitignored — only this write-up and any small scoring scripts get
committed.

## Result

_Not run yet._

## Verdict

_Pending._ Whichever approach wins becomes the detection method carried into
the real capture → detect pipeline (episode 02); if neither clears the bar,
that's the finding — and the next experiment is picking a different signal
(e.g. change-detection between frames instead of absolute scoring).
