---
name: methodology-ieee
description: "Methodology writing for CV/Robotics/IP top journals and conferences — A./B./C. subsections closed by numbered Remark N. paragraphs"
metadata:
  migrated-from: "methodology-ieee.mdc"
  source-always-apply: "false"
  source-globs: ""
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source rule had no file glob; Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Methodology Writing

> **Note**: Use this skill when drafting/revising `\section{Methodology}` (or `\section{Method}`) of a top-tier journal or conference paper. The A./B./C. subsection + closing `Remark N.` pattern is the dominant convention across IEEE T-PAMI, TIP, CVPR, ICCV, and related venues.

## Core Principle

The Methodology reads top-down as a sequence of **alphabetically named** subsections (`\subsection{Overall Architecture}`, `\subsection{Module A}`, ...). Each subsection is *closed* by a short paragraph beginning **`Remark N.`** that summarizes the design lever in plain English. The section closes with no Remark when the subsection has no clear single-sentence takeaway.

```
[Architecture figure, full-width at top of page]
\subsection{A. Overall Architecture}        → ends with Remark 1
\subsection{B. <Module 1>}                  → ends with Remark 2
\subsection{C. <Module 2>}                  → ends with Remark 3
\subsection{D. <Upsampler / Loss / Pipeline>} → ends with Remark N
```

## Constants

- **SUBSECTION_PATTERN**: `\subsection{<Cap.>.<Title>}` - Capital letter followed by period then title (IEEEtran default).
- **REMARK_PATTERN**: `\textbf{Remark N.}` - Bold opener, period after the number, then 2-4 sentences. Numbered consecutively across the whole Methodology section.
- **DESIGN_INTENT_PATTERN**: `\textbf{Design Intent:}` - Use for equation interpretation that crosses subsections; rare in practice.

## Rules

### ✅ DO

- Place the **architecture diagram** at the top of the section, full-width when possible, captioned `\cref{fig:framework}`
- Open Subsection A with an *element equation line*: `Output = Network(Input)` to anchor the entire forward flow symbolically
- Order subsections so each **builds on** the previous one: overview → encoder → decoder/loss
- End **every** methodology subsection with a **`Remark N.`** paragraph (3-4 sentences max); the Remark restates what the subsection *enabled*, not what it *is*
- Use equations inside subsections with `\cref{eq:xxx}`; the equation is the subsection's claim, the Remark below is the interpretation
- Place a single Algorithm block (e.g. `Algorithm 1`) at the end of the *last* methodology subsection that contains pseudo-code

### ❌ DON'T

- Don't open the methodology with a wall of equations — start with the architecture diagram + Equation (1) of the overall flow
- Don't use `\subsubsection`; most venue classes don't render it reliably in journal mode — go one level deep per module only
- Don't bury the architecture diagram at section end; reviewers expect it as the first visual anchor
- Don't end a subsection at an equation without a follow-up `Remark N.`
- Don't write "it is easy to see that" / "obviously" — use a `Remark N.` block instead
- Don't reuse Remark numbers across subsections; Remark 1 belongs to Subsection A, Remark 2 to Subsection B, etc.

## Patterns

### A./B./C./D. Subsections Closed by Remark N.

