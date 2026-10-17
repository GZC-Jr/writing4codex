---
name: human-writing-style
description: "Avoid AI-flavored English in academic writing and produce prose that reads like a researcher wrote it — CV/Robotics/IP top-journal/conference style (T-PAMI / TIP / CVPR / ICRA)"
metadata:
  migrated-from: "human-writing-style.mdc"
  source-always-apply: "true"
  source-globs: ""
---

## Codex Invocation

Use this skill for every academic prose task in this project.
It is the prose baseline, with section or artifact skills added when their triggers match.
The source rule had no file glob.
Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern.
If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Human Writing Style for Academic Papers

> **Note**: This skill is the prose baseline for every section.
> Section-specific skills build on top of it.

## Core Principle

Academic prose should be precise, varied, and unforced.
Use the following as writing choices when they serve the content, rather than as a fixed paragraph template.

1. **Natural sentence variation** — combine direct claims, qualifying clauses, causal explanations, consequences, and supported numeric statements as the argument requires.
2. **Hedging without hedging vocabulary** — quality human voice hedges by stating limits concretely (*"performance degrades sharply when the baseline encounters OOD inputs"*) rather than with the adverb *"probably"*.
3. **Causal explanations** — use *"By incorporating X, Y ..."* when the mechanism supports that relationship and the grammatical subject performs the action.
   Avoid forcing every design paragraph or subsection ending into this form.

## Rules

### Mandatory Avoidance: Semicolons and Contractions

**强烈避雷：普通学术行文默认禁用分号，动词和否定形式必须写全，不得使用缩写。**

- **No semicolons in ordinary prose**: do not use `;` or `；` to connect clauses in Chinese or English academic writing, including abstracts, body text, captions, and review responses.
  Split independent clauses into complete sentences, keeping one sentence per source line, or use a suitable conjunction without creating a comma splice.
  Preserve semicolons only in verbatim quotations or required technical syntax, such as code, mathematical notation, or citation commands.
- **No verb or negation contractions**: write `it is`, `there is`, `we are`, `it has`, `we have`, `will not`, `cannot`, and `do not` in full.
  Do not use forms such as `it's` / `it’s`, `there's` / `there’s`, `we're`, `we've`, `won't`, `can't`, or `don't` in academic prose.
  This rule covers contractions with either straight or typographic apostrophes.
  Expand `'s` / `’s` to `is` or `has` according to meaning, and expand other contracted auxiliaries in the same way.
  Preserve possessive apostrophes, as in `the model's output` or `the authors’ results`.

These requirements apply throughout the project and take precedence over conflicting positive examples in section skills.

### Preferred Voice: Object-Centered Passive Statements

**语态偏好：尽可能避免以 `we` 为主语陈述研究贡献或操作，优先采用以方法、模块、实验等为主语的被动语态。**

- Prefer natural passive constructions for proposing, designing, introducing, developing, training, evaluating, and other author actions.
  Recast `we propose`, `we proposed`, `we design`, `we designed`, and similar statements wherever the same meaning can be preserved.
- Use a complete, grammatically inflected passive verb, choosing `is/are`, `was/were`, or `has/have been` from the section and context.
  Preserve whether an action is completed, ongoing, or planned, along with its certainty and attribution.
  The shorthand `be proposed` must be inflected appropriately when used as the main verb of a sentence.
- Use named methods, components, and results as subjects when explaining their behavior or findings.
  State observations directly instead of adding empty wrappers such as `It is observed that` or `It can be seen that`.
- In reviewer responses, conventional acknowledgments such as `We thank the reviewer` may be retained, with revision actions phrased as `A paragraph has been added` wherever natural.

- Avoid:
  `We propose a method.`
  Prefer:
  `A method is proposed.`
- Avoid:
  `We proposed a method.`
  Prefer:
  `A method was proposed.`
- Avoid:
  `We designed a module.`
  Prefer:
  `A module was designed.`
- Avoid:
  `We introduce a strategy.`
  Prefer:
  `A strategy is introduced.`
- Avoid:
  `We conducted experiments.`
  Prefer:
  `Experiments were conducted.`

### ✅ DO

- **Vary sentence length** by combining direct statements with useful qualifications.
  `This design adds overhead.`
  `Although this design adds overhead, its 1.50 M parameters remain within the deployment budget.`
- **Open sections with substance**, not a transition phrase like *"In this section, we discuss..."*
- **Use field-standard vocabulary sparingly**: do not reach for buzzwords (*"delve into"*, *"leverage"*, *"tapestry of"*, *"robust solution"*) — say *"use"*, *"build on"*, *"suitable"*
- **Hedge concretely**: replace *"probably will degrade"* with *"PSNR drops to 24.09 dB at ×6"* and *"somewhat robust"* with *"robust in-domain, degrades at ×6 out-of-distribution"*
- **Cite the work you build on** to make attribution explicit
- **Use "By X, Y" causal openers** when introducing a design rationale: *"By incorporating scale-prompting information into the feature extraction module, the model realizes adaptive representation."*
- **Close methodology subsections with a supported design takeaway**, using a causal sentence when it explains the mechanism accurately.

### ❌ AVOID

