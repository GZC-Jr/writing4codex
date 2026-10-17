---
name: abstract-ieee
description: "Abstract writing for CV/Robotics/IP top journals and conferences — Background → Problem → Method → Evidence → Result five-beat arc"
metadata:
  migrated-from: "abstract-ieee.mdc"
  source-always-apply: "false"
  source-globs: "**/abstract*.tex"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact.
Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was `**/abstract*.tex`.
Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern.
If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Abstract Writing

> **Note**: Use this skill when drafting/revising the `\begin{abstract}...\end{abstract}` block.
> The five-beat pattern applies across IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, and related venues.

## Core Principle

An Abstract is a 200-250 word self-contained synopsis in **five beats**:

**Background** → **Problem** → **Method** → **Evidence (evaluation or dataset)** → **Headline result**, with a verified code link when available and permitted.

Omit figures, citations, and displayed equations by default, following the actual venue's abstract requirements.
The five beats describe content roles, with sentence counts adjusted to the evidence and word budget.

## Constants

- **BEATS**: `[Background, Problem, Method, Evidence, Result]` - Five-beat canonical arc in this exact order.
- **WORD_BUDGET_JOURNAL**: 250 - Typical cap for journal abstracts (T-PAMI, TIP, TII, TIM).
- **WORD_BUDGET_CONFERENCE**: 200 - Typical cap for CVPR, ICCV, ECCV, ICRA, NeurIPS, ICML.

## Rules

### ✅ DO

- Open the **Background** beat by stating the *domain affordance* — what the technology enables, not "research has attracted much attention"
- Move to **Problem** beat with explicit limitation verbs: *"suffer from"*, *"limited by"*, *"fail to"*, *"lack the ability to"*
- Name the proposed method in the **Method** beat.
  Wrap the acronym in `\textbf{}` on first appearance
- Prefer passive contribution statements such as `A method is proposed` or `A module is designed`, with tense chosen from context.
- Add an Evidence beat based on available evaluation, which may use established datasets, an actual new dataset, or a documented experiment.
  Describe a new dataset only when it is part of the work.
- Close the Result beat with verified numeric results and named baselines where available.
  Include a code URL only when a verified public repository exists and the venue permits it.
- Join micro-clauses with suitable conjunctions rather than semicolons, and keep beats paragraph-distinct only when the abstract is multi-paragraph.

### ❌ AVOID

- Do not open with *"In this paper, we propose..."* — start with the *problem*, not the *contribution*
- Do not cite references inside the abstract (`\cite{}` is forbidden by most venues)
- Do not introduce notation not defined in the main paper
- Do not write filler transitions like *"in recent years, with the vigorous development of..."*
- Do not conflate Method and Evidence or force their content into one sentence per beat.
- Do not use the verb *"leverage"* — reviewers flag it as AI-flavored

## Patterns

### Five-Beat Abstract

```latex
% ✅ Good: five content roles with verified results supplied in the placeholders.
\begin{abstract}
[Background] Sensing modalities such as thermal imaging or RGB-depth cameras significantly augment the operational capabilities of autonomous systems in challenging environments.
[Problem] However, the limited resolution of commodity sensors constrains fine-grained perception, making it difficult to accurately identify small objects, delineate boundaries, and extract fine-grained scene information.
Existing methods often adopt identical feature representations across all conditions, lacking the ability to adaptively adjust processing according to varying requirements, leading to suboptimal performance.
[Method] To address these limitations, a method (\textbf{OurMethod}) is proposed.
A new architecture is introduced to explicitly encode task-relevant information for adaptive feature representation.
[Evidence] OurMethod is evaluated on [datasets] using [protocol], with [ablation] to examine [design choice].
[Result] On [benchmark], OurMethod attains [metric value], improving on [baseline] by [measured margin] under [conditions].
% Add a source-code sentence only when a verified public URL is available.
\end{abstract}
```

```latex
% ❌ Bad: meta opener, vague result, and no concrete evidence.
\begin{abstract}
In this paper, we propose a novel method that uses deep learning to improve performance.
Our method is very effective and outperforms existing methods.
Experiments show that the proposed method achieves state-of-the-art results.
The method has great potential in many applications.
\end{abstract}
% "In this paper, we propose" is the canonical opener to delete
% "very effective", "great potential" are anti-specific
% No concrete evaluation is identified to support the result claim.
```

## Examples

### ✅ Good Opening

> "Thermal imaging significantly augments the operational capabilities of intelligent systems in complex environments.
> However, due to the limited resolution of onboard sensors, captured images suffer from insufficient detail and blurred boundaries..."

### ✅ Good Method Beat

> "To address these limitations, a novel method (\textbf{OurMethod}) is proposed for enhanced perception."

### ✅ Good Evidence Beat

> "Furthermore, a new dataset (OurDataset) comprising [verified sample count] samples covering both indoor and outdoor scenes is constructed..."

### ❌ Bad Opening (AI-flavored)

> "In recent years, with the rapid development of deep learning and the vigorous growth of autonomous systems, [topic] has become a hot research topic..."

## Beat Counters

Use the beat labels as planning annotations and remove them from the submitted text.
A sentence may serve related roles when the method, evidence, and result remain clear.
The sentence counts below are planning ranges, with the actual abstract governed by the venue budget and available evidence.

| Beat | Marker phrase (any of) | Count in 250 words |
|------|------------------------|--------------------|
| Background | "augments", "enables", "represents a critical" | 1-2 sentences |
| Problem | "However", "limited by", "lacks" | 2-3 sentences |
| Method | "is proposed", "is designed", "is introduced" | 3-5 sentences |
| Evidence | "Additionally", "Furthermore", "constructed" | 1-2 sentences |
| Result | "outperforms", "Experimental results" | 2-3 sentences |

## Benefits

- **Coverage**: The five-beat plan keeps the problem, method, evidence, and result identifiable.
- **Searchability**: An acronym in `\textbf{}` shows up well in digital libraries
- **Evidence**: Evaluation on relevant established or new datasets supports the result claim.
- **Reproducibility**: A verified code URL can help when a public release exists and the venue permits it.

## Related Skills

- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Sentence-shape and word-choice discipline carry into the abstract
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Defines the `\begin{abstract}` environment
- [rule-academic-writing-introduction-ieee](../introduction-ieee/SKILL.md) - The Introduction must not duplicate the abstract verbatim

## Remember

- Five content roles: Background → Problem → Method → Evidence → Result, with an optional verified code link.
- `\textbf{YourAcronym}` on first appearance, inside the Method beat
- 200-250 words.
  `\cite{}` is forbidden inside the abstract
- Every beat is one paragraph-segment only.
  The whole abstract flows as one block
