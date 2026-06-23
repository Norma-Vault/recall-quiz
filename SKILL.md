---
name: recall-quiz
description: Active recall layer. After giving a substantive answer, ask one compact multiple-choice question (4-5 options) mined from that answer, then grade it and explain. Use whenever the user asks to be quizzed or tested or wants to retain material — quiz me, test me, pop quiz, test my knowledge, check my understanding, drill me, help me remember this, make it stick, keep me sharp, don't let me deskill, active recall, learning mode, study mode, quiz mode — or is studying for an exam or certification, and as an ongoing layer once the user opts into being quizzed as they go; references/trigger-lexicon.md holds the full trigger families. Counters cognitive offloading and skill atrophy from passive AI use. Always answer first and never gate the answer; one question per answer; never on sensitive, urgent, or transactional content; stop instantly and durably on stop, pause, enough, not now, or no more quizzes.
license: MIT
metadata:
  version: 1.3.1
  author: Norma Vault
---

# Recall Quiz

Passive AI answers offload thinking; retrieval makes it stick (the testing effect). After a real answer, pose one compact multiple-choice question drawn from that answer, grade it, and explain in a sentence — the user keeps the speed of being told and gains the retention of being tested.

**Loop:** ANSWER → MINE → ASK → GRADE → REINFORCE. Never reorder it.

## Decision policy

Run these gates in order on every reply. A quiz happens only if all six pass.

1. **Intent.** Is the user asking for *their own* knowledge to be exercised — any paraphrase of the trigger families in `references/trigger-lexicon.md` — or is ambient mode armed, or is the user unmistakably in a learning posture? If none, stop: no quiz.
2. **Suppression.** Do any cues apply: urgency or time pressure; emotional, personal, or sensitive load; a purely transactional task (reformat, translate, run or fix code, simple lookup); authoring-for-others; or mid-task interruption risk? Suppression always beats triggers, silently — explain only if the user asks why. A request to author quiz or test content for third parties is an ordinary task, not a trigger, unless the user separately and explicitly asks to be quizzed too — then do both.
3. **Substance.** Is the answer substantive — does it teach at least one concept, distinction, definition, mechanism, threshold, or process step? Pure lookups, reformats, translations, and one-line clarifications are not substantive. If not, no quiz.
4. **Sufficiency.** Can plausible distractors be sourced from the answer's own material — the correct item plus near-misses actually taught or directly implied? If not: on an explicit trigger, either naturally expand the answer so a fair question exists, or say in one line that there isn't enough material yet for a useful question; in ambient mode, skip silently. Never invent distractors from material the answer didn't teach.
5. **Cadence.** In ambient mode, is a quiz due? Canonical rule (this gate is the single source): one quiz per 3–4 substantive answers by default; the user can ask for more or less. Explicit requests are always due.
6. **Checkpoint.** Is this a natural pause — task complete, plan agreed, or a self-contained explanation finished? Never mid-troubleshooting, mid-execution, or between steps of a workflow; if mid-task, hold the quiz for the next checkpoint.

## Rules

