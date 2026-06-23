# Recall Quiz

**An Agent Skill that turns passive AI answers into active recall.**

> Stop downskilling. After Claude answers your question, it asks you one short multiple-choice question drawn from that answer — then grades it and explains. You keep the convenience of being told *and* get the retention of being tested.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
![Version](https://img.shields.io/badge/version-1.3.1-blue)
![Instruction-only](https://img.shields.io/badge/scripts-none-blue)
![No network](https://img.shields.io/badge/network-none-blue)
![No data sent](https://img.shields.io/badge/data%20sent-none-blue)

---

## Why

Heavy, unstructured AI use offloads thinking — and unpractised skills fade. Recent work links it to measurable declines: a 2025 study (Gerlich, n=666) tied heavier AI reliance to weaker critical thinking via cognitive offloading; a 2025 RCT found AI-assisted learners retained less on a delayed test (≈57.5% vs ≈68.5% at 45 days); and the UK Department for Education's January 2026 GenAI safety standard now expects tools to *actively mitigate cognitive deskilling*.

The fix isn't to use AI less — it's to add back a little of the effort the tool removes. **Retrieval practice** (the "testing effect") is one of the most robust findings in learning science: pulling a fact from memory strengthens it far more than re-reading it. Recall Quiz is retrieval practice in its lightest possible form, riding on top of questions you were already asking.

## What it does

```
ANSWER  →  MINE  →  ASK  →  GRADE  →  REINFORCE
  |          |        |        |          |
 full      pick a    one     check     explain why;
 answer    quiz-     MCQ,     the       remember misses
 first     worthy    4-5      reply     for later
           item      options
```

1. **Answers your question fully** — the quiz is never a gate.
2. **Mines the answer** for one high-value item: an acronym, a distinction, a key number, a definition, a mechanism.
3. **Asks one multiple-choice question** (4–5 options) with *plausible* distractors built from real misconceptions — via tappable buttons where the host supports them, or a clean inline A–D list otherwise. Defaults, not shackles: ask for open-ended questions or several questions and it obliges.
4. **Grades and explains** in one or two sentences — corrective feedback is where the learning happens.
5. **Reinforces over the session** — re-surfaces misses later (spacing + interleaving) and adapts difficulty.

Behavior is governed by a six-gate decision policy run in order on every reply — intent, suppression, substance, sufficiency, cadence, checkpoint — so the quiz fires only when it should: never on sensitive, urgent, transactional, or mid-task content, never on answers too thin to support fair distractors, and never after you've said stop.

## Triggering

The skill recognizes over a hundred trigger phrasings across seven intent families — direct requests ("quiz me", "pop quiz", "test my knowledge"), retention intent ("make it stick", "help me remember this"), sharpness ("keep me sharp", "don't let me deskill"), mode activation ("study mode", "learning mode"), ambient opt-in ("quiz me as we go"), study context ("I'm prepping for my certification"), and learning-science jargon ("active recall", "retrieval practice") — plus 15 opt-out phrasings and explicit suppression cues with documented precedence (suppression > trigger > opt-out). The full lexicon: [`references/trigger-lexicon.md`](references/trigger-lexicon.md).

## How it's different

| | Recall Quiz | Decision-gate skills (e.g. anti-deskilling) | Flashcard / study-mode skills |
|---|---|---|---|
| **When** | *After* the answer | *Before/during* a decision | In a dedicated study session |
| **Mechanism** | Retrieval practice (testing effect) | Preserves decision *agency* | Generates/reviews a deck |
| **Format** | One graded MCQ, 4–5 options | Open question / confirmation | Card stacks, SRS export |
| **Scope** | Any informational answer | Coding decisions | Material you assemble |
| **Keeps you as** | Knowledge-holder | Decision-maker | Studier |

They're complementary, not competing. Recall Quiz is the only one that adds **ambient, post-answer retrieval practice** to ordinary Q&A.

## Install

**Claude Code**
```bash
git clone https://github.com/Norma-Vault/recall-quiz ~/.claude/skills/recall-quiz
```

**Claude.ai** — Settings → Capabilities → Skills → upload `recall-quiz.skill` (from [Releases](https://github.com/Norma-Vault/recall-quiz/releases)).

**Claude API** — upload via the `/v1/skills` endpoint and reference the `skill_id` with the code-execution container.

The Agent Skills format is an open standard, so the same skill also runs on other skills-compatible agents (Cursor, Codex CLI, Gemini CLI, Antigravity, Windsurf, and others).

## Use

> "Explain OAuth, then **quiz me** so it sticks."
> "**Study mode** — I'm prepping for my AWS cert."
> "Walk me through this and **make it stick**."
> "**Quiz me as we go** for the rest of this session."

To stop: "stop", "pause", "enough", "not now", "no more quizzes". It ends quietly and won't re-pitch; only an explicit "quiz me again" resumes it. "Skip this one" skips just the current question.

## What's inside

```
recall-quiz/
├── SKILL.md                      # the authoritative policy: loop, decision gates, rules, budgets
├── CHANGELOG.md                  # version history
├── CONTRIBUTING.md               # contribution standards and design invariants
├── LICENSE                       # MIT
├── README.md
├── references/
│   ├── trigger-lexicon.md        # 105 trigger phrases, opt-outs, suppression cues, precedence
│   ├── question-design.md        # distractor patterns, sufficiency test, difficulty ladder, examples
│   ├── learning-science.md       # the testing effect, spacing, the deskilling evidence
│   └── session-state.md          # in-session streaks, spacing, interleaving
└── evals/
    └── evals.json                # 24 behavioral test cases (incl. mixed-intent and hard negatives)
```

SKILL.md is canonical; every reference file declares itself subordinate to it.

## Performance & focus

Two fair questions, measured (token figures are tokenizer estimates, ±10%):

**Does it cost tokens?** Marginally, by design. Always-on metadata is ~214 tokens (~0.1% of a 200k window). The instruction body (~1,650 tokens) loads only when quizzing actually triggers. Each quiz exchange is capped at ~105 tokens — three quizzes occupy ~1% of a typical 30k-token session — and ambient cadence defaults to one quiz per 3–4 substantive answers. References load only on demand. The counterfactual is the expensive path: a fact you don't retain is a question you re-ask in a future session.

**Does it dilute session focus?** It's engineered not to. Questions are mined exclusively from the session's own answers — on-topic by construction, never imported trivia. The decision policy defers quizzes to natural checkpoints (never mid-task or mid-chain), the reply returns to the main thread in the same message after grading, and "mode bleed" is forbidden — quizzing may never change the style, depth, or rigor of main answers. Benchmarks show *irrelevant* context is what degrades agent accuracy; a 105-token elaboration of the answer just given is the opposite of irrelevant.

## Quality assurance

Three kinds of quality claims, kept deliberately separate:

1. **Measured — format and lexical testing.** Each release passes the official Agent Skills validator, a structural lint of 156 automated checks (link integrity in both directions, MCQ format on every example, banned-string and placeholder scans, version consistency, eval-suite schema, token budget), and a seeded trigger simulation: 17,550 generated utterances expanding the lexicon's 105 trigger phrases through prefix/suffix templates with casing, punctuation, and typo perturbations, plus templated hard negatives, scored under the documented precedence rules — **99.3% lexical recall** on trigger paraphrases and **0.00% false-trigger rate** on hard negatives.
2. **Specified — behavioral conformance.** The 24 cases in [`evals/evals.json`](evals/evals.json) define expected conduct for mixed trigger-plus-suppression messages, insufficient-content answers, format overrides, soft vs hard opt-out, re-enable after a durable stop, authoring-plus-self requests, mid-task checkpointing, and frustrated-user tone. They are a conformance specification for model-executed testing, not a measured pass rate.
3. **Expected — semantic generalization.** The model matches trigger *intent*, so paraphrases beyond the lexicon are expected to work better than the lexical proxy measures. That is a qualitative engineering expectation, not a measured guarantee.

## Safety

Instruction-only. **No scripts, no network calls, no data sent, no files written.** Everything happens in the conversation, and the whole skill is auditable in a couple of minutes. It never quizzes you on sensitive or personal content, never mines your own private details as quiz material, and suppresses itself under urgency, emotional load, and mid-task pressure.

## License

MIT — see [LICENSE](LICENSE). Contributions welcome: see [CONTRIBUTING.md](CONTRIBUTING.md).
