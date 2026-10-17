---
name: methodology-ieee
description: "Methodology drafting with ordered module descriptions, source attribution, equation interpretation, and supported design takeaways"
metadata:
  migrated-from: "methodology-ieee.mdc"
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

# Methodology Writing

> **Note**: Use this skill when drafting/revising `\section{Methodology}` or `\section{Method}`.
> The subsection and closing Remark pattern is a project preference, subject to the actual manuscript and venue.

## Core Principle

The Methodology reads top-down as a sequence of logically ordered subsections.
Use plain subsection titles and let the document class generate their numbering.
Close a substantive module subsection with a short numbered Remark when it has a supported design takeaway.
For a descriptive subsection without such a takeaway, use a concise transition instead.

```
[Architecture figure, full-width at top of page]
\subsection{Overall Architecture}        → ends with Remark 1
\subsection{<Module 1>}                  → ends with Remark 2
\subsection{<Module 2>}                  → ends with Remark 3
\subsection{<Upsampler / Loss / Pipeline>} → ends with Remark N
```

Use the manuscript's existing Remark environment, or the optional labeled helper in [proof and design intent](../latex-proof-and-design-intent/SKILL.md#numbered-remark-implementation), before using `\methodremark` from the examples.

## Constants

- **SUBSECTION_PATTERN**: `\subsection{<Title>}` with class-generated numbering.
- **REMARK_PATTERN**: `\methodremark{rem:...}` or the existing template environment - Bold opener, period after the number, then 2-4 sentences.
  Numbered consecutively across the whole Methodology section.
- **DESIGN_INTENT_PATTERN**: `\textbf{Design Intent:}` - Use for equation interpretation that crosses subsections.
  Rare in practice.

## Rules

### ✅ DO

- Place the architecture diagram near the section opening and reference it with the manuscript's selected cross-reference command.
  Use a descriptive caption and a `\label{fig:framework}` anchor, choosing width from the actual layout.
- Open Subsection A with an *element equation line*: `Output = Network(Input)` to anchor the entire forward flow symbolically
- Order subsections so each **builds on** the previous one: overview → encoder → decoder/loss
- When a named existing method or component is used, place its source citation immediately after its name, before the implementation explanation.
- Close each substantive module subsection with a concise Remark when the design takeaway is supported, usually 2-4 sentences.
  Skip a redundant Remark for a purely descriptive subsection.
- Use equations inside subsections with `\cref{eq:xxx}`.
  The equation is the subsection's claim, the Remark below is the interpretation
- Place a single Algorithm block (e.g. `Algorithm 1`) at the end of the *last* methodology subsection that contains pseudo-code

### ❌ AVOID

- Do not open the methodology with a wall of equations — start with the architecture diagram + Equation (1) of the overall flow
- Do not add deeper heading levels unless the argument needs them and the template supports them.
- Do not bury the architecture diagram at section end.
  Reviewers expect it as the first visual anchor
- Do not leave a non-trivial equation uninterpreted, using inline explanation or a closing Remark as appropriate.
- Do not write "it is easy to see that" / "obviously" — use a `Remark N.` block instead
- Do not assign a fixed Remark number to each subsection regardless of whether a Remark is present.
  Number the Remarks actually used consecutively across the Methodology section.

## Patterns

### A./B./C./D. Subsections Closed by Remark N.

