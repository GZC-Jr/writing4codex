---
name: latex-ieee-conference
description: "IEEE conference LaTeX paper standards (10pt, two-column, page-limited)"
metadata:
  migrated-from: "latex-ieee-conference.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# IEEE Conference LaTeX Paper Standards

> **Note**: For IEEE *conference* papers (CVPR, ICCV, ECCV, NeurIPS, ICML) where `main.tex` uses `10pt`/`twocolumn` options and a strict page limit. For journal papers, see `latex-ieee-paper skill` instead.

## Core Principle

Conference submissions are shorter, denser, and more figure-driven than journal papers. Brevity and clarity take precedence over exhaustive proof.

## Constants

- **MAIN_TEX**: `main.tex` - Single-file root of a conference paper.
- **CLASS_CONFERENCE**: Conference class (e.g. `cvpr`/`iccv`/`acmart`/`llncs`) - Load via `\documentclass[...]`.
- **PAGE_LIMIT**: 8 (CVPR/ICCV/ECCV main) - Hard page limit; supplementary does not count.

## Rules

### ✅ DO

- Declare the conference class explicitly, e.g. `\documentclass[10pt,twocolumn,letterpaper]{article}` with the matching `\usepackage{iccv2025}` style
- Keep the abstract under 300 words; most conferences cap at 200-250
- Place teaser/overview figure at the top of the introduction (before paragraph 3)
- Reference supplementary material only via a `\supple{}` or footnote, never inline
- Use `%TODO:` comments to flag missing figures/results so re-runs of compile do not silently drop content

### ❌ DON'T

- Don't extend beyond the page limit (well-known cause of desk rejection)
- Don't put numbered section headings before the first numbered section (most conferences want `\section{Introduction}` numbered)
- Don't repurpose the journal `IEEEtran` class — it lacks the conference-style option set
- Don't hide weak results in supplementary without acknowledging them in the main paper

## Patterns

### Conference vs. Journal Preamble

```latex
% ✅ Good: Conference (CVPR-style)
\documentclass[10pt,twocolumn,letterpaper]{article}
\usepackage{iccv2025}
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage{subcaption}
```

```latex
% ❌ Bad: Journal class repurposed for a conference submission
\documentclass[lettersize,journal]{IEEEtran}
% Missing: page count, two-column flow, conference bibliography style
```

### Teaser Figure Placement

```latex
% ✅ Good: teaser before paragraph 3 of the introduction
\section{Introduction}
\label{sec:intro}

% Paragraph 1: motivation
% Paragraph 2: gap in prior work
\begin{figure}[t]
  \centering
  \includegraphics[width=\columnwidth]{teaser.pdf}
  \caption{Teaser: MAE-OVT tracks arbitrary targets via natural-language descriptions
    under aerial degradation.}
  \label{fig:teaser}
\end{figure}
% Paragraph 3: our contribution
```

```latex
% ❌ Bad: teaser buried at the end of introduction
% ... paragraph 4 ...
\begin{figure}[t]
  \includegraphics[width=\columnwidth]{teaser.pdf}
  \caption{Teaser.}
\end{figure}
% conference reviewers rarely read past Fig. 1; burying hurts first impression
```

## Benefits

- **Submission success**: Matches conference-deck expectations, reducing desk-reject risk
- **Readability**: Page-limit discipline forces the strongest arguments to surface first
- **Reproducibility**: `%TODO:` markers ensure deferred assets are tracked across re-runs

## Related Skills

- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Sibling rule for journal submissions
- [rule-academic-writing-latex-figures-and-tables](../latex-figures-and-tables/SKILL.md) - Figure policy shared across venues

## Remember

- Conference page limits are hard; if you cannot fit, cut a comparison or move it to supplementary
- Journal and conference preambles are not interchangeable
- Teaser figure earns its place at the start of the introduction, not at the end