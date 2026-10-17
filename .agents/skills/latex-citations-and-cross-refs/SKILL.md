---
name: latex-citations-and-cross-refs
description: "Citation and cross-reference conventions for IEEE-style LaTeX papers"
metadata:
  migrated-from: "latex-citations-and-cross-refs.mdc"
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

# Citations and Cross-References

> **Note**: Apply to bibliography citations and cross-references in the actual manuscript and template.
> Inspect the bibliography files, reference commands, and loaded packages before editing.

## Core Principle

Citations and cross-references are part of the prose.
Cite precisely, label predictably, and let the macros do the work.

## Constants

- **BIB_FILE**: the manuscript's actual bibliography file or files, commonly `references.bib`.
- **CROSS_REFERENCE_COMMAND**: the convention supported by the venue and preamble, such as `\cref{}` or `Fig.~\ref{}` / `\eqref{}`.

## Rules

### ✅ DO

- Cite claims that build on prior work and distinguish them from author-provided results.
- **Place the citation immediately after a specific method's name**, as in `Transformer \cite{vaswani2017attention}`.
  Put the method name and citation on the same physical source line, before descriptive text or the next clause.
- Cite each distinct named method separately when several methods occur in one sentence.
  Group keys in one `\cite{a,b,c}` only for the same named method or a shared general claim without distinct named methods.
- Follow the manuscript's chosen cross-reference convention consistently.
  Use `\cref{}` only when `cleveref` is loaded and configured for the venue, or use the template's explicit prefixes with `\ref{}` / `\eqref{}`.
- Add a `\label{}` to every numbered section, equation, figure, and table
- Let the venue's bibliography style determine reference ordering, rather than choosing an arbitrary order.

### ❌ AVOID

- Do not write `[1]` inline manually — let BibTeX numbering do it
- Do not duplicate bibliography entries inline when the manuscript already uses a bibliography source.
  Follow the template if it explicitly uses `thebibliography`.
- Do not move the citation for a named method to the sentence end or combine distinct method references into an ambiguous shared citation.
- Do not invent citation keys, source metadata, or unsupported links between a method and a reference.
- Do not refer to figures as "the figure above" or "the table on the next page".
  `\cref{}` is exact
- Do not write "Ref. [3]" or "Reference (4)".
  The class will format it correctly via `\cite{}`

## Patterns

### Inline Citation

```latex
% ✅ Good: the citation immediately follows the named method.
Transformer \cite{vaswani2017attention} is used as the backbone.
```

```latex
% ❌ Bad: the citation is detached from the specific method name.
Transformer is used as the backbone \cite{vaswani2017attention}.
```

```latex
% ✅ Good: each distinct method is mapped to its own source.
Method A \cite{ref_method_a} and Method B \cite{ref_method_b} are compared under the same protocol.
```

```latex
% ❌ Bad: the grouped citation obscures which source belongs to which method.
Method A and Method B are compared under the same protocol \cite{ref_method_a,ref_method_b}.
```

```latex
% ✅ Good: grouping is appropriate for a general claim without named methods.
Cross-modal tracking builds on open-vocabulary detection \cite{ref_detection_a,ref_detection_b}.
```

### Cross-References

```latex
% ✅ Good: \cref auto-detects the type ("Figure 3", "Section 4.2", "Equation (5)")
As shown in \cref{fig:framework}, the SE-UpdateNet module sits between the visual encoder and the tracking head.
The gating mechanism in \cref{eq:gate} prevents unreliable updates.
```

```latex
% ❌ Bad: hard-coded figure/section labels; breaks on reorder
As shown in Figure 3, the SE-UpdateNet module sits between the visual encoder and the tracking head; the gating mechanism in Eq. (5) prevents unreliable updates.
```

## Benefits

- **Refactor-resilient**: `\cref{}` updates automatically when sections/figures move
- **Attribution**: Immediate method citations make the method-to-source mapping clear.
- **Style compliance**: Class-defined bibliography style is preserved when BibTeX entries live in `{BIB_FILE}`

## Related Skills

- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Defines document class and `\label{}` placement
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Avoids "we cite [3,4,5]" prose patterns

## Remember

- Cite a specific method immediately after its name.
- Group keys only when their attribution is shared and unambiguous.
- For floats, place `\label{}` immediately after `\caption{}`.
- Use the actual template's cross-reference commands and bibliography style.
