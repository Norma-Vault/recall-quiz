# Learning Science

SKILL.md is the authoritative policy; this file holds the evidence and rationale behind it.

Why a ten-second multiple-choice question after an answer is worth the friction. Read this if asked to justify the approach, or to explain *why* a quiz helps.

## The problem this addresses: cognitive offloading and deskilling

When a tool does the thinking, the user stops practising the thinking — and unpractised skills fade. This is **cognitive offloading**, and a growing body of work links heavy, unstructured AI use to measurable declines in independent reasoning.

- A 2025 mixed-methods study by Gerlich (n = 666) found heavier reliance on AI tools associated with lower critical-thinking scores, with cognitive offloading as the mediating mechanism — the author describes a drift toward "cognitive laziness."
- A 2025 randomised controlled trial reported by Barcaui found learners who used AI assistance scored lower on a delayed retention test (about 57.5%) than those who did not (about 68.5%) measured 45 days later — exposure without retrieval did not stick.
- The UK Department for Education's GenAI product-safety standards (updated January 2026) now expect tools used in schools to make every effort to mitigate cognitive deskilling — including not handing over final answers by default and tracking when learners offload thinking. The direction of regulation is toward *guarded* assistance, not raw answer-vending.

The takeaway is not "AI harms cognition" — it's that *passive* consumption does. The fix is to reintroduce a small amount of the effort the tool removed.

## The mechanism this uses: the testing effect (retrieval practice)

Retrieving information from memory strengthens that memory far more than re-reading the same information. This is one of the most robust findings in the science of learning (the "testing effect", established by Roediger and Karpicke and replicated widely). A short quiz is retrieval practice in its lightest possible form: it forces the user to *produce* the fact rather than merely *recognise* that they saw it.

Crucially, the quiz comes **after** the answer, so it adds retrieval on top of comprehension rather than replacing the answer with a riddle. The user keeps the speed of being told and gains the durability of being tested.

## Three principles that shape the design

1. **Desirable difficulties (Bjork).** Learning that feels harder in the moment often produces better retention. A question that takes a few seconds of genuine effort to answer is doing more than one that's trivially obvious — but it must remain *answerable from what was just taught*, or it becomes a discouraging gotcha rather than a desirable difficulty.

2. **Spacing and interleaving.** Re-asking a previously-missed item a few turns later, mixed in with other material, beats asking it twice in a row. The spacing effect (Ebbinghaus onward) and interleaving research both support distributing and mixing retrieval rather than massing it.

3. **Immediate corrective feedback.** Feedback delivered right after a miss is where much of the gain occurs. Telling the user the correct answer *and why their choice was wrong* corrects the misconception while it's still active. Feedback withheld or vague wastes the rep.

## Why multiple choice (and why distractors matter)

Multiple choice is fast, low-friction, and tappable — ideal for an ambient layer that must not feel like homework. Its weakness is that bad distractors let users pass by elimination without knowing the material. The research-backed remedy is **plausible distractors built from real misconceptions and adjacent concepts**, which is why `references/question-design.md` spends most of its length on distractor construction. Good distractors convert a recognition task into a discrimination task, which is most of the learning value of MCQs.

## What this skill deliberately is *not*

- **Not a Socratic answer-withholder.** Some "learning mode" designs refuse to give the answer and only ask questions. That suits formal study but is hostile in everyday work. This skill always answers first.
- **Not a flashcard generator or a study app.** Those require the user to assemble material and sit a session. This rides on questions the user was already asking.
- **Not a decision-gate.** Tools that pause before a decision to make the human choose (preserving *agency*) solve a different problem — keeping the human as decision-maker. This skill keeps the human as *knowledge-holder* via retrieval. The two are complementary.

## One-line summary

Passive AI use offloads thinking and erodes retention; a brief, well-built retrieval question after the answer reintroduces the effort that makes knowledge stick, at almost no cost to convenience.
