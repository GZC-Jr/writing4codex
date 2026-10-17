# Academic Writing Project

## Scope

These instructions govern academic drafting, revision, translation, peer-review responses, LaTeX editing, citation work, figure/table preparation, and submission checks in this project.
Codex uses the project skills under `.agents/skills/`.

## Instruction Precedence

- System and developer instructions always take precedence over this file.
- Follow the user's explicit deliverable, language, discipline, venue, and evidence constraints.
- Apply this file to every task in the project.
- Use a skill only when its trigger matches the task.
  A skill adds detail.
  It does not weaken these baseline constraints.
- A named venue or provided template overrides generic IEEE defaults.
  When requirements conflict, report the conflict and follow the highest-priority applicable source.
- Section lengths, citation counts, paragraph patterns, colors, and Remark conventions in the skills are project defaults, subject to the user's instructions and actual venue template.
  Apply them where they fit the evidence and task without padding text, references, or experiments.

## Evidence Integrity

- Never fabricate references, quotations, DOI or page numbers, datasets, participants, measurements, statistical values, experiments, code URLs, or findings.
- Do not claim that a source was searched, opened, verified, or cited unless that action actually occurred.
- Distinguish source-supported facts, author-provided claims, interpretation, hypothesis, and speculation.
- Preserve the original level of certainty, limitations, causal strength, and attribution when editing or translating.
- If required information is missing, use a clearly marked placeholder or report the missing item.
  Do not silently fill it in.
- Do not silently add, delete, merge, or reorder references or results.
- Example numbers, citation keys, method names, and result claims illustrate writing or formatting.
  Verify them against the supplied manuscript and sources before using them as evidence.

## Citation Placement

- **When a specific method is named and cited, place its citation immediately after the method name.**
  Use `Transformer \cite{vaswani2017attention}` or `Transformer~\cite{vaswani2017attention}`, before the subsequent explanation, verb, or clause.
  Keep the method name and its citation on the same physical source line.
- When several distinct methods are named, attach the correct citation to each method separately.
  Do not collect their references into a shared sentence-end citation that obscures the mapping between methods and sources.
- Group keys in one citation only when they support the same named method or the same general claim without distinct named methods.
- Use the actual bibliography keys and preserve attribution.
  Citation placement does not authorize inventing a reference or adding a citation to the paper's own newly proposed method without a source.
- Apply this placement rule where citations are permitted by the target venue.
  Keep a citation-free abstract citation-free when its venue requires that format.

## Human Writing Baseline

This baseline is always active.
The full examples and checklist remain in the `human-writing-style` skill.

- Write precise, varied, unforced prose that reads like a researcher wrote it under deadline.
  Open paragraphs with substantive claims, not empty transitions.
- Vary sentence shapes naturally within a paragraph, using direct claims, qualifying clauses, consequences, causal explanations, or concrete-number claims where appropriate.
  Avoid a fixed sequence that makes every paragraph follow the same template.
- Hedge with concrete limits and conditions rather than vague adverbs.
  Preserve uncertainty.
  Never turn an estimate or hypothesis into a fact.
- Use field-standard vocabulary sparingly.
  Prefer `use`, `build on`, or `suitable` over buzzwords such as `leverage`, `delve into`, `tapestry`, `robust solution`, or `harness the power of`.
- Avoid repeated paragraph openers, emphatic adjectives (`crucial`, `vital`, `paramount`, `revolutionary`), apology phrases, empty reporting wrappers, Markdown punctuation, and emoji in LaTeX body text.
- Use specific numbers and named baselines when available.
  Keep `novel` to at most one occurrence in an abstract and use `leverage` zero times in academic prose unless it is a literal technical term.
- In methodology and related-work limitation paragraphs, use a causal explanation such as `By X, Y` when it accurately describes the mechanism.
  Do not force the pattern when the evidence does not support it.
- **Mandatory avoidance: no semicolons in ordinary prose.**
  Do not use `;` or `；` to connect clauses in Chinese or English academic writing.
  Split the clauses into complete sentences or join them with a suitable conjunction.
  Preserve semicolons only in verbatim quotations or required technical syntax, such as code, mathematical notation, or citation commands.
- **Mandatory avoidance: no verb or negation contractions.**
  Write `it is`, `there is`, `we are`, `it has`, `we have`, `will not`, `cannot`, and `do not` in full.
  Never shorten them to forms such as `it's` / `it’s`, `there's` / `there’s`, `we're`, `we've`, `won't`, `can't`, or `don't` in academic prose.
  Expand `'s` / `’s` according to whether it means `is` or `has`, while preserving possessives such as `the model's output`.
