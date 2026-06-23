# Trigger Lexicon

SKILL.md's decision policy is authoritative; this file is its lexical elaboration and never overrides it.

How recall-quiz decides when to fire. An Agent Skill triggers on *intent*, not on string matching — the model reads meaning, so any paraphrase of the intents below counts. These families enumerate the intent space explicitly: they make triggering reliable, they are the calibration corpus for the project's simulation testing, and they give contributors a single place to extend coverage.

**Precedence (apply in this order):**
1. **Suppression cues** (section I) — if present, do not quiz, even if a trigger phrase also appears as part of an authoring or transactional request.
2. **Trigger phrases** (sections A–G) — fire the loop after the answer.
3. **Opt-out phrases** (section H) — only meaningful once quizzing is active or offered; an explicit positive request ("stop me from deskilling") outranks the bare word "stop" inside it.
4. Neither — answer normally, no quiz.

A bare topical mention of "quiz" or "test" is **not** a request to be quizzed ("the pub quiz is on Friday", "run the test suite", "blood test results"). The user must be asking for *their own* knowledge to be exercised.

## A. Direct requests (30)

- "quiz me"
- "test me"
- "pop quiz"
- "pop quiz me"
- "give me a quiz"
- "give me a pop quiz"
- "quiz me on that"
- "quiz me on this"
- "test me on that"
- "test me on this"
- "test my knowledge"
- "test my understanding"
- "check my understanding"
- "check my knowledge"
- "knowledge check"
- "quick knowledge check"
- "see if I got it"
- "see if I understood"
- "ask me a question about it"
- "ask me questions about this"
- "drill me"
- "drill me on this"
- "grill me"
- "grill me on this"
- "give me a test"
- "run me through a quiz"
- "throw a question at me"
- "fire a question at me"
- "hit me with a question"
- "put me to the test"

## B. Retention intent (20)

- "help me remember this"
- "help me remember that"
- "make it stick"
- "help me make it stick"
- "make sure I remember"
- "make sure this sticks"
- "make sure I actually learn this"
- "I want to retain this"
- "help me retain this"
- "help me memorize this"
- "commit this to memory"
- "so I don't forget"
- "so I won't forget this"
- "I keep forgetting this"
- "I need this to stay with me"
- "burn this into my brain"
- "help me internalize this"
- "lock this in"
- "help me lock this in"
- "I want this to stick"

## C. Sharpness and anti-deskilling (15)

- "keep me sharp"
- "keep my mind sharp"
- "keep my brain active"
- "keep my brain engaged"
- "don't let me deskill"
- "stop me from deskilling"
- "I don't want to deskill"
- "save me from cognitive offloading"
- "stop me from offloading my thinking"
- "I don't want AI to make me lazy"
- "I feel like AI is making me dumber"
- "keep me from getting rusty"
- "don't let my skills atrophy"
- "use it or lose it"
- "keep my critical thinking alive"

## D. Mode activation (12)

- "learning mode"
- "learning mode on"
- "study mode"
- "study mode on"
- "quiz mode"
- "quiz mode on"
- "active recall mode"
- "tutor mode"
- "teacher mode"
- "turn on quizzes"
- "enable quizzing"
- "switch to learning mode"

## E. Ambient opt-in (10)

These arm the skill for the rest of the session, not just one answer.

- "quiz me as we go"
- "test me as we go"
- "quiz me along the way"
- "keep quizzing me"
- "quiz me after every answer"
- "check me as we go"
- "quiz me throughout this session"
- "test me whenever you explain something"
- "keep the quizzes coming"
- "quiz me from now on"

## F. Study context signals (10)

A stated study goal plus informational questions is a learning posture; quiz at natural pauses.

- "I'm studying for an exam"
- "I'm studying for a test"
- "I'm preparing for an exam"
- "I'm prepping for my certification"
- "I'm revising for finals"
- "I'm cramming for a test"
- "preparing for an interview on this"
- "I'm onboarding into this domain and need to learn it"
- "studying this for work"
- "I have an exam on this next week"

## G. Learning-science jargon (8)

- "active recall"
- "retrieval practice"
- "use the testing effect"
- "spaced repetition this"
- "give me retrieval practice"
- "do active recall with me"
- "desirable difficulty please"
- "interleave some questions"

## H. Opt-out phrases (15)

Instant and durable for the session. No re-pitch, no asking why.

- "stop"
- "pause"
- "enough"
- "not now"
- "stop quizzing me"
- "no more quizzes"
- "drop the quizzes"
- "turn off the quizzes"
- "quiz mode off"
- "skip the quiz"
- "skip this one"
- "I'm done with quizzes"
- "maybe later"
- "give the quizzes a rest"
- "that's enough testing"

("skip the quiz" / "skip this one" skip the current question only; repeated consecutive skips are a soft opt-out — stop offering, silently.)

After a durable opt-out, quizzing resumes only on explicit quiz-intent — a family A, D, or E phrase. A study-context mention (family F) alone does not re-arm it.

## I. Suppression cues — do NOT trigger

Suppression beats triggering. Categories with markers:

- **Urgency / time pressure:** "asap", "urgent", "I'm in a meeting", "no time", "right now", "hurry". Deliver the answer with zero extras.
- **Emotional or sensitive load:** grief, health scares, personal crises, conflict ("my cat just died", "I'm really struggling today"). Never gamify these.
- **Transactional tasks:** reformatting, translation, summarizing a document, running or fixing code, simple lookups ("what's the date").
- **Topical mentions, not requests:** the words quiz/test/exam referring to an external artifact or event — "pub quiz", "test suite", "unit test", "A/B test", "test environment", "test drive", "blood test", "my exam went terribly".
- **Authoring requests:** creating quiz or test content for third parties — "write a quiz for my students", "create a pop quiz worksheet for my class", "design a test plan". Do the task; do not quiz the requester.

### Hard negatives (calibration corpus — must never fire)

- "we're hosting a pub quiz on friday, draft the invitation"
- "write a quiz for my students about the water cycle"
- "create a pop quiz worksheet for my class"
- "run the test suite and tell me what fails"
- "the unit tests are failing, fix this bug asap"
- "set up a test environment for the API"
- "design an A/B test for the landing page"
- "what's the date today"
- "reformat this list to use semicolons"
- "translate this paragraph to German"
- "summarize this PDF for me"
- "my cat just died and I want to understand kidney disease"
- "I'm in a meeting, quick — what does CAP stand for"
- "book a test drive for saturday"
- "my exam went terribly and I feel awful"
- "what does my blood test result mean"
- "set up load testing for the checkout flow"
- "schedule the penetration testing window for friday"
- "check the test coverage report for the new module"
- "recommend a quiz app for my phone"
- "my practice test results came back today"
- "the exam board changed the syllabus again"
- "we did a taste test of the new menu items"

## Extending this lexicon

Add phrases to the family they belong to, keep them multi-word and specific (bare "test" or "quiz" would collide with topical mentions), and add a matching hard negative if the new phrase risks collision. Phrases here flow into the project's simulation harness, so additions are automatically covered by the next test run.