```latex
% ✅ Good: A/B/C/D subsections, each closed by a Remark N. paragraph
\section{Methodology}
\label{sec:method}

\begin{figure}[!t]
  \centering
  \includegraphics[width=\linewidth]{framework.pdf}
  \caption{Overall architecture of the proposed method. The encoder
  integrates task-relevant information to explicitly assign specific
  feature encoding to different requirements, enabling more accurate
  and flexible representation. The upsampler reconstructs the output
  from the deep latent code.}
  \label{fig:framework}
\end{figure}

\subsection{A. Overall Architecture}
\label{sec:overall}
As illustrated in \cref{fig:framework}, the proposed \textbf{OurMethod}
consists of two key components: the input encoder $E_X$ and the
upsampler $U$. Given an input signal $I \in \mathbb{R}^{h \times w \times c}$,
where $h$ and $w$ denote the height and width, the encoder extracts
deep latent features. This process is denoted as follows:
\begin{equation}
  E_{out} = E_X(I)
  \label{eq:encoder}
\end{equation}

\textbf{Remark 1.} The input encoder is designed to generate accurate
and adaptive representations tailored for varying conditions. The
upsampler reconstructs the output at the corresponding scale.

\subsection{B. Module A}
\label{sec:module_a}
In many existing methods, a critical challenge is ensuring that the
model effectively adapts to varying conditions. Traditional approaches
typically rely on fixed feature extraction, making them ill-suited for
dynamic requirements. This limitation is particularly problematic in
applications where inputs vary across conditions. To address this,
Module A is proposed, as shown in \cref{fig:module_a}.
\begin{equation}
  F_{out} = \mathrm{Linear}(F_{in,1} \cdot F_{in,2}) + F_{task}
  \label{eq:module_a}
\end{equation}

\textbf{Remark 2.} By modulating features based on task-relevant signals,
Module A learns to differentiate and emphasize task-dependent features,
thereby improving scalability and reconstruction quality.

\subsection{C. Module B}
\label{sec:module_b}
The proposed Module B builds upon Module A. Module B introduces a
residual branch to further enhance feature representation by
dynamically learning adaptive weights, as shown in \cref{fig:module_b}.
\ldots
\begin{equation}
  F = \mathrm{Linear}\!\left(\sum_{i=1}^{n} W^{i}_{kernel} \cdot W_{i};
  F_{in}\right) + F^M_{out}
  \label{eq:module_b}
\end{equation}

\textbf{Remark 3.} By incorporating the adaptive branch, Module B
enhances the modeling capability, ensuring that the extracted
features are task-aware and adaptive.

\subsection{D. Upsampler}
\label{sec:upsampler}
Traditional upsampling methods typically utilize the areas between
the target point and its surrounding points to weight latent codes.
While this method is computationally simple, it fails to fully
capture complex interactions, resulting in limited detail representation.
To address this, a novel upsampler is designed. \ldots
\begin{equation}
  w_{ij} = \phi(d_{ij}) = \exp\!\left(-\frac{d^{2}_{ij}}{2\sigma^{2}}\right)
  \label{eq:rbf}
\end{equation}
\ldots Finally, the output $O$ can be calculated as:
\begin{equation}
  O = O^{HF} + \mathrm{BI}(I)
  \label{eq:final}
\end{equation}
where $\mathrm{BI}$ denotes bilinear interpolation. The complete
algorithm flow is shown in Algorithm~\ref{alg:upsampler}.

\textbf{Remark 4.} By explicitly learning feature space weights and
embedding spatial information, the upsampler enhances spatial
interpretation and accurately reconstructs fine-grained details.
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
Let $I \in \mathbb{R}^{h \times w \times c}$ denote the input signal,
where $h$ and $w$ represent its height and width, respectively.
The latent encoding produced by the encoder is
$E_{out} \in \mathbb{R}^{h \times w \times d}$, with $d$ denoting the
feature dimension. The task parameter is denoted as $s \in \mathbb{R}^{k}$.
The output coordinates are $x_q \in X_{out}$, and the input coordinates
are $x \in X_{in}$.
```

```latex
% ❌ Bad: symbols introduced ad-hoc in flow
% "We use $X$ for the template and $Y$ for the text and $Z$ for the
%  region. Symbols will be introduced as needed."
```

## Examples

### ✅ Good Remark N. Opener

> "**Remark 2.** By modulating features based on task-relevant signals,
> Module A learns to differentiate and emphasize task-dependent
> features, thereby improving scalability and reconstruction quality."

### ✅ Good Equation Interpretation (above the Remark)

> "$\sigma$ is modeled as a learnable parameter. After training, the
> learned $\sigma$ converges to 1.15. The parameter $\sigma$ regulates
> the rate at which the weight decays with respect to the distance $d$.
> An excessively large $\sigma$ renders the weight less sensitive to
> variations in $d$, \ldots"

### ❌ Bad Subsection End

> "% ... equation dropped with no interpretation, no Remark ..."

## Benefits

- **Self-contained reading**: An expert in the field but not the specific topic can follow from the architecture diagram and Equation (1) onward
- **Equation-to-claim traceability**: Each subsection's Remark maps to a specific equation and a downstream ablation row
- **Reviewer auditability**: A subsection ends with a Remark makes the section easy to skim — reviewers re-read only the Remarks

## Related Skills

- [rule-academic-writing-latex-math-notation](../latex-math-notation/SKILL.md) - Notation discipline feeds Methodology clarity
- [rule-academic-writing-latex-proof-and-design-intent](../latex-proof-and-design-intent/SKILL.md) - Mandatory `Remark N.` closing each subsection
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - IEEEtran default Roman-numeral + alphabetic subsection numbering

## Remember

- Architecture diagram at the top of the section, captioned `\cref{fig:framework}`
- Subsections named `A.`, `B.`, `C.`, ... via `\subsection{<Cap>.<Title>}`
- Each non-trivial subsection ends with a `\textbf{Remark N.}` paragraph
- No `Design Intent:` blocks by default — use `Remark N.` for both intent and interpretation