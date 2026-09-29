---
name: latex-ieee-paper
description: "IEEE journal LaTeX paper standards — IEEEtran + Roman-numeral + alphabetic-subsection layout"
metadata:
  migrated-from: "latex-ieee-paper.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# IEEE Journal LaTeX Paper Standards

> **Note**: Applies to `main.tex` of IEEE Transactions / journals (T-PAMI, TIP, TII, TIM, RA-L) and equivalent top-tier journals. Conference papers (CVPR/ICCV/ECCV/NeurIPS) use a different class — see `latex-ieee-conference skill` when applicable.

## Core Principle

IEEE journal papers follow strict, conservative LaTeX conventions enforced by the `IEEEtran` class. The class renders sections as **uppercase Roman numerals** (`I. INTRODUCTION`, `II. RELATED WORK`, ...) and subsections as **capital letters with a period** (`A. Method Family A`, `B. Method Family B`, ...). Respect the class defaults; **titles in `\subsection` should already carry the letter prefix** (`\subsection{A. Overall Architecture}`), not rely on `IEEEtran`'s automatic labeling.

## Constants

- **MAIN_TEX**: `main.tex` - Single-file root of an IEEE-style paper; everything below targets this file.
- **CLASS**: `IEEEtran` - Document class bundled separately from `\documentclass{}`; do not substitute `article`.
- **BIB_FILE**: `references.bib` - BibTeX source for all `\cite{}` calls.
- **SECTION_PATTERN**: `UPPERCASE_TITLE` - `\section{Introduction}` renders as `I. INTRODUCTION` automatically; capitalize manually if needed.
- **SUBSECTION_PATTERN**: `\subsection{<Cap>.<Title>}` - Capital letter + period + title; the prefix is authored, not auto-generated.

## Rules

### ✅ DO

- Use `\documentclass[lettersize,journal]{IEEEtran}` for journal submissions
- Place `\maketitle` immediately after `\begin{document}` + `\title{}` + `\author{}`
- Wrap the Abstract inside `\begin{abstract}...\end{abstract}` before `\begin{IEEEkeywords}`
- Author subsections with **letter prefix + period** (`A.`, `B.`, ...) so the rendered output is consistent with class default
- Author `\section{Reference}` style titles in mixed case (`\section{Introduction}`, not `\section{INTRODUCTION}`)
- Define notation in one place (a Preliminaries subsection or `notation.tex`) and reference it consistently
- Use `\label{sec:...}` / `\label{fig:...}` / `\label{eq:...}` immediately after the corresponding `\caption{}` or `\section{}` / `\begin{equation}`

### ❌ DON'T

- Don't switch to `article` class or rewrite the preamble to mimic conference templates
- Don't override IEEEtran's Roman-numeral-to-uppercase conversion by writing `\section{INTRODUCTION}` manually
- Don't redefine `\maketitle`, `\section`, or other IEEEtran-managed commands
- Don't inline BibTeX entries; all entries must live in `{BIB_FILE}`
- Don't use first-person plural more than necessary in objective statements
- Don't write `\subsection{Overall Architecture}` without the `A.` prefix — IEEEtran will still auto-number it, but the visual will read as `A. Overall Architecture` only when you include the prefix yourself

## Patterns

### Section + Subsection Labeling

```latex
% ✅ Good: \section{...} in mixed case, \subsection{<Cap>.<Title>}
\section{Introduction}
\label{sec:introduction}

\section{Related Work}
\label{sec:related}

\subsection{A. Method Family A}
\label{sec:method_family_a}

\subsection{B. Method Family B}
\label{sec:method_family_b}

\subsection{C. Method Family C}
\label{sec:method_family_c}

\section{Methodology}
\label{sec:method}

\subsection{A. Overall Architecture}
\label{sec:overall_arch}

\subsection{B. Module A}
\label{sec:module_a}

\section{Dataset}
\label{sec:dataset}

\subsection{A. Image Collection}
\label{sec:image_collection}

\subsection{B. Analysis of Challenges}
\label{sec:dataset_challenges}
```

```latex
% ❌ Bad: bare subsection titles without letter prefix; class will renumber but
%         the visual will look like "Overall Architecture" without "A." anchor
\section{Methodology}
\subsection{Overall Architecture}
% Reviewers reading the PDF jump to "A." in the bookmark, but the printed
% title is just "Overall Architecture", which is what got lost during copy-edit
```

```latex
% ❌ Bad: label placed before \section, breaks cleveref and PDF bookmarks
\label{sec:introduction}
\section{Introduction}
```

### Figure Placement

```latex
% ✅ Good: [!t] forces top placement; caption precedes label; IEEEtran order
\begin{figure}[!t]
  \centering
  \includegraphics[width=\linewidth]{figures/framework.pdf}
  \caption{Overall framework of the proposed method. The encoder
  integrates task-relevant information into a module to explicitly
  assign specific feature encoding to different requirements.}
  \label{fig:framework}
\end{figure}
```

```latex
% ❌ Bad: label before caption; no placement hint; full-textwidth in a two-column paper
\begin{figure}
  \centering
  \includegraphics[width=\textwidth]{figures/framework.pdf}
  \label{fig:framework}
  \caption{Overall framework of the proposed method.}
\end{figure}
```

### Equation Referencing

```latex
% ✅ Good: equation labeled so future prose can \cref{eq:foo}
\begin{equation}
  X_{temp} = (1 - \lambda \cdot \mathcal{G}) X_0 + (\lambda \cdot \mathcal{G}) X_{new}
  \label{eq:template_update}
\end{equation}
```

## Preamble Skeleton

```latex
% ✅ Good: minimal preamble for an IEEE journal paper
\documentclass[lettersize,journal]{IEEEtran}
\usepackage{amsmath, amssymb}
\usepackage{graphicx}
\usepackage{subcaption}
\usepackage{booktabs}
\usepackage{cleveref}
\usepackage{algorithm}
\usepackage{algorithmic}

\begin{document}
\title{Your Title Here}

\author{
  Author Name, \IEEEmembership{Member, IEEE,}
  \thanks{Manuscript received ...; revised ...; accepted ...}
  \thanks{... corresponding author: ...}
}

\maketitle

\begin{abstract}
...
\end{abstract}

\begin{IEEEkeywords}
keyword1, keyword2, keyword3
\end{IEEEkeywords}
```

## Benefits

- **Compile safety**: Sticking to `IEEEtran` defaults avoids silent class/option conflicts that break PDF output
- **Reviewer-friendly**: Clean, predictable sectioning lets reviewers jump straight to equations or figures
- **Reusability**: A canonical preamble + bibliography can be cloned across submissions with minimal edits
- **Roman-numeral + alphabetic-subsection consistency**: Authoring the letter prefix in `\subsection{}` ensures the rendered PDF matches what reviewers expect

## Related Skills

- [rule-academic-writing-latex-citations-and-cross-refs](../latex-citations-and-cross-refs/SKILL.md) - Citation and `\cref{}` mechanics
- [rule-academic-writing-latex-figures-and-tables](../latex-figures-and-tables/SKILL.md) - Figure/table caption and label conventions
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Tone of voice across all sections

## Remember

- `IEEEtran` is opinionated; override it as little as possible
- `\section{Introduction}` (mixed case), class renders as `I. INTRODUCTION`
- `\subsection{A. Overall Architecture}` (letter prefix + period + title)
- Labels go *after* the thing they label, never before
- The preamble is shared ground — coordinate package changes with co-authors before editing