- **Prefer object-centered passive voice for author actions and contributions.**
  Wherever a natural passive construction preserves the meaning, avoid `we propose`, `we proposed`, `we design`, `we designed`, `we introduce`, and similar author-led statements.
  Use forms such as `A method is proposed`, `A module was designed`, or `Experiments were conducted`, preserving the original tense, certainty, and attribution.
  Use named methods, components, or results as subjects when describing their behavior or findings.
  Keep attribution clear and replace empty wrappers such as `It can be seen that` with the substantive statement.

## Mandatory Sentence-per-Line Formatting

**强制规则：写完一句立即换行，每个完整句子必须独占一个物理行，禁止整段写在同一行。**

- Apply this rule to all newly written or revised Chinese and English prose, including LaTeX abstracts, body text, captions, footnotes, Markdown documents, and review responses.
- Insert a literal newline after each complete sentence, keeping its citations, inline math, and closing markup with that sentence.
- Separate paragraphs with a blank line to preserve paragraph structure and rendered typesetting.
- Do not hard-wrap a sentence at a fixed column width or insert LaTeX `\\` or `\newline` merely to satisfy this source-formatting rule.
- Identify complete sentences by meaning, without treating abbreviations, decimal points, URLs, or LaTeX commands as sentence boundaries.
- Skill examples do not override this mandatory formatting requirement.

## Task Intake

Before writing or editing, identify (or state as unknown):

1. The requested operation: draft, revise, translate, compress, review, format, or rebut.
2. The manuscript section or artifact: abstract, introduction, related work, methodology, experiments, results, discussion, conclusion, references, rebuttal, figure, table, equation, or full paper.
3. Discipline, audience, target venue, document class, language, word/page limit, and citation style.
4. Which claims, data, sources, templates, and files are actually available and which require verification.

Do not block on a missing preference when a conservative assumption is reversible.
State the assumption in the response and flag venue-specific items for confirmation.

## Skill Dispatch

Use the smallest set of skills that covers the task.
Apply `human-writing-style` as the prose baseline for English academic writing, then add the section skill, then the applicable LaTeX or artifact skill:

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

For a LaTeX task, choose `latex-ieee-paper` or `latex-ieee-conference` from the actual document class and venue.
Do not apply both by default.
Combine them with focused skills only when the file contains the corresponding artifact.
The section skills describe content.
The LaTeX skills describe implementation and formatting.

### Dispatch Algorithm

1. Always apply this file and the human-writing baseline for academic prose.
2. Select at most one primary section skill from the requested section.
   If the task spans sections, select each named section skill and keep each section's constraints local.
3. For LaTeX, inspect `\documentclass`, venue, and the actual artifact before selecting a journal or conference skill.
   Never infer the class from a filename alone.
4. Add artifact skills only for artifacts present in the request or file: citations/cross-references, figures/tables, notation, or proof/design intent.
5. Load the selected skill's complete `SKILL.md` only after dispatch.
   Follow its checklist, then run the quality gates below.
6. Resolve conflicts under the instruction precedence above, respecting the user's explicit constraints, applicable venue template, project baseline, and then the more specific artifact rule.
   Record material decisions in the response.
7. A direct user request to use a named skill is an explicit selection, not a request to load unrelated skills.

## Execution Workflow

1. Inspect the relevant manuscript, `.tex`, `.bib`, figures, tables, and venue template before making claims about them.
2. Load the selected skill(s) and preserve the source rule's terminology, thresholds, examples, and checklists unless they conflict with a stated venue requirement.
3. Draft or revise the requested artifact.
   Keep results separate from interpretation where the section structure requires it.
4. Run the relevant checks: evidence/citation consistency, labels and cross-references, figure/table completeness, notation consistency, word/page limits, and compilation when a LaTeX toolchain is available.
5. Return the requested deliverable first, then concise assumptions, unresolved issues, and verification items.
   Never present a placeholder or unverified value as final evidence.

## Quality Gates

- Every major claim has a source, an author-provided result, or an explicitly marked reasoning basis.
- All in-text citations resolve to the intended bibliography entries.
  No bibliography entry is silently orphaned.
- Each cited specific method has its citation immediately after its name, with distinct methods mapped to their own references.
- Every numbered float, section, equation, and algorithm has a stable label and is referenced with the selected convention.
- Figure/table captions, notes, units, legends, scale bars, symbols, and data-source statements are complete.
- Every newly written or revised prose sentence occupies its own physical source line, with blank lines retained between paragraphs.
- Ordinary academic prose contains no semicolons or verb/negation contractions, with possessive apostrophes preserved and any required semicolons checked against the baseline exceptions.
- Author-action and contribution statements use natural object-centered passive constructions wherever possible, with tense, certainty, and attribution preserved.
- Numbers, metrics, units, acronyms, tense, capitalization, and notation are consistent.
- The final section does not introduce unsupported new findings, comparisons, terminology, or citations.
