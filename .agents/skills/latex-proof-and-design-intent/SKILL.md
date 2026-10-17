---
name: latex-proof-and-design-intent
description: "Equation interpretation, proof sketches, and supported subsection-closing Remarks for methodology writing"
metadata:
  migrated-from: "latex-proof-and-design-intent.mdc"
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

# Proof and Design Intent Conventions

> **Note**: Apply when methodology needs equation interpretation, proof sketches, or design takeaways.
> Numbered closing Remarks are a project preference, with inline explanations used where they fit better.

## Core Principle

A new equation or module-sub-section earns its place when the author explains *why*.
Every non-trivial formula is followed by **either** a sentence-level interpretation **or** — for module sub-sections — a numbered **`Remark N.`** paragraph that summarizes the design lever.

```
\begin{equation} ... \label{eq:foo} \end{equation}
[2-3 sentences interpreting eq:foo inline, then transition to next equation]
                                  ← No dedicated block if the next paragraph continues the topic.

OR (when the entire subsection ends here)

\textbf{Remark N.} The <module X> learns to differentiate
<property Y>, thereby improving <metric Z>.
```

## Constants

- **REMARK_PATTERN**: `\textbf{Remark N.}` - Bold opener, period after the number, then 2-4 sentences.
  Numbered consecutively across the whole Methodology section.
- **REMARK_COUNTER_INIT**: 1 for the first Remark actually used in the Methodology section, continuing consecutively across subsections.
- **DESIGN_INTENT_PATTERN**: `\textbf{Design Intent:}` - Reserved for equation interpretation that crosses subsections.
  Rare in practice.

## Rules

### ✅ DO

- Use a numbered Remark for a substantive subsection's supported design takeaway, skipping redundant Remarks for descriptive subsections.
- For an *intermediate* equation inside a sub-section, use **2-3 sentences of inline interpretation** immediately after the equation.
  *do not* start a numbered Remark mid-subsection
- Use Remark 1, 2, 3, ... consecutively for the Remarks that are actually present.
  Reuse the template's Remark environment or use a counter and label, rather than manually maintaining numbers that are cross-referenced.
- Reference the corresponding equation inside the Remark: *"in \cref{eq:rbf}, $\sigma$ acts as a learnable distance scale"*
- Use `\textbf{Proof sketch:}` when only the gist of a proof is needed.
  Reserve `\begin{proof}` for full formal correctness
- Keep each Remark to **2-4 sentences**.
  Longer interpretation belongs to a separate paragraph

### ❌ AVOID

- Do not skip, repeat, or reset Remark numbers within the Methodology section.
  Start the first Remark at 1 and reset its counter at the section boundary.
- Do not drop an equation without any comment — at minimum, write *"Equation (\ref{eq:foo}) reveals that ..."*
- Do not write *"it is easy to see that..."* or *"obviously"* before a non-trivial step — this signals hand-waving
- Do not put a Remark **before** the equation it interprets — the equation should be self-contained first
- Do not exceed 4 sentences in a single Remark.
  Long exposition belongs in `\begin{proof}` or supplementary

## Patterns

### Equation With Inline Interpretation

```latex
% ✅ Good: equation labeled, 2-3 sentences of inline interpretation,
% followed by transition, NOT a numbered Remark in the middle
\begin{equation}
  w_{ij} = \phi(d_{ij}) = \exp\!\left(-\frac{d^{2}_{ij}}{2\sigma^{2}}\right)
  \label{eq:rbf}
\end{equation}
where $i$ and $j$ index spatial positions and $d_{ij}$ denotes their Euclidean distance.
The positive scale $\sigma$ is learned during training.
The parameter $\sigma$ regulates the rate at which the weight decays with respect to the distance $d_{ij}$.
For a larger $\sigma$, the weight varies more slowly with distance.
For a smaller $\sigma$, the weight decays more sharply with distance.
For finite $d_{ij}$ and $\sigma > 0$, the Gaussian weight satisfies $0 < w_{ij} \leq 1$.
```

### Subsection Closing with Remark N.

