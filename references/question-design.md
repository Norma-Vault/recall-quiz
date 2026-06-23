# Question Design

SKILL.md is the authoritative policy; this file elaborates question construction and never overrides it.

The quality of a recall quiz lives almost entirely in the **distractors** — the wrong options. A multiple-choice question with one right answer and three obviously-wrong options tests reading, not memory. A question whose wrong options are real misconceptions tests whether the user actually understood. This file gives patterns for building good distractors per item type, a difficulty ladder, and worked examples.

## Table of contents
1. Universal rules
2. Distractor patterns by item type
3. Difficulty ladder
4. Worked examples across domains
5. Anti-patterns to avoid

---

## 1. Universal rules

- **One unambiguously correct option.** If a domain expert could argue two options are right, rewrite.
- **Three to four plausible distractors.** Four or five total options. Fewer than four total makes guessing too easy.
- **Parallel options.** Same grammatical form, similar length, similar specificity. The correct answer must not stand out by being longest, most hedged, or most technical.
- **Self-contained stem.** The user should be able to answer from memory of the answer just given, without re-reading it.
- **Test the centre, not the corner.** Quiz the main idea of the answer, not an incidental aside.
- **Only test what was taught.** Every option's correctness must be decidable from the answer you gave.
- **Sufficiency test (decision policy gate 4).** Before writing the question, confirm the answer's own material can supply the correct option plus three or four plausible near-misses. If you cannot source the distractors from what was taught or directly implied, the item is not quizzable — expand the answer naturally (explicit trigger) or skip silently (ambient); never pad with invented options.

## 2. Distractor patterns by item type

### Acronyms / abbreviations
- **The other expansion.** Use a different real expansion of the same letters (MCP = Model Context Protocol, not "Master Control Program"; DMA = Digital Markets Act, not "Direct Memory Access" — though in the right context the wrong-domain expansion is a great distractor).
- **The sibling acronym.** Swap in a related acronym from the same field (DMA vs DSA; RAG vs CAG vs fine-tuning).
- **Plausible-but-wrong gloss.** Keep the words, change one to subtly alter meaning ("Digital *Marketing* Act").

### Distinctions (X vs Y)
- **The reversal.** State the rule backwards (the classic and most instructive distractor: "A Directive applies directly; a Regulation must be transposed").
- **The merge.** Claim both behave the same ("both must be transposed").
- **The null.** Claim neither has the property in question.

### Numbers / thresholds / dates
- **Off-by-one-tier.** The adjacent plausible value (15% / 21% / 30% / 50%).
- **The transposed digit or order of magnitude.** 1,500 vs 15,000; 2024 vs 2014.
- **The related-but-different figure.** A reduced rate, a gross-vs-net figure, a different jurisdiction's number.

### Definitions
- **The adjacent concept's definition.** Define a neighbouring term instead (define "retrieval" using the definition of "generation").
- **The partial truth.** Correct but incomplete in a way that changes the meaning.
- **The folk definition.** The common informal misunderstanding.

### Mechanism / cause→effect
- **The reversed arrow.** Swap cause and effect.
- **The correlate.** Name something that co-occurs but isn't the cause.
- **The missing step.** Skip the actual mechanism and jump to the outcome.

## 3. Difficulty ladder

Match the rung to the user's apparent expertise and the conversation's register.

1. **Recognition** — "Which of these is X?" Pick the right label. (Beginner / first exposure.)
2. **Discrimination** — "X differs from Y in that…" Tell two close things apart. (Consolidating.)
3. **Application** — "Given situation S, which applies?" Use the concept in a new case. (Comfortable.)
4. **Analysis** — "Why does X produce Y?" or "Which assumption breaks if Z?" (Expert / stress-test.)

A miss should drop the next item on that topic down a rung; a streak should climb one.

## 4. Worked examples across domains

**Tech / AI (discrimination):**
> Fine-tuning and RAG both adapt a model to your domain. The key difference is:
> A) RAG changes the model's weights; fine-tuning retrieves documents at query time
> B) Fine-tuning changes the weights; RAG retrieves documents at query time ✅
> C) Both change the weights
> D) Neither affects what the model produces
>
> *Why B:* fine-tuning bakes knowledge into parameters; RAG leaves parameters alone and supplies context at inference.

**Law / policy (application):**
> A company self-certifies compliance and the obligation takes effect EU-wide on the same date with no national statute. That instrument is most likely a:
> A) Directive
> B) Regulation ✅
> C) Recommendation
> D) Green Paper
>
> *Why B:* direct, uniform applicability with no transposition is the signature of a Regulation.

**Finance (recognition → discrimination):**
> "TOB" on a Belgian brokerage account refers to the tax on:
> A) Dividend income received
> B) Stock-exchange transactions when you buy or sell ✅
> C) Realised capital gains
> D) Account custody fees
>
> *Why B:* the *taxe sur les opérations de bourse* is levied per transaction, distinct from the withholding tax on dividends (roerende voorheffing).

**Science (mechanism):**
> Spaced repetition improves long-term retention mainly because:
> A) Each review is easier than the last
> B) Effortful retrieval after partial forgetting strengthens the memory more than immediate review ✅
> C) It reduces the total number of reviews needed to zero
> D) It replaces understanding with memorisation
>
> *Why B:* the difficulty of recalling something you've started to forget is the "desirable difficulty" that does the work.

## 5. Anti-patterns to avoid

- **Filler options:** "All of the above", "None of the above", joke answers. They give away the question.
- **The giveaway stem:** wording that telegraphs the answer ("Which is the *correct and complete* definition…").
- **Length tell:** the longest, most-qualified option being correct.
- **Outside knowledge:** testing a fact the answer never mentioned.
- **Trick questions:** double negatives, ambiguous scope, two defensible answers.
- **Interrogation:** more than one question when the user only wanted a light check.
