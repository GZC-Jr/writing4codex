---
name: experiments-ieee
description: "Experiments writing for CV/Robotics/IP top journals and conferences — A./B./C./D./E./F. subsections with dataset / settings / SOTA / qualitative / ablation / class-complexity / real-world"
metadata:
  migrated-from: "experiments-ieee.mdc"
  source-always-apply: "false"
  source-globs: ""
---

## Codex Invocation

Use this skill when the task matches the source rule's scope or when the user names this section/artifact.
Apply it after the project-level AGENTS.md intake and alongside only the focused skills required by the task.
The source rule had no file glob.
Codex dispatches it by task and artifact.
Do not invent missing evidence to satisfy a pattern.
If a source rule requires a dataset, numeric result, code URL, limitation, or venue convention that is unavailable, mark it as missing and report the verification item.

# Experiments Writing

> **Note**: Use this skill when drafting/revising `\section{Experiments}` or `\section{Experiment}` of a top-tier journal or conference paper.
> The A./B./C./D./E./F. alphabetic subsection pattern (Implementation Details → Quantitative → Qualitative → Ablation → Class-Complexity → Real-World Tests) applies across IEEE T-PAMI, TIP, CVPR, ICCV, ECCV, ICRA, and related venues.

## Core Principle

The Experiments section has a **canonical alphabetic subsection sequence**:

```
A. Implementation Details   (training schedule, hardware, metrics)
B. Quantitative Result      (numeric tables, gain vs SOTA)
C. Qualitative Result       (visual comparison figures)
D. Ablation Study           (component-wise removal with numeric drop)
E. Quantitative Assessment of Class Complexity  (per-class breakdown, optional)
F. Real-World Tests         (deployment scenario, runtime, FPS, optional)
```

Each subsection answers **one evaluation question**.
Subsections B and D are non-optional — datasets with structural diversity *benefit from* class-complexity reporting (E), and edge/robotics papers benefit from real-world tests (F).

## Constants

- **SUBSECTION_PATTERN**: `\subsection{<Title>}` with numbering supplied by the actual class.
- **SOTA_TABLE_PREFIX**: `tab:sota_` - Prefix for comparison tables.
  Suffix with benchmark name.
- **ABLATION_TABLE**: `\label{tab:ablation}` for component-wise ablations, referenced wherever its results are discussed.
- **CLASS_COMPLEXITY_TABLE**: `\label{tab:class_complexity}` - Per-class average metrics at each scale/condition.

## Rules

### ✅ DO

- Open with **Implementation Details**: training schedule, optimizer, hardware, batch size, total epochs, evaluation metrics, parameter count
- Use **Quantitative Result** with several `\cref{tab:...}` references, each tied to a specific row of discussion
- Use **Qualitative Result** with `\subfloat{}` panels: organize by scene type or difficulty level
- In **Ablation Study** text, name **which** row by its label.
  e.g. *"Removing the coordinate-offset module drops PSNR by 0.27 dB"* — never *"the ablation shows..."*
- Use **Class Complexity** when datasets span multiple classes with structural diversity
- Close with **Real-World Tests** if your method ships.
  Report runtime + FPS + device specs (e.g. *"×2 ROI patch processing exceeding 25 FPS on RTX 3060"*)
- Mark the best result in each comparable metric column, respecting whether higher or lower values are better.

### ❌ AVOID

- Do not bury Implementation Details in supplementary.
  Reviewers must see what you trained on
- Do not merge Quantitative Result and Ablation into one table.
  Audiences are different
- Do not say *"experiments show our method is best"* — show the **number** (*"+0.51 dB over prior SOTA at ×4"*)
- Do not have a Qualitative subsection without a `\subfloat{}` figure.
  Visual comparison belongs to multi-panel sub-floats
- Do not add per-class or class-complexity analysis merely to meet a class-count threshold.
  Include it when it answers a relevant evaluation question and the data support it.
- Do not imply that deployment was tested without corresponding evidence.
  Report available real-world evidence and identify missing evaluations without inventing them.

## Patterns

### A. Implementation Details

```latex
% ✅ Good: optimizer / LR / warm-up / batch / epoch / hardware / metrics / complexity
\subsection{Implementation Details}
\label{sec:impl}
The dataset is systematically divided into training and testing sets following the standard protocol \cite{ref_data}.
The training set maintains a balanced ratio across scene types to ensure diversity.
\ldots Adam \cite{ref49} is used as the optimizer with the initial learning rate $4 \times 10^{-5}$ and the maximum $4 \times 10^{-4}$.
A warm-up strategy is adopted in the first 20 epochs to stabilize training.
The batch size is $16$ and the number of training epochs is $100$.
All models are trained on an NVIDIA A100 GPU (40-GB memory).
Peak signal-to-noise ratio (PSNR) and structure similarity index measure (SSIM) \cite{ref50} are used to measure performance.
The number of parameters (Params) and multiply--accumulate operations (MACs) are used to measure model complexity.
```

```latex
% ❌ Bad: vague scheduler; missing warm-up / hardware / complexity
\subsection{Implementation Details}
We use Adam to optimize our network.
The learning rate is set to $10^{-4}$.
We train for 200 epochs with batch size 32 on a single GPU.
We report PSNR and SSIM.
```

### B. Quantitative Result (with specific numeric claims)

