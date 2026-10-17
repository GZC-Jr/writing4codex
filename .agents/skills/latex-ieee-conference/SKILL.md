---
name: latex-ieee-conference
description: "Conference LaTeX editing using the actual venue/year template, page budget, and supported figure and reference commands"
metadata:
  migrated-from: "latex-ieee-conference.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact.
Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was `**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}`.
Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern.
If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Conference LaTeX Paper Standards

> **Note**: Apply to conference papers using their actual venue and year template.
> Do not infer the class, column count, page limit, or IEEE affiliation from a conference name alone.
> For journal papers, use `latex-ieee-paper` when its scope matches.

## Core Principle

Conference submissions are shorter, denser, and more figure-driven than journal papers.
Brevity and clarity take precedence over exhaustive proof.

## Constants

- **MAIN_TEX**: `main.tex` - Single-file root of a conference paper.
- **CLASS_CONFERENCE**: the supplied `\documentclass` and any matching style package, preserved with its review or final options.
- **PAGE_LIMIT**: the actual target venue/year limit, including its rules for references and supplementary material.
  Record the limit as unknown when it has not been supplied or verified.

## Rules

### ✅ DO

- Preserve the official class, style package, review mode, anonymity settings, and paper size.
- Check the abstract against the verified venue word limit.
- Place an overview figure early when it helps the argument and the template supports the layout.
- Reference supplementary material with the convention actually defined by the template.
  Use a command such as `\supple{}` only when it is defined.
- Use `%TODO:` comments to flag missing figures/results so re-runs of compile do not silently drop content

### ❌ AVOID

- Do not extend beyond the page limit (well-known cause of desk rejection)
- Do not put numbered section headings before the first numbered section (most conferences want `\section{Introduction}` numbered)
- Do not submit a journal-mode preamble for a conference that requires a different mode or class.
  IEEEtran supports a `conference` option when the actual conference template uses it.
- Do not hide weak results in supplementary without acknowledging them in the main paper

## Patterns

### Conference vs. Journal Preamble

```latex
% ✅ Good: an IEEE conference template that specifies IEEEtran conference mode.
\documentclass[conference]{IEEEtran}
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
% Preserve any additional packages and options from the supplied template.
```

```latex
% ❌ Bad: journal mode used when the venue requires conference mode.
\documentclass[lettersize,journal]{IEEEtran}
% Use the actual venue template, which may instead use article plus a style package.
```

### Teaser Figure Placement

```latex
% ✅ Good: an overview near the introduction opening when the venue permits it.
\section{Introduction}
\label{sec:intro}

% Paragraph 1: motivation
% Paragraph 2: gap in prior work
\begin{figure}[t]
  \centering
  \includegraphics[width=\columnwidth]{teaser.pdf}
  \caption{Teaser: MAE-OVT tracks arbitrary targets via natural-language descriptions under aerial degradation.}
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

- **Template consistency**: The preamble and submission mode follow the actual venue requirements.
- **Readability**: Page-limit discipline forces the strongest arguments to surface first
- **Reproducibility**: `%TODO:` markers ensure deferred assets are tracked across re-runs

## Related Skills

- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Sibling rule for journal submissions
- [rule-academic-writing-latex-figures-and-tables](../latex-figures-and-tables/SKILL.md) - Figure policy shared across venues

## Remember

- Conference page limits are hard.
  If you cannot fit, cut a comparison or move it to supplementary
- Journal and conference preambles are not interchangeable
- Place an overview where it supports the argument, and inspect the rendered float placement.
