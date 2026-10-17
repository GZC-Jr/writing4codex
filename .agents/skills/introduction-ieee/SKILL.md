---
name: introduction-ieee
description: "Introduction writing for CV/Robotics/IP top journals and conferences — multi-paragraph funnel + numbered contribution list"
metadata:
  migrated-from: "introduction-ieee.mdc"
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

# Introduction Writing

> **Note**: Use this skill when drafting/revising `\section{Introduction}` of a top-tier journal or conference paper.
> The multi-paragraph funnel and the numbered-contributions list apply across IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, IROS, and related venues.

## Core Principle

The Introduction follows a **multi-paragraph funnel** that ends with a numbered `\begin{enumerate}` of contributions.
Unlike the rigid 4-paragraph opener, the funnel has **5-7 paragraphs**, each tightening the argument one notch:

```
P1: Domain affordance (what the field enables)
P2: Constraint that motivates the paper (sensor limitation, training cost, latency, ...)
P3: Existing direction 1 + its gap (method family A)
P4: Existing direction 2 + its gap (method family B, current SOTA)
P5: ① + ② + ③ architectural levers that close the gap
P6: "The main contributions are summarized as follows." → numbered \begin{enumerate}
P7: Roadmap sentence (close)
```

The 5-7 paragraph funnel is a planning default, with paragraph length adjusted to the actual argument and venue budget.
Use evidence-supported transitions without forcing every paragraph to the same sentence count or ending.

## Constants

- **PARAGRAPH_FUNNEL**: `[P1 affordance, P2 constraint, P3 prior direction 1, P4 prior direction 2, P5 lever, P6 contributions, P7 roadmap]` - Canonical introduction funnel.
- **ROADMAP_OPENER**: `The remainder of this paper is organized as follows.` - Single sentence, sets up Sect.~X references.
- **CONTRIBUTION_OPENER**: `The main contributions are summarized as follows.` - Single sentence, comes before the `\begin{enumerate}` block.

## Rules

### ✅ DO

- **P1**: open with a strong domain claim, e.g. *"Thermal imaging is a critical sensing modality for autonomous systems in low-light environments"*
- **P2**: surface the *technical* constraint — sensor limitation, training cost, latency — with citation density ≥ 2
- **P3 + P4**: each cover **one prior direction** (e.g. method family A, method family B).
  End each with *"Consequently, ..."* / *"However, ..."* before pivoting to the next
- **P5**: introduce your method, e.g. *"In this work, ... is proposed"*, then enumerate your 2-3 design choices each as its own sentence
- **P6**: precede the `\begin{enumerate}` with the literal phrase *"The main contributions are summarized as follows."*.
  Each `\item` is *1-2 sentences* and self-contained
- **P7**: close with a brief roadmap paragraph using the manuscript's selected section-reference convention.
- Cite relevant sources for the prior directions in P3-P4 and design foundations in P5, without padding to a fixed quota.
  Place each citation immediately after the specific method it identifies.

### ❌ AVOID

- Do not bury the method announcement in P2 or P3 — keep P5 dedicated to **your** method
- Avoid author-led statements such as *"In this paper, we propose ..."* throughout the Introduction, introducing the method in P5 with passive wording such as *"In this work, a method is proposed ..."* instead.
- Do not introduce new notation in the Introduction.
  Defer to Preliminaries (`methodology-ieee skill`)
- Do not end with *"we hope this work contributes to the field"* — always use the roadmap sentence
- Do not write more than 2 sentences in a row using the same sentence structure (intro paragraphs flatten easily)
- Do not split the contributions into a `\begin{enumerate}` of *more than 5 items* — 3-4 is the sweet spot for clarity

## Patterns

### Multi-Paragraph Funnel