```latex
% ✅ Good: equation + transition + Subsection closing Remark 4.
\begin{equation}
  O = O^{HF} + \mathrm{BI}(I)
  \label{eq:final}
\end{equation}
where $\mathrm{BI}$ denotes bilinear interpolation.
The complete algorithm flow is shown in Algorithm~\ref{alg:upsampler}.

\methodremark{rem:upsampler} By explicitly learning feature space weights and embedding spatial information into the local feature ensemble, the upsampler enhances the ability to interpret spatial relationships and accurately reconstruct fine-grained details.
```

```latex
% ❌ Bad: equation dropped without interpretation, no Remark
\begin{equation}
  X_{temp} = (1 - \lambda \cdot \mathcal{G}) X_0 + (\lambda \cdot \mathcal{G}) X_{new}
\end{equation}

Then we update the template.
```

### Inline `\textbf{Design Intent:}` Block (rare, only when the equation interpretation crosses subsections)

```latex
% ✅ Good: when a single Design Intent paragraph bridges two subsections
\textbf{Design Intent:} The gating mechanism $\mathcal{G}$ serves as a reliability measure for the current visual observation.
When the input is occluded, blurred, or experiences severe appearance changes, the visual feature may diverge from the expected pattern.
In such cases, $\mathcal{G}$ approaches $0$, preventing unreliable updates from contaminating the representation.
```

```latex
% ❌ Bad: missing number, vague opener
It is obvious that the gating is different from prior approaches.
% "Obviously" preempts the reader; no number to \cref from
```

## Numbered Remark Implementation

Reuse an existing template environment when available.
For a plain bold opener with automatic numbering, the following optional helper belongs in the preamble:

```latex
\newcounter{methodremark}[section]
\renewcommand{\themethodremark}{\arabic{methodremark}}
\newcommand{\methodremark}[1]{%
  \par\refstepcounter{methodremark}%
  \noindent\textbf{Remark \themethodremark.}\label{#1}\enspace
}
```

Use `\methodremark{rem:upsampler}` before its interpretation paragraph.
If `cleveref` is used, register this counter with `\crefname{methodremark}{Remark}{Remarks}` after loading the package.
Do not redefine an environment or helper that the manuscript already provides.

## Remark N. vs Design Intent Decision Tree

```
Does the current subsection end with a supported design takeaway?
├── YES → Use a concise numbered Remark if the manuscript uses this convention.
└── NO  → Does an explanation need to connect multiple equations or subsections?
          ├── YES → Use a focused design-intent paragraph when useful.
          └── NO  → Explain the equation inline without a numbered block.
```

## Examples

### ✅ Good Remark N. Opener

> "**Remark 4.**
> By explicitly learning feature space weights and embedding spatial information into the local feature ensemble, the upsampler enhances the ability to interpret spatial relationships and accurately reconstruct fine-grained details."

### ✅ Good Inline Equation Interpretation

> "The Gaussian function is popular for its smoothness and effectiveness in interpolation tasks.
> Therefore, the weight is formulated as follows: ..."

### ❌ Bad Subsection End

> "% ... equation dropped with no interpretation, no Remark ..."

## Benefits

- **Reviewer trust**: A Remark N. paragraph shows engineering intent, not just math
- **Citation anchor**: Numbered Remarks provide reusable targets for `\cref{}`
- **Self-explanatory equations**: Without interpretation, an equation is a black box to cross-disciplinary readers
- **Convention**: Consistent use of Remarks keeps the project's design takeaways easy to find.

## Related Skills

- [rule-academic-writing-latex-math-notation](../latex-math-notation/SKILL.md) - Notation discipline feeds Remark readability
- [rule-academic-writing-methodology-ieee](../methodology-ieee/SKILL.md) - Methodology layout and supported module-closing Remarks

## Remember

- Equation first, then interpretation — never reverse
- Use numbered Remarks for supported design takeaways and inline explanations elsewhere.
- `Design Intent:` is reserved for interpretation that crosses subsections (rare)
- 2-4 sentences max in a single Remark
- Reset the counter at the Methodology section boundary and number the Remarks actually used consecutively.
