---
name: human-writing-style
description: "Avoid AI-flavored English in academic writing; produce prose that reads like a researcher wrote it — CV/Robotics/IP top-journal/conference style (T-PAMI / TIP / CVPR / ICRA)"
metadata:
  migrated-from: "human-writing-style.mdc"
  source-always-apply: "true"
  source-globs: ""
---

## Codex Invocation

Use this skill for every academic prose task in this project. It is the prose baseline; add section or artifact skills when their triggers match.
The source rule had no file glob; Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Human Writing Style for Academic Papers

> **Note**: This skill is the prose baseline for every section; section-specific skills build on top of it.

## Core Principle

Academic prose must read like a knowledgeable researcher wrote it under deadline — precise, varied, and unforced. Avoid AI-flavored patterns that signal machine-generated text. Quality writing achieves this via **three measurable patterns**:

1. **Sentence-shape rotation** — within a paragraph, sentences cycle through (subject + verb + claim), (although/clause + main claim), (consequently/therefore, claim), (specific number + claim).
2. **Hedging without hedging vocabulary** — quality human voice hedges by stating limits concretely (*"performance degrades sharply when the baseline encounters OOD inputs"*) rather than with the adverb *"probably"*.
3. **"By X, Y" causal connectors** — the productive pattern for opening design-rationale paragraphs: *"By incorporating X, Y realizes ..."* — reviewers expect this pattern in Methodology and Related Work limitation paragraphs.

## Rules

### ✅ DO

- **Vary sentence length**: mix short, declarative statements (*"This design adds overhead."*) with longer qualifying clauses (*"Although this design adds overhead, the resulting 1.50 M parameters remain acceptable for edge deployment."*)
- **Open sections with substance**, not a transition phrase like *"In this section, we discuss..."*
- **Use field-standard vocabulary sparingly**: do not reach for buzzwords (*"delve into"*, *"leverage"*, *"tapestry of"*, *"robust solution"*) — say *"use"*, *"build on"*, *"suitable"*
- **Hedge concretely**: replace *"probably will degrade"* with *"PSNR drops to 24.09 dB at ×6"*; replace *"somewhat robust"* with *"robust in-domain, degrades at ×6 out-of-distribution"*
- **Cite the work you build on**; reconnaissance-via-citation is the cheapest signal of originality
- **Use "By X, Y" causal openers** when introducing a design rationale: *"By incorporating scale-prompting information into the feature extraction module, the model realizes adaptive representation."*
- **Open Methodology subsection-ends with "By ..."** sentences — well-structured methodology sections end each major subsection with a causal connective summary

### ❌ DON'T

- Don't open multiple paragraphs with *"In order to"*, *"To understand..."*, or *"Recently, [topic] has..."*
- Don't overuse emphatic adjectives: *"crucial"*, *"vital"*, *"paramount"*, *"revolutionary"* — reviewers flag these as AI-tells
- Don't write apology-phrases (*"I'm sorry, but..."*, *"Unfortunately, we cannot..."*) in a research paper
- Don't over-explain motivation in the abstract; the abstract is not a sales pitch
- Don't use Markdown-style punctuation or emoji in LaTeX body text
- Don't write *"leverage"*, *"delve"*, *"tapestry"*, *"harness the power of"* — these are pure AI-flavor markers

## Sentence-Shape Inventory

When you write a methodology paragraph, deliberately rotate through these shapes:

| Shape | Template | Example |
|-------|----------|---------|
| **Claim + cost** | *"<Claim>. However, this <design choice> brings <cost>."* | *"Existing fixed-scale methods achieve strong results at their target scale. However, they require separate models for each upscaling factor, leading to high computational costs and reduced flexibility in practical applications."* |
| **Although + main** | *"Although/While <limitation>, <subject> <verb> <resolution>."* | *"Although this method offers simplicity and efficiency, it introduces several limitations that hinder its performance under domain shift."* |
| **Consequently/Therefore** | *"Consequently/Therefore, <consequence>."* | *"Consequently, separate models must be trained for each target scale, leading to high computational costs and reduced flexibility in practical applications."* |
| **By + cause** | *"By <verb-ing> <mechanism>, <subject> <achieves> <outcome>."* | *"By employing a learnable distance metric to dynamically compute weighting coefficients, the method enables more flexible and precise feature aggregation."* |
| **Specific number** | *"At <scale>, the method attains the <metric> of <num>, surpassing <baseline> by <num>."* | *"At a scaling factor of ×1.2, the method attains the PSNR/SSIM of 40.50 dB/0.9890, surpassing the baseline by 5.07 dB/0.0141."* |
| **Despite + limit** | *"Despite these promising results, several limitations remain."* | Conclusion pivot — a standard professional close |

