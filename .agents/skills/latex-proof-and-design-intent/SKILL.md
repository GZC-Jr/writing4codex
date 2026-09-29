---
name: latex-proof-and-design-intent
description: "Remark N. closing-paragraph convention — every non-trivial equation/subsection is closed by a numbered Remark"
metadata:
  migrated-from: "latex-proof-and-design-intent.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Proof and Design Intent Conventions

> **Note**: Applies to `main.tex` whenever Methodology uses inline proofs or interpretive paragraphs. The canonical pattern is `\textbf{Remark N.}` rather than `\textbf{Design Intent:}` — every non-trivial equation or module-sub-section closes with a numbered Remark.

## Core Principle

A new equation or module-sub-section earns its place when the author explains *why*. Every non-trivial formula is followed by **either** a sentence-level interpretation **or** — for module sub-sections — a numbered **`Remark N.`** paragraph that summarizes the design lever.

```
\begin{equation} ... \label{eq:foo} \end{equation}
[2-3 sentences interpreting eq:foo inline, then transition to next equation]
                                  ← No dedicated block if the next paragraph continues the topic.

OR (when the entire subsection ends here)

\textbf{Remark N.} The <module X> learns to differentiate
<property Y>, thereby improving <metric Z>.
```

## Constants

- **REMARK_PATTERN**: `\textbf{Remark N.}` - Bold opener, period after the number, then 2-4 sentences. Numbered consecutively across the whole Methodology section.
- **REMARK_COUNTER_INIT**: 1 - Remark numbering starts at 1 in the first methodology subsection; the counter is **section-scoped**, not document-scoped.
- **DESIGN_INTENT_PATTERN**: `\textbf{Design Intent:}` - Reserved for equation interpretation that crosses subsections; rare in practice.

## Rules

### ✅ DO

- Use **Remark N.** as the canonical closer for each methodology sub-section (`\subsection{A. ...}`, `\subsection{B. ...}`)
- For an *intermediate* equation inside a sub-section, use **2-3 sentences of inline interpretation** immediately after the equation; *do not* start a numbered Remark mid-subsection
- Use Remark 1, 2, 3, ... consecutively: Subsection A's closer is Remark 1, Subsection B's is Remark 2, etc.
- Reference the corresponding equation inside the Remark: *"in \cref{eq:rbf}, $\sigma$ acts as a learnable distance scale"*
- Use `\textbf{Proof sketch:}` when only the gist of a proof is needed; reserve `\begin{proof}` for full formal correctness
- Keep each Remark to **2-4 sentences**; longer interpretation belongs to a separate paragraph

### ❌ DON'T

- Don't start the methodology's first subsection at Remark 2; the counter resets at Subsection A
- Don't drop an equation without any comment — at minimum, write *"Equation (\ref{eq:foo}) reveals that ..."*
- Don't write *"it is easy to see that..."* or *"obviously"* before a non-trivial step — this signals hand-waving
- Don't put a Remark **before** the equation it interprets — the equation should be self-contained first
- Don't exceed 4 sentences in a single Remark; long exposition belongs in `\begin{proof}` or supplementary

## Patterns

### Equation With Inline Interpretation

```latex
% ✅ Good: equation labeled, 2-3 sentences of inline interpretation,
% followed by transition, NOT a numbered Remark in the middle
\begin{equation}
  w_{ij} = \phi(d_{ij}) = \exp\!\left(-\frac{d^{2}_{ij}}{2\sigma^{2}}\right)
  \label{eq:rbf}
\end{equation}
where $i$ and $j$ represent the index of the spatial position and $d$
represents the Euclidean distance. $\sigma$ is modeled as a learnable
parameter. After training, the learned $\sigma$ converges to 1.15.
The parameter $\sigma$ regulates the rate at which the weight decays
with respect to the distance $d$. An excessively large $\sigma$
renders the weight less sensitive to variations in $d$, \ldots
Conversely, an overly small $\sigma$ leads to an excessively sharp
decay, causing the weight to concentrate almost exclusively on the
nearest points while neglecting the contributions of slightly farther
neighbors. \ldots The advantage of using RBF is that, for any given
$d$, the predicted $w$ always lies between 0 and 1.
```

### Subsection Closing with Remark N.

```latex
% ✅ Good: equation + transition + Subsection closing Remark 4.
\begin{equation}
  O = O^{HF} + \mathrm{BI}(I)
  \label{eq:final}
\end{equation}
where $\mathrm{BI}$ denotes bilinear interpolation. The complete
algorithm flow is shown in Algorithm~\ref{alg:upsampler}.

\textbf{Remark 4.} By explicitly learning feature space weights and
embedding spatial information into the local feature ensemble, the
upsampler enhances the ability to interpret spatial relationships
and accurately reconstruct fine-grained details.
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
\textbf{Design Intent:} The gating mechanism $\mathcal{G}$ serves as
a reliability measure for the current visual observation. When the
input is occluded, blurred, or experiences severe appearance changes,
the visual feature may diverge from the expected pattern. In such
cases, $\mathcal{G}$ approaches $0$, preventing unreliable updates
from contaminating the representation.
```

```latex
% ❌ Bad: missing number, vague opener
It is obvious that the gating is different from prior approaches.
% "Obviously" preempts the reader; no number to \cref from
```

## Remark N. vs Design Intent Decision Tree

```
Is the interpretation about a SINGLE equation/methodology sub-section
and self-contained to it?
├── YES  → Use Remark N. as the subsection closer (default)
└── NO   → Does the interpretation span 2+ equations or 2+ subsections?
           ├── YES → Use \textbf{Design Intent:} block (rare)
           └── NO  → Use 2-3 inline sentences immediately after the equation
```

## Examples

### ✅ Good Remark N. Opener

> "**Remark 4.** By explicitly learning feature space weights and
> embedding spatial information into the local feature ensemble, the
> upsampler enhances the ability to interpret spatial relationships
> and accurately reconstruct fine-grained details."

### ✅ Good Inline Equation Interpretation

> "The Gaussian function is popular for its smoothness and effectiveness
> in interpolation tasks. Therefore, the weight is formulated as follows: ..."

### ❌ Bad Subsection End

> "% ... equation dropped with no interpretation, no Remark ..."

## Benefits

- **Reviewer trust**: A Remark N. paragraph shows engineering intent, not just math
- **Citation anchor**: Numbered Remarks provide reusable targets for `\cref{}`
- **Self-explanatory equations**: Without interpretation, an equation is a black box to cross-disciplinary readers
- **Convention**: `Remark N.` matches the standard methodology convention across top venues

## Related Skills

- [rule-academic-writing-latex-math-notation](../latex-math-notation/SKILL.md) - Notation discipline feeds Remark readability
- [rule-academic-writing-methodology-ieee](../methodology-ieee/SKILL.md) - Methodology layout (architecture diagram → A./B./C. subsections, each closed by a Remark)

## Remember

- Equation first, then interpretation — never reverse
- `Remark N.` is the **default closer** for every methodology subsection
- `Design Intent:` is reserved for interpretation that crosses subsections (rare)
- 2-4 sentences max in a single Remark
- The counter resets at 1 in Subsection A; subsequence-numbered across the Methodology section