# Source Selection

Use this file when you need to decide what material from a PR, release, or model update is safe and useful to turn into a Xiaohongshu post.

## Source Priority

Prefer sources in this order:

1. release notes or public announcement text
2. merged PR title and body
3. linked issue describing the user problem
4. benchmark tables, screenshots, or example outputs
5. commit summaries and diff details
6. model cards or documentation for supporting context

If a higher-priority source contradicts a lower-priority one, trust the higher-priority source.

## What to Extract

| Field | Questions to Answer |
|-------|---------------------|
| change | What capability, behavior, or workflow changed? |
| audience | Who cares about this change right now? |
| outcome | What becomes faster, easier, cheaper, or newly possible? |
| proof | What metric, command, screenshot, or example proves it? |
| limits | What caveat keeps the claim honest? |

## Good Post Sources

Strong candidates:

- measurable performance changes
- newly supported models or modalities
- setup or deployment simplifications
- bug fixes with a clear before/after story
- examples that unblock a real user workflow

Weak candidates:

- internal refactors with no user-visible effect
- naming cleanups
- speculative roadmap items
- churn with no evidence and no visible outcome

## Accuracy Rules

- Do not claim a change is released if it is only on a branch or only in an open PR.
- Do not infer benchmark improvements from code shape alone.
- Do not hide material tradeoffs like hardware limits, memory growth, or changed defaults.
- If a metric lacks workload context, describe the direction of improvement without a hard number.

## Safe Transformations

Allowed:

- compressing a long PR into one user-facing benefit
- translating technical wording into plain-language Chinese
- turning a benchmark table into one headline plus one supporting sentence

Not allowed:

- inventing adoption claims
- inventing quality improvements that were never measured
- implying official endorsement or release timing not stated in source material
- exposing internal issue links, unpublished docs, or security-sensitive details

## Red Flags

Pause and verify before drafting when you see:

- "refactor", "cleanup", or "prep" with no explicit user outcome
- missing benchmark setup for performance claims
- a draft PR or a feature flag that is off by default
- breaking changes without migration notes
- missing tests for a bugfix that will be presented as fully solved
