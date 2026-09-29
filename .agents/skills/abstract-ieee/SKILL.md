---
name: abstract-ieee
description: "Abstract writing for CV/Robotics/IP top journals and conferences — Background → Problem → Method → Evidence → Result five-beat arc"
metadata:
  migrated-from: "abstract-ieee.mdc"
  source-always-apply: "false"
  source-globs: "**/abstract*.tex"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/abstract*.tex; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Abstract Writing

> **Note**: Use this skill when drafting/revising the `\begin{abstract}...\end{abstract}` block. The five-beat pattern applies across IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, and related venues.

## Core Principle

An Abstract is a 200-250 word self-contained synopsis in **five beats**:

**Background** → **Problem** → **Method** → **Evidence (dataset or experiment)** → **Headline result + code**.

No figures, no citations, no equations. Every beat must transition smoothly into the next; do not let one beat eat two sentences.

## Constants

- **BEATS**: `[Background, Problem, Method, Evidence, Result]` - Five-beat canonical arc in this exact order.
- **WORD_BUDGET_JOURNAL**: 250 - Typical cap for journal abstracts (T-PAMI, TIP, TII, TIM).
- **WORD_BUDGET_CONFERENCE**: 200 - Typical cap for CVPR, ICCV, ECCV, ICRA, NeurIPS, ICML.

## Rules

### ✅ DO

- Open the **Background** beat by stating the *domain affordance* — what the technology enables, not "research has attracted much attention"
- Move to **Problem** beat with explicit limitation verbs: *"suffer from"*, *"limited by"*, *"fail to"*, *"lack the ability to"*
- Name the proposed method in the **Method** beat; wrap the acronym in `\textbf{}` on first appearance
- Add an **Evidence** beat (typically a self-collected dataset or pilot experiment) — this beat is the Differentiation signal and is **non-optional**
- Close the **Result** beat with numeric gains (*"+0.51 dB over prior SOTA at ×4"*) and append a code URL with `\url{https://github.com/...}`
- Use semicolons to chain micro-clauses inside one beat; keep beats paragraph-distinct only when the abstract is multi-paragraph

### ❌ DON'T

- Don't open with *"In this paper, we propose..."* — start with the *problem*, not the *contribution*
- Don't cite references inside the abstract (`\cite{}` is forbidden by most venues)
- Don't introduce notation not defined in the main paper
- Don't write filler transitions like *"in recent years, with the vigorous development of..."*
- Don't collapse Method + Evidence into one sentence; if you propose both a method *and* a dataset, give each its own clause
- Don't use the verb *"leverage"* — reviewers flag it as AI-flavored

## Patterns

### Five-Beat Abstract

```latex
% ✅ Good: Background → Problem → Method (with acronym) → Evidence (dataset) → Result + URL
\begin{abstract}
[Background] Sensing modalities such as thermal imaging or RGB-depth
cameras significantly augment the operational capabilities of autonomous
systems in challenging environments. [Problem] However, the limited
resolution of commodity sensors constrains fine-grained perception,
making it difficult to accurately identify small objects, delineate
boundaries, and extract fine-grained scene information. Existing
methods often adopt identical feature representations across all
conditions, lacking the ability to adaptively adjust processing
according to varying requirements, leading to suboptimal performance.
[Method] To address these limitations, a novel method (\textbf{OurMethod})
is proposed. Specifically, a new architecture is introduced to
explicitly encode task-relevant information, enabling more precise
and adaptive feature representation. [Evidence] Furthermore, a new
dataset comprising N\,000 samples covering diverse scenarios is
constructed to facilitate research in this direction. [Result]
Experimental results demonstrate that OurMethod consistently
outperforms state-of-the-art methods across both quantitative
metrics and qualitative assessments. The source code is available at
\url{https://github.com/your-org/your-repo}.
\end{abstract}
```

```latex
% ❌ Bad: meta opener, vague result, no Evidence beat, no URL
\begin{abstract}
In this paper, we propose a novel method that uses deep learning
to improve performance. Our method is very effective and
outperforms existing methods. Experiments show that the proposed
method achieves state-of-the-art results. The method has great
potential in many applications.
\end{abstract}
% "In this paper, we propose" is the canonical opener to delete
% "very effective", "great potential" are anti-specific
% No Evidence beat — drops the dataset/self-collected result that distinguishes the submission
```

## Examples

### ✅ Good Opening

> "Thermal imaging significantly augments the operational capabilities
> of intelligent systems in complex environments. However, due to
> the limited resolution of onboard sensors, captured images suffer
> from insufficient detail and blurred boundaries..."

### ✅ Good Method Beat

> "To address these limitations, a novel method (\textbf{OurMethod})
> is proposed for enhanced perception."

### ✅ Good Evidence Beat

> "Furthermore, a novel dataset (OurDataset) comprising N\,000 samples
> covering both indoor and outdoor scenes is constructed..."

### ❌ Bad Opening (AI-flavored)

> "In recent years, with the rapid development of deep learning and
> the vigorous growth of autonomous systems, [topic] has become a
> hot research topic..."

## Beat Counters

Tag each beat in the abstract once and only once. If you find yourself
needing a sentence in two beats, it means one beat collapsed; the five
beats must be mutually exclusive in topic.

| Beat | Marker phrase (any of) | Count in 250 words |
|------|------------------------|--------------------|
| Background | "augments", "enables", "represents a critical" | 1-2 sentences |
| Problem | "However", "limited by", "lacks" | 2-3 sentences |
| Method | "we propose", "is proposed" | 3-5 sentences |
| Evidence | "Additionally", "Furthermore", "constructed" | 1-2 sentences |
| Result | "outperforms", "Experimental results" | 2-3 sentences |

## Benefits

- **Reviewer compliance**: The five-beat format is the standard abstract structure across top venues
- **Searchability**: An acronym in `\textbf{}` shows up well in digital libraries
- **Differentiation**: The Evidence beat (dataset/experiment) distinguishes a submission from papers that only recycle public data
- **Reproducibility signal**: A code URL in the abstract signals that authors take replication seriously

## Related Skills

- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Sentence-shape and word-choice discipline carry into the abstract
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Defines the `\begin{abstract}` environment
- [rule-academic-writing-introduction-ieee](../introduction-ieee/SKILL.md) - The Introduction must not duplicate the abstract verbatim

## Remember

- Five beats: Background → Problem → Method → Evidence → Result + code
- `\textbf{YourAcronym}` on first appearance, inside the Method beat
- 200-250 words; `\cite{}` is forbidden inside the abstract
- Every beat is one paragraph-segment only; the whole abstract flows as one block