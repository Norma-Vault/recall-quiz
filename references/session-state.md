# Session State

SKILL.md is the authoritative policy; this file elaborates session mechanics and never overrides it. Cadence is defined canonically in SKILL.md's decision policy (gate 5).

A lightweight scheme for running an ongoing quiz session inside a single conversation, without persisting anything to disk. Hold this in working memory only.

## What to track

Keep a small mental ledger of items you've quizzed this session. For each item, note roughly:

- **topic** — the subject area (e.g. "EU instruments", "RAG", "Belgian dividend tax")
- **item** — the specific thing tested (e.g. "Regulation vs Directive")
- **result** — hit / miss / skipped
- **last asked** — how many turns ago
- **rung** — difficulty level last used (recognition / discrimination / application / analysis)

You don't need a literal table in the output; just carry enough to make the next three decisions well.

## Decision 1 — should a missed item come back?

Yes, after a gap. Re-surface a miss a few turns later, reworded so it tests the concept rather than memory of the option letters. Mix it among new material (interleaving) rather than asking it again immediately. If the user gets it on the second pass, consider it consolidated and let it rest longer.

## Decision 2 — what difficulty next?

- Miss → next item on that topic drops one rung or adds scaffolding.
- Hit → hold or climb one rung.
- Two hits in a row on a topic → climb, or move on; don't grind a mastered point.

## Decision 3 — score or no score?

Offer a running tally only if the user responds well to it. Some are motivated by "4/5 so far"; others find it stressful or competitive in an unhelpful way. Default to *no* visible score unless the user keeps one going or asks for it. Never frame a low score as failure — it's information about what to revisit.

## Pacing

- One question per answer by default.
- Don't quiz on every single message in a long exchange; let some answers pass clean. Roughly: quiz when there's something genuinely worth retaining, skip when there isn't.
- If the user goes quiet on the quizzes (stops answering them), stop offering them. Silence is a soft "no".

## Ending a session

When the user opts out ("stop", "pause", "enough", "not now", "no more quizzes"), stop cleanly and don't re-pitch. Resume only on explicit quiz-intent (a direct request or mode phrase) — a study-context mention alone does not re-arm. On "ok quiz me again", resume — and you may briefly re-test an earlier miss to reopen the loop.

## No persistence

Do not write files, set reminders, or store anything beyond the current conversation. If a user wants durable spaced repetition across days, that's a different tool (e.g. an Anki export) — say so rather than pretending to remember between sessions.
