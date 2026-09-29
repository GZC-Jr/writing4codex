---
name: latex-figures-and-tables
description: "LaTeX 实现模式 + caption 表注图注写作风格，全链路覆盖 CV/Robotics/IP 顶会 camera-ready 规范"
metadata:
  migrated-from: "latex-figures-and-tables.mdc"
  source-always-apply: "false"
  source-globs: "**/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}"
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact. Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source Cursor glob was **/{main,paper,manuscript,ms,article,tex,submission}.{tex,sty}; Codex dispatches by task and artifact instead of evaluating Cursor glob syntax.
Do not invent missing evidence to satisfy a pattern. If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Figures and Tables (LaTeX + Writing Style)

> **Note**: Applies to `main.tex` whenever `IEEEtran` + `subfig` + `booktabs` are loaded.
> Covers both single `\begin{figure}` and multi-subfigure `\subfloat` patterns.
>
> **Source baseline**: CV/Robotics/IP universal top-tier conventions —
> IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, IROS camera-ready standards.

## Constants

- **FIG_DIR**: `figures/` — All figure assets (PDF preferred for vectors, PNG ≥ 300 DPI for raster).
- **TAB_PACKAGE**: `booktabs` — Three-line table style; no vertical rules.
- **BEST**: `{\color{red}\textbf{value}}` — best score in a column
- **SECOND**: `{\color{blue}value}` — second-best score in a column
- **OOS-SYMBOL**: `*` — marks cells where the scale/setting exceeds training distribution
- **OOS-TEXT**: `INDICATES THAT THE SCALE IS OUT OF THE TRAINING DISTRIBUTION.`
- **OUT-OF-DIST**: `{\textdagger}` (`†`) — marks methods trained under a different setting
- **STAT-SIG**: `{\textdaggerdbl}` (`‡`) — statistical significance footnote

---

## 1. Caption Structure

### 1.1 Table Captions

Table captions go **above** the table.

```latex
\begin{table*}
\caption{\MakeUppercase{Descriptive title of the table.}}
\label{tab:name}
\end{table*}
```

- **ALL CAPS** title opener — every table caption begins with ALL CAPS
- Use `table*` for two-column spanning; `table` for single-column
- `\caption` before `\label` — IEEE class expects this order for `cleveref` to resolve correctly
- Do NOT end caption with a period unless the title contains abbreviations
- Keep title concise; metric names belong in column headers, not the caption

**Examples:**

| Type | Caption |
|------|---------|
| Quantitative comparison | `QUANTITATIVE COMPARISON ON [DATASET].` |
| Ablation | `ABLATION STUDY ON [MODULE/DESIGN].` |
| Cross-dataset | `CROSS-DATASET GENERALIZATION ANALYSIS.` |
| Complexity | `MODEL COMPLEXITY AND INFERENCE COMPARISON.` |

### 1.2 Figure Captions

Figure captions go **below** the figure.

```latex
\begin{figure*}
\caption{Descriptive caption in sentence case.}
\label{fig:name}
\end{figure*}
```

- **Sentence case** (not ALL CAPS) for figure captions
- For sub-figures, label as `(a)`, `(b)`, `(c)` — lowercase letter in parentheses
- When referencing sub-figures inline: `Fig. 1(a)`, `Figs. 1(a)–(c)`
- Use `figure*` for two-column spanning; `figure` for single-column

**Sub-figure layout conventions:**
- Arrange sub-figures horizontally when ≤ 3 items; stack vertically when > 3
- Maintain consistent width across sub-figures within the same row
- Sub-figure labels should be bold or underlined for clarity
- Include scale indicators (reference bar or magnification label) in all visual comparison figures

**Examples:**

```
Fig. 1. Qualitative results at ×4 scale. (a) LR input. (b) Bicubic.
(c) SRCNN. (d) Ours.
```

```
Fig. 2. Attention map visualization. (a) Input image. (b)–(d) Attention
weights from stages 1–3 of the proposed model.
```

---

## 2. Table Note Writing

### 2.1 Note Header

Begin every table note with **ALL CAPS**, preceded by `Note—`:

```latex
\begin{tablenotes}
\item[Note—] {\textbf{QUANTITATIVE COMPARISON ON [DATASET] AT SCALES ... .}}
\item[$\dagger$] {Training set includes this scale / setting.}
\item[$*$]   {INDICATES THAT THE SCALE IS OUT OF THE TRAINING DISTRIBUTION.}
\end{tablenotes}
```

- `Note—` (em-dash) introduces the primary note block in **bold ALL CAPS**
- Do NOT use `\footnote` inside `table`/`tabular` environments — always use `tablenotes`
- Threeparttable + booktabs is the standard package stack

### 2.2 Symbol Footnotes

Use `*.` to mark cells where the scale/setting exceeds training distribution:

```latex
\item[$*$] {INDICATES THAT THE SCALE IS OUT OF THE TRAINING DISTRIBUTION.}
```

Use `†` for methods trained at a different setting:

```latex
\item[$\dagger$] {Method trained under a different setting.}
```

Use `‡` for statistical significance:

```latex
\item[$\ddagger$] {Statistically significant improvement over the baseline ($p < 0.05$).}
```

**Symbol priority**: `*` → `†` → `‡` → `§` (extend if needed)

### 2.3 Note Content Rules

- **Quant comparison notes**: State metric abbreviation, dataset name, and scale/range in ALL CAPS; explain symbols in mixed case
- **Ablation notes**: Define each module abbreviation once in the note; reference figure panels if needed
- **Complexity notes**: Define `#params`, `FLOPs`, `FPS` on first use; specify hardware context
- **Cross-dataset notes**: Clarify "Seen" vs. "Unseen" column groupings explicitly
- **General**: All symbols used in the table must be defined in the note; no orphan symbols

---

## 3. Color and Bold Conventions

Apply color-and-bold marking **per-column**, not per-row.

| Mark | Rendering | When to use |
|------|-----------|-------------|
| **BEST** | `{\color{red}\textbf{value}}` | Highest value (higher-is-better) or lowest (lower-is-better) in a metric column |
| **SECOND** | `{\color{blue}value}` | Second-highest / second-lowest in the same column |

- For metrics where **higher is better** (e.g., accuracy, PSNR, SSIM): mark the **maximum**
- For metrics where **lower is better** (e.g., FLOPs, latency, #params): mark the **minimum**
- Apply **per-column**, not per-row — the "best" in a runtime column differs from an accuracy column
- Fallback for B&W print or arXiv: use `textbf` for BEST, `textit` for SECOND
- Do **not** use row shading — reserved for table headers only

---

## 4. LaTeX Patterns

### 4.1 Subfigure Composition

```latex
% ✅ Good: two-panel subfigure with shared caption and individual label
\begin{figure}[!t]
  \centering
  \subfloat[]{\includegraphics[width=0.48\columnwidth]{framework_a.pdf}\label{fig:framework_a}}
  \hfil
  \subfloat[]{\includegraphics[width=0.48\columnwidth]{framework_b.pdf}\label{fig:framework_b}}
  \caption{(a) Overall pipeline. (b) Detailed SE-UpdateNet architecture.}
  \label{fig:framework}
\end{figure}
```

```latex
% ❌ Bad: separate figures with mismatched captions and no shared anchor
\begin{figure}[!t]
  \includegraphics[width=0.48\textwidth]{framework_a.pdf}
  \caption{Pipeline.}
\end{figure}
\begin{figure}[!t]
  \includegraphics[width=0.48\textwidth]{framework_b.pdf}
  \caption{Architecture.}
\end{figure}
% Reviewers must \cref two figures to understand one concept
```

### 4.2 Booktabs Table

```latex
% ✅ Good: booktabs three-line, color-best result, caption before label
\begin{table}[!t]
  \centering
  \caption{QUANTITATIVE COMPARISON ON [DATASET].}
  \label{tab:comparison}
  \begin{tabular}{lcc}
    \toprule
    Method & PSNR $\uparrow$ & SSIM $\uparrow$ \\
    \midrule
    Baseline-A & 28.50 & 0.82 \\
    Baseline-B & 29.12 & 0.85 \\
    \textbf{\color{red}Ours} & \textbf{\color{red}31.44} & \textbf{\color{red}0.91} \\
    \bottomrule
  \end{tabular}
\end{table}
```

```latex
% ❌ Bad: vertical rules, unstyled caption, no color-best
\begin{table}
  \centering
  \begin{tabular}{|l|c|c|} \hline
    Method & PSNR & SSIM \\ \hline
    Baseline-A & 28.50 & 0.82 \\ \hline
  \end{tabular}
\end{table}
% IEEE LaTeX never uses vertical rules; color-best is missing
```

### 4.3 Table with tablenotes

```latex
\begin{table}[!t]
  \centering
  \caption{QUANTITATIVE COMPARISON ON [DATASET] AT SCALES $\times$2, $\times$4, $\times$6.}
  \label{tab:main}
  \begin{threeparttable}
    \begin{tabular}{lcccccc}
      \toprule
      Method & \multicolumn{2}{c}{\centering $\times$2} & \multicolumn{2}{c}{\centering $\times$4}
              & \multicolumn{2}{c}{\centering $\times$6} \\
      \cmidrule(lr){2-3}\cmidrule(lr){4-5}\cmidrule(lr){6-7}
              & PSNR & SSIM & PSNR & SSIM & PSNR & SSIM \\
      \midrule
      Bicubic   & 31.20 & 0.89 & 25.10 & 0.74 & 21.30 & 0.58 \\
      Ours      & \textbf{\color{red}35.44} & \textbf{\color{red}0.96}
                & \textbf{\color{red}29.52} & \textbf{\color{red}0.91}
                & \color{blue}23.14\tnote{*} & \color{blue}0.65\tnote{*} \\
      \bottomrule
    \end{tabular}
    \begin{tablenotes}
      \item[Note—] {\textbf{QUANTITATIVE COMPARISON ON [DATASET] AT SCALES $\times$2, $\times$4, $\times$6.
                     BEST AND SECOND-BEST RESULTS ARE MARKED IN RED AND BLUE, RESPECTIVELY.}}
      \item[$*$] {INDICATES THAT THE SCALE IS OUT OF THE TRAINING DISTRIBUTION.}
    \end{tablenotes}
  \end{threeparttable}
\end{table}
```

---

## 5. In-Text Cross-References

### 5.1 Referring to Tables

| Context | Correct | Incorrect |
|---------|---------|-----------|
| Singular, start of sentence | `Table I` | `table I` |
| Singular, mid-sentence | `Table I` | `table I` |
| Plural | `Tables I and II` | `Table I and II` |
| Reference specific column | `"the ×4 column of Table I"` | `"the fourth column of Table I"` |

- **Always capitalize** "Table" when referring to a specific numbered table
- Use `Table~I` (tilde) to prevent line break between "Table" and numeral
- Avoid vague references: write `"Table I reports"` not `"The following table shows"`
- Pair table/figure references: *"As shown in Table II and Fig. 3, ..."*

### 5.2 Referring to Figures

| Context | Correct | Incorrect |
|---------|---------|-----------|
| Singular, start of sentence | `Figure 1` | `figure 1`, `fig. 1` |
| Singular, mid-sentence | `Fig. 1` | `Figure 1` (overly formal) |
| Plural | `Figs. 1 and 2` | `Figure 1 and 2` |
| Sub-figure reference | `Fig. 1(a)` | `Figure 1a`, `fig. 1a` |
| Sub-figure range | `Figs. 1(a)–(c)` | `Fig. 1(a)(b)(c)` |

- Use `Figure` at the beginning of a sentence; `Fig.` elsewhere
- Always use dot notation for sub-figures: `Fig. 1(a)`, not `Fig 1a`

### 5.3 Referring to Sections and Equations

- Section references: `Section II-B`, `Sections I and III`
- Equation references: `Eq. (1)`, `Eqs. (3)–(5)` — parentheses around the number
- Algorithm references: `Algorithm 1`

---

## 6. Camera-Ready Layout

### 6.1 Font and Spacing

- Table body: `\footnotesize` (9 pt) for camera-ready; confirm target venue requirements
- Figure labels, legends, scale bars: minimum 8 pt; 9–10 pt preferred for axis tick labels
- Line spacing within tables: 1.0 or `0.95`; do not stretch to fill space
- Vertical spacing around tables: `\bigskip` or equivalent

### 6.2 Table Column Structure

- Use `booktabs`: no vertical rules; `\toprule`, `\midrule`, `\bottomrule`
- Numeric columns: right-align numbers; text columns: left-align
- Column headers: **bold**, centered, sentence case or ALL CAPS per venue
- Multi-column headers: `\multicolumn` with centered text and horizontal rule below
- Units in column headers: `(dB)`, `(\%)` — not repeated in every cell
- Precision consistency: `38.52` not `38.5` mixed with `38.52` in the same column

### 6.3 Figure Layout

- Preferred formats: PDF (vector) > PNG (≥ 300 DPI) > TIFF
- Preferred widths: single-column (~3.5 in) or double-column (~7.0 in); respect margins
- Use `subcaption` or `subfig` package; label as `(a)`, `(b)`, `(c)`
- Multi-panel comparisons: sort left-to-right by ascending quality or alphabetically
- Always include: axis labels, tick marks, unit indicators, colorbar for heatmaps
- Scale indicators: reference bar or magnification label (`×4`) in all reconstruction figures

### 6.4 Positioning

- Use `[!htbp]` placement hint: prefer here → top → bottom → page float
- Place tables and figures as close to their first reference as possible
- Do not force tables to the bottom of a page where they spill across columns

---

## 7. Checklist

Before submission, verify:

- [ ] All table captions are above the table; all figure captions are below
- [ ] Table captions begin with ALL CAPS; figure captions use sentence case
- [ ] Each `*.` symbol in the table has a corresponding `item[$*]` in `tablenotes`
- [ ] `*. INDICATES THAT THE SCALE IS OUT OF THE TRAINING DISTRIBUTION.` is present if OOS scales exist
- [ ] BEST cells use `{\color{red}\textbf{...}}`; SECOND cells use `{\color{blue}...}`
- [ ] Color marking is per-column, not per-row
- [ ] Sub-figures are labeled `(a)`, `(b)`, `(c)` and referenced as `Fig. 1(a)`
- [ ] All scale bars, colorbars, and axis labels are present in every figure
- [ ] In-text references use `Table I`, `Fig. 1`, `Section II-B`, `Eq. (1)` conventions
- [ ] `tablenotes` used instead of `\footnote` inside table environments
- [ ] No vertical rules in tables; `booktabs` style throughout
- [ ] Precision is consistent within each numeric column
- [ ] `\caption` precedes `\label` in every float environment

---

## Related Skills

- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) — `\caption{}` / `\label{}` order in IEEE context
- [rule-academic-writing-latex-citations-and-cross-refs](../latex-citations-and-cross-refs/SKILL.md) — Enables `\cref{tab:...}` use