```latex
% ✅ Good: ties numeric claim to specific baseline + scale
\subsection{Quantitative Result}
\label{sec:quant}
Tables~\ref{tab:sota_test1} and \ref{tab:sota_test2} present the quantitative comparison of different methods on two test sets.
In Table~\ref{tab:sota_test1}, several scaling factors are selected randomly to conduct quantitative comparisons.
OurMethod achieves the highest PSNR values at all testing scales, outperforming both traditional interpolation (Bicubic) and state-of-the-art methods (MethodA, MethodB, MethodC).
Notably, at a scaling factor of $\times 1.2$, the method attains the PSNR/SSIM of $40.50$\,dB$/0.9890$, surpassing Bicubic by $5.07$\,dB$/0.0141$ and exceeding the second-best method by $0.17$\,dB$/0.0008$.
\ldots The proposed method maintains significant advantages even at extreme scales \ldots
```

```latex
% ❌ Bad: vague; runs together
Our method performs better than other methods on most datasets.
The improvements are significant and demonstrate the effectiveness of our approach.
```

### C. Qualitative Result with `subfloat`

```latex
% ✅ Good: two-panel subfloat tied to top-row text + bottom-row text
\subsection{Qualitative Result}
\label{sec:qual}
The results for several images from the test set are presented in Figs.~~\ref{fig:qual_set1} and \ref{fig:qual_set2}.
In these figures, the top two images are from scenes with rich textures, and their visualizations reflect the performance in structurally complex environments.
The bottom two images are from scenes with sparser content, focusing on performance in handling small objects.
\begin{figure}[!t]
  \centering
  \subfloat[]{\includegraphics[width=0.48\linewidth]{qual_a.pdf}
    \label{fig:qual_a}}
  \hfil
  \subfloat[]{\includegraphics[width=0.48\linewidth]{qual_b.pdf}
    \label{fig:qual_b}}
  \caption{Visual comparison results. (a) Result from Method A. (b) Result from Method B. (c) Result from Method C. (d) Ground truth.
  The proposed method generates higher quality outputs with finer details.}
  \label{fig:qual_set1}
\end{figure}
```

### D. Ablation Result Paragraph (numeric drop tied to component)

```latex
% ✅ Good: every removal cited by name and number
\subsection{Ablation Study}
\label{sec:ablation}
Tables~\ref{tab:ablation_module_a} and \ref{tab:ablation_module_b} illustrate the impact of Module A and Module B on model performance.
PSNR is positively correlated with the two hyperparameters.
Although performance continues to improve, the total parameter number grows quadratically.
To strike a balance between performance and model size, the numbers are set to the reported values.

To validate the contributions of key components in the proposed method, ablation experiments are conducted by systematically removing or modifying individual modules.
Table~\ref{tab:ablation_module} demonstrates the progressive impact of each component.
The whole model achieves the highest PSNR, confirming the synergistic effectiveness of all components.
PSNR gradually decreases as modules are removed one by one.
```

```latex
% ❌ Bad: w/o commentary, unjustified "improve"
\subsection{Ablation}
As shown in the table, our ablation study verifies the importance of each component.
The full model achieves the best results, while the model without some modules performs worse.
```

### E. Quantitative Assessment of Class Complexity

```latex
% ✅ Good: per-class breakdown table + per-class interpretation
\subsection{Quantitative Assessment of Class Complexity}
\label{sec:class}
The quantitative results in Table~\ref{tab:class_complexity} reveal that the performance exhibits notable variations across different scene classes and conditions.
For the primary test set, classes such as A, B, and C achieve relatively higher PSNR values (approximately 33 dB under condition X) compared to D and E, which remain slightly lower, indicating that fine-grained texture structures are better preserved in some regions than in large uniform areas.
As the condition intensifies, a consistent degradation in PSNR is observed across all classes.
```

### F. Real-World Tests

```latex
% ✅ Good: deployment scenario + sensor spec + FPS at multiple scales
\subsection{Real-World Tests}
\label{sec:real}
For real-world testing, a sensor mounted on the platform is employed, as shown in \cref{fig:real_world}.
This experimental setup facilitates flexible integration and enables real-time processing.
\ldots The platform can support $\times 2$ processing with a frame rate (FPS) exceeding $25$ while maintaining an FPS above $14$ under $\times 3$ processing.
These results confirm the practicality and operational feasibility of the method.
```

## Examples

### ✅ Good Subsection Titles

> "A.
> Implementation Details" "B.
> Quantitative Result" "C.
> Qualitative Result" "D.
> Ablation Study" "E.
> Quantitative Assessment of Class Complexity" "F.
> Real-World Tests"

### ✅ Good Per-Component Ablation Interpretation

> "Removing the coordinate-offset refinement module drops PSNR by 0.27 dB, confirming that spatial awareness is the primary source of boundary fidelity."

### ❌ Bad Ablation Paragraph

> "As shown in the table, our ablation study verifies the importance of each component.
> The full model achieves the best results."

## Benefits

- **Reviewer auditability**: Numeric claims tied to a labeled table make rebuttal trivial
- **Reproducibility**: A.
  Implementation Details is concrete enough that another lab can re-run
- **Class-complexity reporting** (E) defends against *"how do you know it is not class bias?"* critiques
- **Real-world closure** (F) defends against *"but does it run on the actual platform?"* critiques

## Related Skills

- [rule-academic-writing-latex-figures-and-tables](../latex-figures-and-tables/SKILL.md) - Table caption/label order and `booktabs` style
- [rule-academic-writing-methodology-ieee](../methodology-ieee/SKILL.md) - Ablation rows correspond to modules defined earlier
- [rule-academic-writing-latex-ieee-paper](../latex-ieee-paper/SKILL.md) - Venue defaults surface alphabetic subsection numbering

## Remember

- A./B./C./D./E./F. alphabetic subsections, in this order
- Mark the best value per comparable metric column in comparison tables.
- Every ablation row has a numeric drop, paired with a paragraph explaining the cause
- Include Real-World Tests when needed to support deployment claims, reporting missing evidence as an unresolved item.
