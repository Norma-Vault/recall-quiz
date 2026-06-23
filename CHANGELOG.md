# Changelog

All notable changes to recall-quiz. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows [SemVer](https://semver.org/).

## [1.3.1] — 2026-06-11

### Fixed
- Critical: the worked examples marked the correct option inline with a checkmark, which the model copied into delivered quizzes — revealing the answer and defeating retrieval practice. Examples now disclose the answer only in the post-reply explanation; SKILL.md Rule 5 forbids any marker, emphasis, or hint on options in delivered output, and a standing rule in question-design.md keeps contributors from reintroducing it.

### Changed
- Delivery presentation: quizzes now open with a bold label and bold stem with each option on its own line, so the quiz stands out from surrounding prose instead of blending in.
- A one-line note that tappable answer buttons are unavailable on this surface is shown only on the first quiz of a conversation, not repeated thereafter.

### Added
- Eval #25: regression guard asserting no delivered quiz reveals or marks the correct option.

## [1.3.0] — 2026-06-11

### Added
- Six-gate decision policy in SKILL.md (intent → suppression → substance → sufficiency → cadence → checkpoint), run in order on every reply; cadence is now defined canonically in gate 5.
- Insufficient-content branch (gate 4): no quiz when the answer cannot supply plausible distractors from its own material — natural expansion or a one-line note on explicit triggers, silent skip in ambient mode; matching sufficiency test in references/question-design.md.
- Format-override rule: MCQ 4–5 and one-question-per-answer are explicit defaults overridable by user request; answer-first, suppression precedence, only-test-what-was-taught, opt-out, and the focus guard remain invariant.
- Hardened opt-out semantics: resume only on explicit quiz-intent (study-context mentions alone do not re-arm); "skip this one" is question-scoped; repeated skips are a silent soft opt-out.
- Authoring exception: authoring quiz content for others plus a separate explicit self-request yields both behaviors.
- Operational definitions: substantive answer; quiz-item reject list (trivia, caveats, side remarks, the user's own personal details or data, untaught material).
- Authority declarations: SKILL.md is canonical; all four reference files now state subordination explicitly.
- Seven new topical hard negatives (load testing, penetration testing, test coverage, quiz app, practice test results, exam board, taste test); eval suite expanded 14 → 24 covering mixed intent, insufficient content, format overrides, skip-vs-stop, re-enable, authoring-plus-self, mid-task checkpointing, and frustrated-user tone.

### Changed
- README quality claims separated into measured (validator, lint, trigger simulation), specified (behavioral eval conformance spec), and expected (qualitative semantic generalization) — replacing wording that overstated semantic performance as measured.

### Notes
- Hardening informed by an external model review; each finding was independently assessed before adoption.

## [1.2.0] — 2026-06-11

### Added
- `references/trigger-lexicon.md`: 105 trigger phrases across 7 intent families (direct requests, retention intent, sharpness/anti-deskilling, mode activation, ambient opt-in, study context, learning-science jargon), 15 opt-out phrases, suppression cue categories with hard negatives, and explicit precedence rules (suppression > trigger > opt-out).
- Authoring-request suppression: writing quiz/test content for third parties is now an explicit non-trigger.
- Opt-out re-enable path: clean resumption after "quiz me again", with optional re-test of one earlier miss.
- `CHANGELOG.md` and `CONTRIBUTING.md`.

### Changed
- Frontmatter description expanded with high-value trigger phrases while remaining within the 1024-character limit.
- Eval suite expanded from 6 to 14 cases, adding paraphrase triggers, urgency suppression, authoring suppression, topical-mention hard negatives, opt-out re-enable, and miss re-surfacing.

### Quality
- Release tested with: official skill validator; structural lint; and a seeded trigger simulation harness measuring lexical recall on perturbed trigger paraphrases and false-trigger rate on hard negatives under the documented precedence rules.

## [1.1.0] — 2026-06-10

### Changed
- Instruction body slimmed by 54% (≈2,493 → ≈1,148 estimated tokens); always-on metadata reduced 31%; per-quiz exchange format capped (≈105 tokens). Cumulative context cost roughly halved in modeled 20- and 40-turn sessions.

### Added
- Focus guard: on-topic-by-construction quizzing, checkpoint-only firing in multi-step work, close-and-hand-back after grading, no mode bleed into main answers.
- Token budget: capped quiz/grading sizes, ambient cadence of one quiz per 3–4 substantive answers, on-demand-only reference loading.

## [1.0.0] — 2026-06-09

### Added
- Initial release: ANSWER → MINE → ASK → GRADE → REINFORCE loop; distractor-quality question design; sensitivity, transactional, and decline suppressions; instant durable opt-out; session-level spacing and interleaving; references for question design, learning science, and session state; 6-case eval suite; MIT license.