## Hedging Without Hedging Vocabulary

| AI-flavored hedge | Better (concrete hedging) |
|-------------------|---------------------------|
| *"Our method probably performs better on most cases."* | *"Our method attains 40.50 dB/0.9890 at ×1.2, surpassing the previous best by 0.17 dB/0.0008."* |
| *"This is somewhat effective."* | *"Robust in-domain; degrades to 24.09 dB at ×6 out-of-distribution."* |
| *"In general, X is more suitable than Y."* | *"X attains 5.07 dB/0.0141 over the baseline at ×1.2; the gain narrows to 0.04 dB at ×6."* |
| *"It is believed that ..."* | *"Empirically, ..."* (when in fact) or *"..., as evidenced by ..."* (when supported by ablations) |

## Examples

### ✅ Good

```markdown
Although high-resolution sensors can alleviate these issues, they
are prohibitively expensive and lack the flexibility to perform
arbitrary-scale zooming. Super-resolution (SR) techniques provide
a promising solution by enhancing spatial quality. However, most
existing SR methods adopt identical feature representations across
all scales, lacking the ability to adaptively adjust features
according to varying requirements, leading to suboptimal results.
```

### ❌ Bad (AI-flavored)

```markdown
In recent years, with the vigorous development of deep learning
and the growing importance of computer vision, the field has
attracted tremendous attention from both academia and industry.
However, it is crucial to note that existing methods face certain
challenges. Specifically, they generally leverage visual cues,
which are unfortunately not robust under all conditions. To
address this critical issue, we delve into a novel paradigm.
```

**Why the bad version fails:** every sentence is the same length, every paragraph opens with a transition, *"crucial/important/critical"* stack up, *"leverage"* and *"delve"* are AI-tells, no concrete numbers.

## Anti-Pattern Checklist

- **Repeated transition opener**: *"Furthermore/Moreover/Additionally"* in 3+ consecutive paragraphs — rewrite as *"By X, Y"* or *"Consequently, ..."*
- **Wishy-washy intensifier**: *"very"*, *"really"*, *"quite"*, *"rather"* as filler
- **Passive stacking**: *"It is observed that..."*, *"It can be seen that..."* — rewrite in active voice
- **Buzzword inflation**: count occurrences of *"novel"*, *"state-of-the-art"*, *"remarkable"* — keep ≤ 1 per abstract
- **Symmetric climax**: every sentence ends with a punchy noun — readers suspect templating
- **"Novel" overuse**: limit to ≤ 1 occurrence in the abstract; replace later uses with *"proposed"*, *"designed"*, *"introduced"*
- **"Leverage" appearances**: zero — use *"use"*, *"build on"*, *"exploit"*

## Benefits

- **Trust**: Reviewers trust prose that sounds like a human wrote it
- **Clarity**: Variation in sentence shape reveals what matters
- **Memorability**: Specific numbers and concrete claims stick; vague hype does not
- **Consistency**: Sentence-shape rotation + "By X, Y" openers match the dominant house voice across top-tier venues

## Related Skills

- [rule-academic-writing-abstract-ieee](../abstract-ieee/SKILL.md) - Apply human-style discipline inside the Abstract
- [rule-academic-writing-introduction-ieee](../introduction-ieee/SKILL.md) - Tone carries through the multi-paragraph funnel
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Class-default macros reinforce the human voice

## Remember

- Specific numbers > generic claims
- Active voice > passive stacking
- Short sentences > uniform-length paragraphs
- Rotate through Claim+cost / Although+main / Consequently / By+cause / Specific number within each methodology paragraph
- Open Methodology section-closers with *"By ..."* sentences