- Do not open multiple paragraphs with *"In order to"*, *"To understand..."*, or *"Recently, [topic] has..."*
- Do not overuse emphatic adjectives: *"crucial"*, *"vital"*, *"paramount"*, *"revolutionary"* — reviewers flag these as AI-tells
- Do not write apology-phrases (*"I'm sorry, but..."*, *"Unfortunately, we cannot..."*) in a research paper
- Do not over-explain motivation in the abstract or turn it into a sales pitch
- Do not use Markdown-style punctuation or emoji in LaTeX body text
- Do not write *"leverage"*, *"delve"*, *"tapestry"*, *"harness the power of"* — these are pure AI-flavor markers

## Sentence-Shape Inventory

Use these sentence shapes selectively, varying the prose without imposing a fixed sequence on every paragraph:

- **Claim and cost**:
  Existing fixed-scale methods achieve strong results at their target scale.
  However, separate models are required for each upscaling factor, increasing computational cost.
- **Qualification**:
  Although this method offers simplicity and efficiency, its performance degrades under domain shift.
- **Consequence**:
  Consequently, separate models must be trained for each target scale.
- **Cause**:
  By using a learnable distance metric to compute weighting coefficients, the method supports adaptive feature aggregation.
- **Specific result**, with illustrative values that must be replaced by verified results:
  At a scaling factor of ×1.2, the method attains a PSNR/SSIM of 40.50 dB/0.9890, surpassing the baseline by 5.07 dB/0.0141.
- **Limitation**:
  Despite these promising results, several limitations remain.

## Hedging Without Hedging Vocabulary

Use measured results and concrete conditions when they are available.
The values below illustrate phrasing and must be verified before use.

- Avoid:
  `Our method probably performs better on most cases.`
  Prefer:
  `The method attains 40.50 dB/0.9890 at ×1.2, surpassing the previous best by 0.17 dB/0.0008.`
- Avoid:
  `This is somewhat effective.`
  Prefer:
  `The method is robust in-domain but degrades to 24.09 dB at ×6 out-of-distribution.`
- Avoid:
  `In general, X is more suitable than Y.`
  Prefer:
  `The gain over the baseline narrows from 5.07 dB/0.0141 at ×1.2 to 0.04 dB at ×6.`
- Replace `It is believed that ...` with an attributed claim or a direct observation supported by the available evidence.
  Preserve uncertainty when measurements or support are unavailable.

## Examples

### ✅ Good

```markdown
Although high-resolution sensors can alleviate these issues, they are prohibitively expensive and lack the flexibility to perform arbitrary-scale zooming.
Super-resolution (SR) techniques provide a promising solution by enhancing spatial quality.
However, most existing SR methods adopt identical feature representations across all scales, lacking the ability to adaptively adjust features according to varying requirements, leading to suboptimal results.
```

### ❌ Bad (AI-flavored)

```markdown
In recent years, with the vigorous development of deep learning and the growing importance of computer vision, the field has attracted tremendous attention from both academia and industry.
However, it is crucial to note that existing methods face certain challenges.
Specifically, they generally leverage visual cues, which are unfortunately not robust under all conditions.
To address this critical issue, we delve into a novel paradigm.
```

**Why the bad version fails:** every sentence is the same length, every paragraph opens with a transition, *"crucial/important/critical"* stack up, *"leverage"* and *"delve"* are AI-tells, no concrete numbers.

## Anti-Pattern Checklist

- **Semicolons**: remove `;` and `；` from ordinary academic prose, checking any retained occurrences against the mandatory exceptions above.
- **Contractions**: expand contracted verbs, auxiliaries, and negation with either apostrophe style, while preserving possessive forms.
- **Author-led contributions and actions**: recast `we propose`, `we proposed`, `we design`, `we designed`, and similar statements in natural object-centered passive voice wherever possible.
- **Repeated transition opener**: replace repeated *"Furthermore/Moreover/Additionally"* openings with substantive statements or a transition supported by the actual relationship.
- **Wishy-washy intensifier**: *"very"*, *"really"*, *"quite"*, *"rather"* as filler
- **Empty reporting wrappers**: remove *"It is observed that..."* and *"It can be seen that..."* when the observation can be stated directly, while retaining useful passive constructions for author actions.
- **Buzzword inflation**: count occurrences of *"novel"*, *"state-of-the-art"*, *"remarkable"* — keep ≤ 1 per abstract
- **Symmetric climax**: every sentence ends with a punchy noun — readers suspect templating
- **"Novel" overuse**: limit to ≤ 1 occurrence in the abstract and replace later uses with *"proposed"*, *"designed"*, *"introduced"*
- **"Leverage" appearances**: zero — use *"use"*, *"build on"*, *"exploit"*

## Benefits

- **Trust**: Reviewers trust prose that sounds like a human wrote it
- **Clarity**: Variation in sentence shape reveals what matters
- **Memorability**: Specific numbers and concrete claims are more memorable than vague hype
- **Consistency**: Natural variation and supported causal explanations maintain the project's writing style.

## Related Skills

- [rule-academic-writing-abstract-ieee](../abstract-ieee/SKILL.md) - Apply human-style discipline inside the Abstract
- [rule-academic-writing-introduction-ieee](../introduction-ieee/SKILL.md) - Tone carries through the multi-paragraph funnel
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Class-default macros reinforce the human voice

## Remember

- Specific numbers > generic claims
- Prefer object-centered passive voice for author actions and contributions, with clear attribution and no empty reporting wrappers
- Short sentences > uniform-length paragraphs
- Vary sentence shapes to suit the argument, using numeric claims only when evidence is available.
- Use causal subsection summaries when supported, without forcing a *"By ..."* opener.
