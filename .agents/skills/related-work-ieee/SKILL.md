---
name: related-work-ieee
description: "Related Work writing for CV/Robotics/IP top journals and conferences — thematic clusters with supported limitation paragraphs"
metadata:
  migrated-from: "related-work-ieee.mdc"
  source-always-apply: "false"
  source-globs: ""
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact.
Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source rule had no file glob.
Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern.
If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Related Work Writing

> **Note**: Use this skill when drafting/revising `\section{Related Work}` of a top-tier journal or conference paper.
> The thematic-cluster-then-limitation paragraph pattern is standard across IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, and related venues.

## Core Principle

Related Work is a sequence of **thematic** clusters (`\subsection{Method Family A}`, `\subsection{Method Family B}`, `\subsection{Method Family C}`).
Each cluster:

1. Groups prior work by **technique lineage**, not by paper
2. **Begins** with seminal work, **moves through** recent advances, and **closes** with a *limitation paragraph* (1-3 sentences) that names the gap your work fills

The limitation paragraph is the bridge to your Methodology — it should re-appear, in paraphrased form, as the *gap sentence* in your Introduction's P3 or P4.

## Constants

- **CLUSTER_PATTERN**: `\subsection{<Thematic Title>}` with class-generated numbering.
- **LIMITATION_OPENER**: a substantive limitation statement or a suitable transition such as `However, ...`.
  Vary openings naturally while making the gap explicit after the cited work.

## Rules

### ✅ DO

- Use 3-5 thematic clusters as a planning default, with one per relevant line of prior work and plain subsection titles.
- Use the 5-12 references per cluster as a planning guide only when that many relevant sources are available.
  Cite enough to support the lineage and gap without adding references to meet a quota.
- Attach each specific method's citation immediately after its name, before explaining its mechanism or results.
  Cite distinct named methods separately rather than appending a combined citation at the sentence end.
- Open each cluster with the **seminal paper** of that lineage, then move chronologically to the SOTA
- Close every cluster with a **limitation paragraph**: 1-3 sentences that name the gap your method fills, e.g. *"However, they use the same feature representation for all upscaling factors, lacking the ability to adapt to varying scale requirements."*
- Include relevant prior work by the authors under the same relevance and attribution criteria as other sources.
- Reference the **latest SOTA** with `\cite{}` so reviewers see you compare against the right baseline

### ❌ AVOID

- Do not write a flat list of single-sentence summaries — Related Work needs structure
- Do not compare to your own method via vague phrases ("better than previous work").
  Name the prior method and the metric
- Do not omit a relevant foundational citation merely because the method is well known.
  Place implementation background in Preliminaries when appropriate, and avoid irrelevant citation padding.
- Do not end a cluster with a forward-only *"we will discuss our method in Sect. III"* — name the gap instead
- Do not apologize for not citing a specific paper.
  Either cite it or move on

## Patterns

### A./B./C. Thematic Clusters with Limitation Paragraphs

```latex
% ✅ Good: 3 alphabetic clusters, each closed by a limitation paragraph
\section{Related Work}
\label{sec:related}

\subsection{Method Family A}
Early approaches to this problem primarily rely on technique A \cite{ref22} and method B \cite{ref23} to establish a baseline.
They are often computationally intensive and have limited performance.
The introduction of deep learning has significantly advanced the field.
Dong et al. \cite{ref24} are the first to apply convolutional networks to this problem.
Subsequent developments such as DRCN \cite{ref25} incorporate recursive architectures, while DRRN \cite{ref26} utilizes parameter sharing to reduce model complexity.
More recent advances have focused on attention mechanisms to enhance feature modeling.
SwinIR \cite{ref18} employs a shifting window technique to capture long-range dependencies.
SRFormer \cite{ref33} introduces permuted self-attention, which enables the advantages of large-window self-attention while reducing computational costs.

However, all these methods are tailored for fixed conditions and fail to incorporate prior scale information.
Their backbones achieve limited performance when applied to varying conditions.

\subsection{Method Family B}
The development of deep learning in related tasks has inspired researchers to investigate the potential for enhancing performance using technique C.
TEN \cite{ref34} addresses the low-resolution issue by learning an end-to-end mapping.
Method D \cite{ref35} further incorporates attention into a contrastive learning framework.
Method E \cite{ref36} introduces a channel-splitting network which extracts versatile features while eliminating redundancy.
Method F \cite{ref38} extends this line of research by introducing a transformer-based framework that maintains robustness under varying conditions.

However, the datasets used in these methods do not cover the target scenarios, and all these methods are limited in their ability to generalize across varying conditions.

\subsection{Method Family C}
Recent advancements have addressed the challenge with several methods emerging to improve performance.
MetaSR \cite{ref13} introduces the first meta-learned approach for the task, using an established baseline for feature extraction.
Building on this, LIIF \cite{ref21} utilizes coordinate information and deep features as inputs to predict values at specified coordinates.
Inspired by the meta-learning approach, RSAN \cite{ref40} uses coordinate information and polynomial functions of scale factors to predict reconstruction.
SRNO \cite{ref44} first maps the low-resolution input into a higher dimensional latent space to capture sufficient basis functions.

However, they use the same feature representation across all conditions.
Besides, the separation between feature values and spatial coordinates prevents the model from fully utilizing both visual and positional information for accurate prediction.
```

```latex
% ❌ Bad: flat enumeration, no sub-organization, no gap statement
\section{Related Work}
[Various papers have proposed various methods.
Method A does X.
Method B does Y.
Method C does Z.
We propose something different.]
```

### Limitation Paragraph Templates

```latex
% ✅ Good: 1-3 sentences naming the gap your method fills
However, all these methods are tailored for fixed conditions and fail to incorporate prior scale information.
Their backbones achieve limited performance when applied to varying conditions.

% ✅ Good: 2 sentences citing the limitation, then a sentence on impact
However, the datasets used in these methods do not cover the target scenarios, and all these methods are limited in their ability to generalize across varying conditions.
```

```latex
% ❌ Bad: forward-only paragraph without naming the gap
We will discuss our method in the next section.
% Reviewer can only ask: "what gap are you filling?"
```

## Examples

### ✅ Good Limitation Paragraph

> "However, they use the same feature representation across all conditions.
> Besides, the separation between feature values and spatial coordinates prevents the model from fully utilizing both visual and positional information for accurate prediction."

### ✅ Good Subsection Cluster Title

> "A.
> Method Family A" "B.
> Method Family B" "C.
> Method Family C"

### ❌ Bad Limitation Paragraph

> "We feel that our approach is different from these existing methods.
> Hopefully this analysis can demonstrate the advantages of our framework."

## Benefits

- **Coverage**: Relevant citations establish each lineage and its limitations.
- **Positioning**: The limitation paragraph at the end of each cluster positions your work without sales pitch
- **Self-disclosure**: Calling out co-author prior work prevents "hidden dual submission" flags

## Related Skills

- [rule-academic-writing-introduction-ieee](../introduction-ieee/SKILL.md) - P3-P4 of the Introduction funnel borrow citation density from this section
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Avoid "Existing methods have achieved great success, however..."

## Remember

- 3-5 alphabetic clusters by thematic lineage
- Each cluster ends with a **limitation paragraph** (1-3 sentences) that names the gap
- The same limitation sentence re-appears, paraphrased, in Introduction P3 or P4
- Cite relevant seminal and recent work, with citations immediately after specific method names.
