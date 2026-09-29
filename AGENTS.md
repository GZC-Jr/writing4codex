# Academic Writing Project

## Scope

These instructions govern academic drafting, revision, translation, peer-review responses, LaTeX editing, citation work, figure/table preparation, and submission checks in this project. The original Cursor rules remain in the repository as `.mdc` source files; Codex uses the migrated skills under `.agents/skills/`.

## Instruction Precedence

- System and developer instructions always take precedence over this file.
- Follow the user's explicit deliverable, language, discipline, venue, and evidence constraints.
- Apply this file to every task in the project.
- Use a migrated skill only when its trigger matches the task. A skill adds detail; it does not weaken these baseline constraints.
- A named venue or provided template overrides generic IEEE defaults. When requirements conflict, report the conflict and follow the highest-priority applicable source.

## Evidence Integrity

- Never fabricate references, quotations, DOI or page numbers, datasets, participants, measurements, statistical values, experiments, code URLs, or findings.
- Do not claim that a source was searched, opened, verified, or cited unless that action actually occurred.
- Distinguish source-supported facts, author-provided claims, interpretation, hypothesis, and speculation.
- Preserve the original level of certainty, limitations, causal strength, and attribution when editing or translating.
- If required information is missing, use a clearly marked placeholder or report the missing item; do not silently fill it in.
- Do not silently add, delete, merge, or reorder references or results.

## Human Writing Baseline

This baseline is always active. The full examples and checklist remain in the `human-writing-style` skill.

- Write precise, varied, unforced prose that reads like a researcher wrote it under deadline. Open paragraphs with substantive claims, not empty transitions.
- Rotate sentence shapes within a paragraph: direct claim, although/while clause, consequence, causal `By X, Y`, and a concrete-number claim where the evidence supports one.
- Hedge with concrete limits and conditions rather than vague adverbs. Preserve uncertainty; never turn an estimate or hypothesis into a fact.
- Use field-standard vocabulary sparingly. Prefer `use`, `build on`, or `suitable` over buzzwords such as `leverage`, `delve into`, `tapestry`, `robust solution`, or `harness the power of`.
- Avoid repeated paragraph openers, emphatic adjectives (`crucial`, `vital`, `paramount`, `revolutionary`), apology phrases, passive stacking, Markdown punctuation, and emoji in LaTeX body text.
- Use specific numbers and named baselines when available. Keep `novel` to at most one occurrence in an abstract and use `leverage` zero times in academic prose unless it is a literal technical term.
- In methodology and related-work limitation paragraphs, use a causal explanation such as `By X, Y` when it accurately describes the mechanism; do not force the pattern when the evidence does not support it.

## Task Intake

Before writing or editing, identify (or state as unknown):

1. The requested operation: draft, revise, translate, compress, review, format, or rebut.
2. The manuscript section or artifact: abstract, introduction, related work, methodology, experiments, results, discussion, conclusion, references, rebuttal, figure, table, equation, or full paper.
3. Discipline, audience, target venue, document class, language, word/page limit, and citation style.
4. Which claims, data, sources, templates, and files are actually available and which require verification.

Do not block on a missing preference when a conservative assumption is reversible. State the assumption in the response and flag venue-specific items for confirmation.

## Skill Dispatch

Use the smallest set of skills that covers the task. Apply `human-writing-style` as the prose baseline for English academic writing, then add the section skill, then the applicable LaTeX or artifact skill:

| Task signal | Skill |
|---|---|
| Abstract block or abstract prose | `abstract-ieee` |
| Introduction | `introduction-ieee` |
| Related Work | `related-work-ieee` |
| Methodology or Method | `methodology-ieee` |
| Experiments or Experiment | `experiments-ieee` |
| Conclusion | `conclusion-ieee` |
| Reviewer response or rebuttal | `rebuttal` |
| IEEE journal/Transactions LaTeX | `latex-ieee-paper` |
| IEEE/CV conference LaTeX | `latex-ieee-conference` |
| Citations, labels, or cross-references | `latex-citations-and-cross-refs` |
| Figures, tables, captions, or notes | `latex-figures-and-tables` |
| Equations or notation | `latex-math-notation` |
| Proof interpretation or design-intent paragraphs | `latex-proof-and-design-intent` |

For a LaTeX task, choose `latex-ieee-paper` or `latex-ieee-conference` from the actual document class and venue; do not apply both by default. Combine them with focused skills only when the file contains the corresponding artifact. The section skills describe content; the LaTeX skills describe implementation and formatting.

### Dispatch Algorithm

1. Always apply this file and the human-writing baseline for academic prose.
2. Select at most one primary section skill from the requested section. If the task spans sections, select each named section skill and keep each section's constraints local.
3. For LaTeX, inspect `\documentclass`, venue, and the actual artifact before selecting a journal or conference skill. Never infer the class from a filename alone.
4. Add artifact skills only for artifacts present in the request or file: citations/cross-references, figures/tables, notation, or proof/design intent.
5. Load the selected skill's complete `SKILL.md` only after dispatch; follow its checklist, then run the quality gates below.
6. If two selected skills conflict, prefer the explicit venue template, then the user request, then the more specific artifact rule. Record the decision in the response.
7. A direct user request to use a named skill is an explicit selection, not a request to load unrelated skills.

## Execution Workflow

1. Inspect the relevant manuscript, `.tex`, `.bib`, figures, tables, and venue template before making claims about them.
2. Load the selected skill(s) and preserve the source rule's terminology, thresholds, examples, and checklists unless they conflict with a stated venue requirement.
3. Draft or revise the requested artifact. Keep results separate from interpretation where the section structure requires it.
4. Run the relevant checks: evidence/citation consistency, labels and cross-references, figure/table completeness, notation consistency, word/page limits, and compilation when a LaTeX toolchain is available.
5. Return the requested deliverable first, then concise assumptions, unresolved issues, and verification items. Never present a placeholder or unverified value as final evidence.

## Quality Gates

- Every major claim has a source, an author-provided result, or an explicitly marked reasoning basis.
- All in-text citations resolve to the intended bibliography entries; no bibliography entry is silently orphaned.
- Every numbered float, section, equation, and algorithm has a stable label and is referenced with the selected convention.
- Figure/table captions, notes, units, legends, scale bars, symbols, and data-source statements are complete.
- Numbers, metrics, units, acronyms, tense, capitalization, and notation are consistent.
- The final section does not introduce unsupported new findings, comparisons, terminology, or citations.

## Migration Notes

The mapping from each Cursor `.mdc` source to its Codex skill is recorded in `migration/rule-map.md`. Do not edit the source `.mdc` files when changing Codex behavior; update the corresponding `SKILL.md` and the migration record together. Run `powershell -ExecutionPolicy Bypass -File migration/validate-rules.ps1` after rule changes.
