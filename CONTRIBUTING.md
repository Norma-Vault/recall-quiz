# Contributing to recall-quiz

Contributions are welcome — especially new distractor patterns, trigger phrases, and eval cases. A few standards keep the skill trustworthy.

## Non-negotiable design invariants

Pull requests that violate these will not be merged:

1. **Answer-first.** The user's answer is never gated, teased, or conditioned on the quiz.
2. **Instruction-only.** No executable scripts, no network calls, no persistence, no data collection — in the skill *and* in this repository. Auditability is a feature.
3. **One question per answer by default.** Suppressions (sensitive, urgent, transactional, authoring, mid-task) always beat triggers.
4. **Opt-out is instant and durable.** No re-pitching.

## Where things go

| Contribution | File |
|---|---|
| New trigger phrases or hard negatives | `references/trigger-lexicon.md` (keep phrases multi-word and specific; add a hard negative if collision is plausible) |
| New distractor patterns or worked examples | `references/question-design.md` |
| Evidence or learning-science rationale | `references/learning-science.md` |
| Session/spacing behaviour | `references/session-state.md` |
| New behavioural test cases | `evals/evals.json` (next integer id; include both the prompt and the precise expected behaviour) |
| Core loop or decision-policy changes | `SKILL.md` — open an issue first; the body is deliberately token-budgeted, so additions must justify their cost |

## Before opening a PR

1. Validate the skill format: with [Claude Code](https://docs.claude.com), run the skill-creator validator against the repo root, or at minimum confirm: YAML frontmatter parses; `name` is kebab-case; `description` is under 1024 characters with no angle brackets; every `references/*.md` mentioned in `SKILL.md` exists.
2. Check that examples with options (A–E) have exactly one correct answer marked and 4–5 options.
3. Keep token cost in mind: the `SKILL.md` body is deliberately budgeted; bulk content belongs in `references/`.
4. Update `CHANGELOG.md` under an Unreleased heading.

## Style

- Plain, direct prose. Short sentences. No marketing language inside the skill files.
- British or American spelling both accepted; be consistent within a file.
- Quiz examples must be factually correct and self-contained.

## Reporting issues

Open a GitHub issue with: what you asked, what the skill did, what you expected, and (if a triggering problem) the exact phrasing used — trigger reports feed directly into `references/trigger-lexicon.md`.
