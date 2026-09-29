---
name: rebuttal
description: "Rebuttal letter conventions for IEEE peer-review (per-reviewer structure, evidence-based responses)"
metadata:
  migrated-from: "rebuttal.mdc"
  source-always-apply: "false"
  source-globs: ""
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source rule had no file glob; Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Rebuttal Letter Writing

> **Note**: Use this skill when responding to reviewer comments on an IEEE submission. Built from `8-Rebuttal.md`.

## Core Principle

A rebuttal is per-reviewer and per-comment. Each reviewer comment is acknowledged, answered with concrete evidence (figure/table/section/line number), and the eventual change is stated explicitly. Polite but firm.

## Constants

- **RESPONSE_PREFIX**: `R{X}.{Y}:` - Per-reviewer response heading (e.g. `R2.3:` for reviewer 2 comment 3).
- **EVIDENCE_PATTERN**: `Section~\ref{sec:...}` / `Eq.~\ref{eq:...}` / `Fig.~\ref{fig:...}` - Always cite the concrete location of the change.

## Rules

### ✅ DO

- Start with `We thank the reviewer for the constructive comment.`
- Open a new line for every reviewer comment (`R1.1`, `R1.2`, ...) so authors can navigate easily
- Provide concrete evidence: `\cref{}` to the section/equation/figure that was added or modified
- If you did not address a comment, say why explicitly; do not silently skip
- Re-run experiments if a comment asks for them, even if it costs a day

### ❌ DON'T

- Don't open with "We apologize for the limitations of our work..." — never apologize for the work
- Don't argue a reviewer is wrong; show evidence that addresses the concern
- Don't promise to do work "in the future" without specifying the change
- Don't write a one-sentence dismissal like "We disagree"; cite evidence and explain

## Patterns

### Standard Response

```latex
% ✅ Good: thank → restate → evidence → concrete change
\textbf{R2.3: What evidence supports the claim that SE-UpdateNet reduces
template drift, beyond the Anti-UAV benchmark?}

We thank the reviewer for raising this. We have now added a dedicated
ablation on the DTB70 benchmark that confirms the same trend:
removing SE-UpdateNet drops Success by 8.2 points, comparable to
the 10-point drop observed on Anti-UAV (see the new row in
Table~\ref{tab:ablation_dtb70}). The corresponding paragraph in
Sect.~\ref{sec:exp} now reads: ``The semantic-consistency gate
contributes a consistent 8-10 point Success gain across both
benchmarks, suggesting that the mechanism generalizes beyond
Anti-UAV-specific characteristics.''
```

```latex
% ❌ Bad: dismissive, no evidence, vague future
\textbf{R2.3:}
We think this is correct but our method is good. We will improve
it in future work.
```

### Reference Insertion

```latex
% ✅ Good: clarification via additional citations and revisited claim
\textbf{R3.2: The paper should better position itself against recent
vision-language tracking work.}

We thank the reviewer for the suggestion. We have extended Sect.~\ref{sec:related}
with three additional citations~\cite{memvlt_neurips2024,
atctrack_iccv2025, cldtracker_2025}, and added a closing paragraph in
Sect.~\ref{sec:intro} that explicitly contrasts MAE-OVT's
semantic-consistency gate with COVTrack++'s adaptive multi-cue
fusion. The contrast is summarized in the new Remark~1 in
Sect.~\ref{sec:se_updatenet}.
```

## Examples

### ✅ Good Tone

> "We thank the reviewer for this thoughtful observation. We have
> added the following experiment: ..."

### ❌ Bad Tone

> "We respectfully disagree with this comment. The reviewer appears to
> have overlooked the fact that our method is fundamentally different
> from prior works..."

## Anti-Patterns

- **Deflection-only responses**: "We will improve this in the final version" without specifying what and where
- **Multi-page rambling**: Each comment answered in ≤ 300 words; brevity wins
- **Identity disputes**: Disputing whether a reviewer is correct — instead, present evidence

## Benefits

- **Editorial processing**: Rebuttals structured as `R{X}.{Y}:` let editors paste into decision letters
- **Argument auditability**: Concrete `\cref{}` references make each claim verifiable
- **Professional reputation**: Polite, evidence-based tone prevents reviewer retaliation

## Related Skills

- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Avoid "I'm sorry" and apologetic openers
- [rule-academic-writing-experiments-ieee](../experiments-ieee/SKILL.md) - Additional ablation tables often appear during rebuttal

## Remember

- Every comment: thank, restate, evidence, concrete change
- Cite `\cref{}` of the section/equation/figure that changed
- Never apologize for the work; argue with evidence