```latex
% ✅ Good: A/B/C/D subsections, each closed by a Remark N. paragraph
\section{Methodology}
\label{sec:method}

\begin{figure}[!t]
  \centering
  \includegraphics[width=\linewidth]{framework.pdf}
  \caption{Overall architecture of the proposed method.
  The encoder integrates task-relevant information to explicitly assign specific feature encoding to different requirements, enabling more accurate and flexible representation.
  The upsampler reconstructs the output from the deep latent code.}
  \label{fig:framework}
\end{figure}

\subsection{Overall Architecture}
\label{sec:overall}
As illustrated in \cref{fig:framework}, the proposed \textbf{OurMethod} consists of two key components: the input encoder $E_X$ and the upsampler $U$.
Given an input signal $I \in \mathbb{R}^{h \times w \times c}$, where $h$ and $w$ denote the height and width, the encoder extracts deep latent features.
This process is denoted as follows:
\begin{equation}
  E_{out} = E_X(I)
  \label{eq:encoder}
\end{equation}

\methodremark{rem:encoder} The input encoder is designed to generate accurate and adaptive representations tailored for varying conditions.
The upsampler reconstructs the output at the corresponding scale.

\subsection{Module A}
\label{sec:module_a}
In many existing methods, a critical challenge is ensuring that the model effectively adapts to varying conditions.
Traditional approaches typically rely on fixed feature extraction, making them ill-suited for dynamic requirements.
This limitation is particularly problematic in applications where inputs vary across conditions.
To address this, Module A is proposed, as shown in \cref{fig:module_a}.
\begin{equation}
  F_{out} = \mathrm{Linear}(F_{in,1} \cdot F_{in,2}) + F_{task}
  \label{eq:module_a}
\end{equation}

\methodremark{rem:module_a} By modulating features based on task-relevant signals, Module A learns to differentiate and emphasize task-dependent features, thereby improving scalability and reconstruction quality.

\subsection{Module B}
\label{sec:module_b}
The proposed Module B builds upon Module A.
Module B introduces a residual branch to further enhance feature representation by dynamically learning adaptive weights, as shown in \cref{fig:module_b}.
\ldots
\begin{equation}
  F = \mathrm{Linear}\!\left(\sum_{i=1}^{n} W^{i}_{kernel} \cdot W_{i};
  F_{in}\right) + F^M_{out}
  \label{eq:module_b}
\end{equation}

\methodremark{rem:module_b} By incorporating the adaptive branch, Module B enhances the modeling capability, ensuring that the extracted features are task-aware and adaptive.

\subsection{Upsampler}
\label{sec:upsampler}
Traditional upsampling methods typically utilize the areas between the target point and its surrounding points to weight latent codes.
While this method is computationally simple, it fails to fully capture complex interactions, resulting in limited detail representation.
To address this, an upsampler is designed.
\ldots
\begin{equation}
  w_{ij} = \phi(d_{ij}) = \exp\!\left(-\frac{d^{2}_{ij}}{2\sigma^{2}}\right)
  \label{eq:rbf}
\end{equation}
\ldots Finally, the output $O$ can be calculated as:
\begin{equation}
  O = O^{HF} + \mathrm{BI}(I)
  \label{eq:final}
\end{equation}
where $\mathrm{BI}$ denotes bilinear interpolation.
The complete algorithm flow is shown in Algorithm~\ref{alg:upsampler}.

\methodremark{rem:upsampler} By explicitly learning feature space weights and embedding spatial information, the upsampler enhances spatial interpretation and accurately reconstructs fine-grained details.
```

```latex
% ❌ Bad: subsection without Remark closing; equations dropped with no interpretation
\subsection{Module-Name}
% Five paragraphs of prose, equations buried, no diagram reference, no Remark
```

### Preliminaries (Mathematical Notation Block)

```latex
% ✅ Good: each symbol declared exactly once before its first use
\subsection{Preliminaries and Notation}
Let $I \in \mathbb{R}^{h \times w \times c}$ denote the input signal, where $h$ and $w$ represent its height and width, respectively.
The latent encoding produced by the encoder is $E_{out} \in \mathbb{R}^{h \times w \times d}$, with $d$ denoting the feature dimension.
The task parameter is denoted as $s \in \mathbb{R}^{k}$.
The output coordinates are $x_q \in X_{out}$, and the input coordinates are $x \in X_{in}$.
```

```latex
% ❌ Bad: symbols introduced ad-hoc in flow
% "We use $X$ for the template and $Y$ for the text and $Z$ for the
%  region. Symbols will be introduced as needed."
```

## Examples

### ✅ Good Remark N. Opener

> "**Remark 2.**
> By modulating features based on task-relevant signals, Module A learns to differentiate and emphasize task-dependent features, thereby improving scalability and reconstruction quality."

### ✅ Good Equation Interpretation (above the Remark)

> "$\sigma$ is modeled as a positive learnable parameter.
> The parameter $\sigma$ regulates the rate at which the weight decays with respect to the distance $d$.
> An excessively large $\sigma$ renders the weight less sensitive to variations in $d$, \ldots"

### ❌ Bad Subsection End

> "% ... equation dropped with no interpretation, no Remark ..."

## Benefits

- **Self-contained reading**: An expert in the field but not the specific topic can follow from the architecture diagram and Equation (1) onward
- **Equation-to-claim traceability**: Each subsection's Remark maps to a specific equation and a downstream ablation row
- **Reviewer auditability**: A subsection ends with a Remark makes the section easy to skim — reviewers re-read only the Remarks

## Related Skills

- [rule-academic-writing-latex-math-notation](../latex-math-notation/SKILL.md) - Notation discipline feeds Methodology clarity
- [rule-academic-writing-latex-proof-and-design-intent](../latex-proof-and-design-intent/SKILL.md) - Inline interpretation and supported subsection-closing Remarks
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - IEEEtran default Roman-numeral + alphabetic subsection numbering

## Remember

- Architecture diagram near the section opening, with a descriptive caption and stable label
- Plain subsection titles via `\subsection{<Title>}`, with numbering supplied by the class
- Close substantive module subsections with a supported design takeaway and a numbered Remark when appropriate.
- No `Design Intent:` blocks by default — use `Remark N.` for both intent and interpretation