```latex
% ✅ Good: 7-paragraph funnel with numbered contributions
\section{Introduction}
\label{sec:intro}

% P1: domain affordance
[Domain] Thermal imaging is a critical sensing modality for autonomous systems in low-light or visually obscured environments where visible light imaging is ineffective \cite{ref2, ref3, ref4}.

% P2: technical constraint
However, a fundamental limitation of typical onboard thermal sensors is their inherently low resolution (LR) \cite{ref5}, which leads to a significant loss of spatial detail.
This degradation makes it challenging to accurately identify small or distant objects, delineate boundaries, and extract fine-grained scene information.
Although high-resolution (HR) thermal sensors can alleviate these issues, they are prohibitively expensive and lack the flexibility to perform arbitrary-scale zooming.

% P3: prior direction 1
Super-resolution (SR) techniques provide a promising solution by enhancing spatial quality \cite{ref6, ref7, ref8, ref9}.
However, most existing SR methods are designed for fixed-scale reconstruction, where a specific upscaling factor is predefined during training \cite{ref10}.
Consequently, separate models must be trained for each target scale, leading to high computational costs and reduced flexibility in practical applications.

% P4: prior direction 2 + remaining gap
To address the limitation of fixed-scale SR, arbitrary-scale SR methods have emerged as a more flexible alternative \cite{ref12, ref13, ref14}.
These methods generate images at any resolution without requiring separate models for each upscaling factor.
However, most existing arbitrary-scale SR methods adopt identical feature representations across all scales, lacking the ability to adaptively adjust features according to varying requirements, leading to suboptimal results.

% P5: method announcement + design levers
In this work, an arbitrary-scale SR method is proposed for image reconstruction.
The proposed method (\textbf{OurMethod}) is designed to handle any scale factors.
By incorporating task-relevant information into both feature extraction and upsampling, OurMethod realizes robust and high-quality reconstructions.
To achieve this, a module (Module A) is introduced to embed target information into the feature extraction process.
In addition, a feature aggregation strategy is designed in the upsampler by jointly integrating multiple information sources.

% P6: numbered contributions
The main contributions are summarized as follows.
\begin{enumerate}
  \item The OurMethod network is proposed to realize high-quality image reconstruction.
  Different from most existing methods, OurMethod jointly encodes task-relevant information and thoroughly considers the significance of design choice A.
  \item Task-relevant information is integrated into the network module, allowing the model to adaptively understand variations across conditions, thereby providing precise feature representations for the target resolution.
  \item By explicitly learning feature space weights and embedding design information into the local feature ensemble, the proposed upsampler enhances the ability to interpret spatial relationships and accurately reconstruct fine-grained details.
  \item Extensive experiments on benchmark datasets demonstrate that OurMethod outperforms existing state-of-the-art methods in both quantitative and qualitative results.
\end{enumerate}

% P7: roadmap
The remainder of this paper is organized as follows.
Previous studies are reviewed in Sect.~\ref{sec:related}.
The proposed method is introduced in Sect.~\ref{sec:method}.
Experiments are reported in Sect.~\ref{sec:exp}.
Conclusions are presented in Sect.~\ref{sec:conclusion}.
```

```latex
% ❌ Bad: 3 paragraphs only; vague method announcement; no numbered list; vague close
\section{Introduction}
% ... two paragraphs of pure background ...
% ... "we propose a novel method" with no design levers ...
% ... ends with "we hope this contributes ..." ...
```

### Standard Roadmap Paragraph

```latex
% ✅ Good
The remainder of this paper is organized as follows.
Closely-related work is reviewed in Sect.~\ref{sec:related}.
The proposed method is described in Sect.~\ref{sec:method}.
Experiments are presented in Sect.~\ref{sec:exp}.
Conclusions are presented in Sect.~\ref{sec:conclusion}.
```

```latex
% ❌ Bad
We have organized the paper as follows...
[vague] In the next section, we will discuss...
[forward reference, no \cref]
```

## Examples

### ✅ Good P1 Opening

> "Thermal imaging is a critical sensing modality for autonomous systems in low-light or visually obscured environments where visible light imaging is ineffective."

### ✅ Good P5 (Method Announcement + Levers)

> "In this work, a novel method is proposed for image reconstruction.
> To achieve this, a module (Module A) is introduced to embed target information into the feature extraction process.
> In addition, the feature aggregation strategy is designed in the upsampler by jointly integrating multiple information sources."

### ❌ Bad P1 (AI-flavored)

> "In recent years, with the vigorous development of technology and deep learning, object tracking has been extensively studied..."

## Benefits

- **Reviewer flow**: A 5-7 paragraph funnel maps cleanly to "domain → constraint → prior → gap → method → contributions → roadmap"
- **Citation discipline**: P3-P4 carry the citation density.
  Readers know where to look
- **Contribution traceability**: Each `\item` in P6 has an explicit section anchor downstream
- **Self-disclosure**: Numbered contributions include any *new dataset* or *new benchmark*

## Related Skills

- [rule-academic-writing-abstract-ieee](../abstract-ieee/SKILL.md) - The Introduction must add depth, not paraphrase the abstract
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Vary sentence shape across paragraphs
- [rule-academic-writing-related-work-ieee](../related-work-ieee/SKILL.md) - P3-P4 supply citations consumed by the Related Work section

## Remember

- 5-7 paragraphs, each with one job.
  The funnel tightens monotonically
- The literal phrase *"The main contributions are summarized as follows."* precedes the `\begin{enumerate}`
- Close the Introduction with a brief roadmap when required by the venue or useful for the reader.
- Do not duplicate the abstract.
  Add technical depth
