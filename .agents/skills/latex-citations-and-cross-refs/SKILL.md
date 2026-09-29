---
name: latex-citations-and-cross-refs
description: "Citation and cross-reference conventions for IEEE-style LaTeX papers"
metadata:
  migrated-from: "latex-citations-and-cross-refs.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Citations and Cross-References

> **Note**: Applies to `main.tex` whenever `IEEEtran` is in use and `references.bib` is the canonical bib source. Assumes the `cleveref` package is loaded for forward references.

## Core Principle

Citations and cross-references are part of the prose. Cite precisely, label predictably, and let the macros do the work.

## Constants

- **BIB_FILE**: `references.bib` - Single BibTeX source for `\cite{}` calls.
- **CLEVEREF_PREFIX**: `cleveref` - Use `\cref{}` for figures / sections / equations after `\usepackage{cleveref}`.

## Rules

### ✅ DO

- Cite every claim that builds on prior work; no result appears from nowhere
- Group multiple citations into one `\cite{a,b,c}` rather than `\cite{a}\cite{b}\cite{c}`
- Use `\cref{fig:...}`, `\cref{sec:...}`, `\cref{eq:...}` consistently — never mix with `\ref{}`
- Add a `\label{}` to every numbered section, equation, figure, and table
- Sort references by appearance order or alphabetically — pick one and stick to it

### ❌ DON'T

- Don't write `[1]` inline manually — let BibTeX numbering do it
- Don't drop BibTeX entries into `main.tex` as inline `\bibitem{}`; keep `{BIB_FILE}` as the single source
- Don't refer to figures as "the figure above" or "the table on the next page"; `\cref{}` is exact
- Don't write "Ref. [3]" or "Reference (4)"; the class will format it correctly via `\cite{}`

## Patterns

### Inline Citation

```latex
% ✅ Good: bundled citation, exact key
Cross-modal tracking inherits from open-vocabulary detection
\cite{li2022glip, liu2024groundingdino, cheng2024yoloworld}.
```

```latex
% ❌ Bad: stacked single-key citations; harder to reorder
Cross-modal tracking inherits from open-vocabulary detection
\cite{li2022glip}\cite{liu2024groundingdino}\cite{cheng2024yoloworld}.
```

### Cross-References

```latex
% ✅ Good: \cref auto-detects the type ("Figure 3", "Section 4.2", "Equation (5)")
As shown in \cref{fig:framework}, the SE-UpdateNet module sits between
the visual encoder and the tracking head; the gating mechanism
in \cref{eq:gate} prevents unreliable updates.
```

```latex
% ❌ Bad: hard-coded figure/section labels; breaks on reorder
As shown in Figure 3, the SE-UpdateNet module sits between the visual
encoder and the tracking head; the gating mechanism in Eq. (5) prevents
unreliable updates.
```

## Benefits

- **Refactor-resilient**: `\cref{}` updates automatically when sections/figures move
- **Reviewer-friendly**: Single `\cite{}` with multiple keys produces a tighter reference list
- **Style compliance**: Class-defined bibliography style is preserved when BibTeX entries live in `{BIB_FILE}`

## Related Skills

- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Defines document class and `\label{}` placement
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Avoids "we cite [3,4,5]" prose patterns

## Remember

- Group multi-cites with commas in one `\cite{}`
- `\label{}` goes immediately after the `\caption{}`, never before
- `\cref{}` replaces "Figure X" / "Section Y" / "Equation (Z)"