1. **Answer first, fully.** The quiz never gates, teases, or conditions the answer. This is the most important rule.
2. **Mine one item** from the answer just given — the single highest-value learnable thing: an acronym expansion, an X-vs-Y distinction, a key number or threshold, a definition, a mechanism. Central to the answer, not a footnote. Never quiz on trivia, caveats, side remarks, the user's own personal details or data, or anything the answer didn't teach.
3. **One question, 4–5 options, exactly one correct.** The craft is the distractors: real misconceptions and near-misses — the other expansion of the acronym, the reversed rule, the off-by-one number, the adjacent concept. Options parallel in length and form; stem self-contained; no tricks, no "all/none of the above". Calibrate difficulty to the user's level.
4. **Defaults, not shackles.** Multiple-choice with 4–5 options and one question per answer are defaults; an explicit user format request — open-ended, several questions, a different style — overrides them. What never bends: answer-first, suppression precedence, only-test-what-was-taught, opt-out, and the focus guard.
5. **Deliver compactly, and make it stand out.** Use the host's native single-select control if available; otherwise a tight inline block — stem ≤ 25 words, options ≤ 12 words each. The quiz must read as a distinct interactive moment, not blend into prose: open with a bold label (e.g. **Quick check**), bold the question stem, put each option on its own line, and end with "(Reply with a letter, or say skip.)" **Never mark, hint at, bold, or otherwise reveal which option is correct** — no checkmarks, no "(correct)", no emphasis on the right answer. All options must look identical in weight. The correct answer is disclosed only after the user replies (Rule 6). The first time a quiz is delivered in a conversation, add one short line below it noting that tappable answer buttons aren't available here so they can reply with a letter; do not repeat this note on later quizzes. Then stop and wait.
6. **Grade in at most two sentences.** Correct: confirm plus a one-line why. Wrong or skipped: kind correction plus why the right option is right and theirs wasn't — corrective feedback is where the learning happens. Coach, not examiner.

## Focus guard

The quiz must never degrade the main session.

- **On-topic by construction:** quiz only material mined from this session's own answers, never imported topics. The quiz elaborates the thread; it does not fork it.
- **Close and hand back:** after grading, return to the main thread in the same message (e.g. "Back to the migration —"). If the user digs into the quiz topic, answer briefly, then steer back.
- **No mode bleed:** quizzing must not change the style, depth, or rigor of main answers, and must never bias answer content toward "quizzable" material.

## Token budget

Quizzes are cheap; keep them that way.

- Quiz block ≤ ~120 tokens, grading ≤ ~60. No preamble beyond "Quick check:".
- Read reference files only when actually needed (an unusual item type, unclear trigger intent, a request to justify the science, a long session). The body above is sufficient for routine quizzes.

## Session behaviour

Track lightly in working memory — topic, item, hit/miss, difficulty rung. Re-surface a miss a few turns later, reworded (spacing + interleaving). Miss → easier next item on that topic; streak → harder. Show a running score only if the user wants one. No persistence: never write files or pretend to remember across sessions.

**Opt-out is instant and durable:** "stop", "pause", "enough", "not now", "no more quizzes" ends quizzing — no re-pitch, no asking why. Resume only on explicit quiz-intent (a direct request or mode phrase); a study-context mention alone does not re-arm. "Skip this one" skips the current question only; repeated skips are a soft opt-out — stop offering, without comment. On a clean resume ("ok quiz me again"), you may briefly re-test one earlier miss to reopen the loop.

## Example

The answer below is delivered first, in full. Then the quiz — note the options carry **no marking of which is correct**; that is revealed only after the user replies.

After an answer explaining RAG:

> **Quick check** — In a RAG pipeline, what does the **retrieval** step do?
> A) Generates the final answer token by token
> B) Fetches relevant source passages to ground the answer
> C) Fine-tunes the model's weights on your documents
> D) Compresses the prompt to save tokens
>
> (Reply with a letter, or say skip. Tappable buttons aren't available here, so just type the letter.)

User picks C → "Not quite — that's fine-tuning, which changes the weights. The answer is **B**: retrieval leaves the model untouched and pulls in relevant passages at query time." (The one-line platform note is shown only on this first quiz, not on later ones.)

## Reference files

This SKILL.md is the authoritative policy; reference files elaborate it and never override it.

- `references/trigger-lexicon.md` — the full trigger phrase families, opt-out phrases, and suppression cues with precedence rules; read when trigger intent is unclear.
- `references/question-design.md` — distractor patterns per item type, difficulty ladder, sufficiency test, worked examples across domains.
- `references/learning-science.md` — testing effect, spacing, and the deskilling evidence; read when asked to justify the approach.
- `references/session-state.md` — in-session streak, spacing, and interleaving scheme; read for long quiz sessions.

Instruction-only: no scripts, no network calls, no data sent, no files written.
