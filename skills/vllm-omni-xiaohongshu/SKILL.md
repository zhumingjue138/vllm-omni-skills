---
name: vllm-omni-xiaohongshu
description: Turn vLLM-Omni pull requests, releases, benchmark results, and model updates into Xiaohongshu posts with accurate technical framing and evidence-backed claims. Use when drafting Chinese community updates, launch notes, feature teasers, or creator-friendly summaries from vllm-omni engineering work.
---

# vLLM-Omni Xiaohongshu Content

## Overview

Use this skill to convert engineering changes into publishable Xiaohongshu copy for Chinese-speaking developers and AI creators. Optimize for one clear takeaway, concrete proof, and a tone that is accessible without flattening the technical substance.

## Inputs

Start from source material, not from imagination:

- PR title and body
- merged commit summary or diff summary
- linked issue or user pain point
- benchmark, latency, memory, or quality measurements
- release notes or model documentation when the PR alone is incomplete

If the change touches a specialized subsystem, load the matching technical skill first so the post does not misstate behavior or limitations.

## Workflow

### Step 1: Establish Source Truth

Extract four facts before drafting:

1. What changed
2. Why it matters
3. Who benefits
4. What evidence proves it

If any of these is weak or missing, downgrade the post from a strong launch claim to a smaller progress update.

For source priority, inclusion rules, and red flags, see [references/source-selection.md](references/source-selection.md).

### Step 2: Choose One Angle

Pick one primary angle. Do not combine three stories into one post.

| Angle | Use When | Watch Out For |
|-------|----------|---------------|
| Feature launch | New capability is usable now | Do not imply GA if still experimental |
| Performance win | There are before/after numbers | Do not claim speedup without workload context |
| Deployment simplification | Setup or serving got easier | Show the exact simplification |
| New model support | A model family was added or improved | Name the model and what it unlocks |
| Bugfix story | A painful failure mode is fixed | Include the old failure and regression protection |

### Step 3: Structure the Post

Use this order:

1. Hook title with the outcome
2. Opening lines that state the pain point and the change
3. Three to five short body blocks or bullets
4. A proof section with numbers, commands, or concrete behavior
5. A close that tells readers who should try it or why it matters

Start from [assets/xiaohongshu-template.md](assets/xiaohongshu-template.md) instead of freehand drafting.

### Step 4: Draft in Xiaohongshu Style

- Write in Simplified Chinese by default
- Keep model names, repo paths, flags, API routes, and metrics exact
- Prefer short sentences and concrete nouns over abstract product language
- Keep one core claim per post
- If there is no hard evidence, present the update qualitatively

For tone, title patterns, and hashtag strategy, see [references/xiaohongshu-style.md](references/xiaohongshu-style.md).

### Step 5: Run a Publishing Safety Check

Before finalizing:

- verify every metric against the source
- remove private links, internal branch names, secrets, and roadmap details
- do not claim a PR is released if it is only merged or still under review
- do not write "best", "SOTA", or similar claims without proof
- mention constraints when they materially affect adoption, such as VRAM or hardware limits

## Deliverables

Produce:

- 2-3 title options
- one final post body
- one cover-text suggestion
- 5-8 hashtags
- an optional pinned-comment line for FAQs or repo links

## Common Patterns

- For benchmark-driven updates, lead with the user-visible win, then show the measurement context.
- For model support posts, explain what the model enables before naming implementation details.
- For bugfix posts, describe the failure mode plainly and mention the regression guard if one exists.
- For setup or serving updates, show the new path in one command or one config snippet when possible.

## References

- For source selection and claim safety, see [references/source-selection.md](references/source-selection.md)
- For Xiaohongshu-specific tone and format, see [references/xiaohongshu-style.md](references/xiaohongshu-style.md)
- For the drafting skeleton, use [assets/xiaohongshu-template.md](assets/xiaohongshu-template.md)
