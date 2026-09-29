---
name: latex-math-notation
description: "Mathematical notation conventions for IEEE-style LaTeX papers"
metadata:
  migrated-from: "latex-math-notation.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Mathematical Notation

> **Note**: Applies to `main.tex` whenever mathematical content dominates (methodology / experiments / supplementary). Borrowed from the conventions of `IEEEtran` papers in CV/remote-sensing.

## Core Principle

Notation must be consistent across the paper: same symbol means the same thing, different symbols look different. Document every new symbol in the Preliminaries subsection before using it.

## Constants

- **NOTATION_FILE**: `notation.tex` (optional) - Centralized symbol definitions, included via `\input{notation.tex}`.

## Rules

### ✅ DO

- Use `\mathcal{}` for sets and random variables: $\mathcal{V}$, $\mathcal{M}$, $\mathcal{T}$
- Use `\mathbf{}` for matrices and vector-valued bold symbols: $\mathbf{F}$, $\mathbf{Y}$
- Use `\mathrm{}` for operator names: `\mathrm{GAP}`, `\mathrm{MLP}`, `\mathrm{UpdateNet}`
- Use `\mathbf{R}^{n\times m}` (or `\mathbb{R}^{n\times m}`) for vector spaces, consistently throughout
- Define each new symbol the first time it appears in the Preliminaries subsection; reuse without redefinition elsewhere

### ❌ DON'T

- Don't mix italic (`$x$`) and upright (`$\mathrm{x}$`) for function/operator names — pick one
- Don't overload symbols: if `$X$` is a feature map and `$X_0$` is the initial feature map, do not also use `$X_0$` for "the first method"
- Don't typeset brackets and parens inconsistently: stick with `[\cdot;\cdot]` for concatenation
- Don't write multi-line inline formulas when `\begin{equation}` is available

## Patterns

### Operator Naming

```latex
% ✅ Good: upright operators, gap with mathrm, clear concatenation
\begin{equation}
  \mathcal{G}
  = \sigma\!\left(\mathrm{MLP}\!\left([\mathrm{GAP}(X_t);\, \mathbf{Y}]\right)\right),
  \label{eq:gate}
\end{equation}
```

```latex
% ❌ Bad: italic operator names, ambiguous separators
\begin{equation}
  G = \sigma (MLP ([GAP(X_t), Y])),
  \label{eq:gate}
\end{equation}
% GAP, MLP become italic math variables, blending in with features
```

### Set and Sequence Notation

```latex
% ✅ Good: video as sequence, indexed symbolically
Let $\mathcal{V} = \{I_0, I_1, \ldots, I_T\}$ denote an input video
sequence with $T + 1$ frames.
```

```latex
% ❌ Bad: variable-name overload for set vs sequence
Let $V = \{I_0, ..., I_T\}$ denote an input video sequence.
% Bold mathcal disappears; loses the "set" affordance
```

## Benefits

- **Clarity**: `\mathbf{}` vs `\mathcal{}` vs `\mathrm{}` makes logic visible at a glance
- **Refactor safety**: Notation declared once in Preliminaries is easy to update paper-wide
- **Reviewer trust**: Consistent symbols signal discipline; mismatched notation is a common complaint

## Related Skills

- [rule-academic-writing-latex-proof-and-design-intent](../latex-proof-and-design-intent/SKILL.md) - Design Intent paragraphs rely on this notation rule
- [rule-academic-writing-methodology-ieee](../methodology-ieee/SKILL.md) - Methodology subsection structure reinforces Preliminaries placement

## Remember

- Upright operators (`\mathrm{}`), italic features (`$X$`), bold matrices (`\mathbf{}`), calligraphic sets (`\mathcal{}`)
- Define a symbol before using it; do not redefine later
- Concatenation uses `[a; b]` semicolon, with thin spaces before/after