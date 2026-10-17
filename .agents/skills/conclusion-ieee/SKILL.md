---
name: conclusion-ieee
description: "Conclusion writing for CV/Robotics/IP top journals and conferences — recap → 'Despite promising results, several limitations remain...' → future work"
metadata:
  migrated-from: "conclusion-ieee.mdc"
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

# Conclusion Writing

> **Note**: Use this skill when drafting/revising `\section{Conclusion}` of a top-tier journal or conference paper.
> The `Despite ... limitations remain ...` pivot sentence is the canonical closing pattern across IEEE T-PAMI, TIP, CVPR, ICCV, ICRA, and related venues.

## Core Principle

The Conclusion covers **three content roles**, using the paragraph structure required by the venue:

1. **Recap** — restate the contributions using a different angle from the abstract and introduction.
   Do not copy-paste sentences
2. **Limitations** — identify concrete, scoped limitations with an explicit transition.
   Use the suggested pivot phrase when it fits the findings.
3. **Future work** — same number of bullet-sentences as limitations.
   Pair each limitation with a future direction

Total length: **200-260 words** for journal papers, **80-120** for conference.
No new equations, no new terminology, no new comparisons.

## Constants

- **PIVOT_PHRASE**: `Despite these promising results, several limitations remain.` - Canonical opener of the limitations beat.
- **WORD_BUDGET_JOURNAL**: 260 - Upper bound for a journal Conclusion.
- **WORD_BUDGET_CONFERENCE**: 120 - Upper bound for a conference Conclusion.

## Rules

### ✅ DO

- **Recap** contributions with passive forms such as *"was proposed"*, *"was designed"*, or *"was introduced"*, choosing tense consistently with the manuscript.
- **Limitations** with explicit cost/limitation: *"inference cost remains a bottleneck on edge devices"*, *"significant drop in FPS when facing extreme conditions"*
- **Future work** with parallel scoping: pair each limitation with a `will focus on ...` sentence
- Introduce limitations explicitly, using *"Despite these promising results, several limitations remain."* when it fits or an equally specific transition.

### ❌ AVOID

- Do not repeat the abstract sentence-for-sentence.
  Change emphasis
- Do not introduce new experiments or new baselines (Conclusion is closed-world)
- Avoid author-led recap statements such as *"we have proposed a novel method..."*, preferring a passive restatement that adds a different angle from the Introduction.
- Do not end with *"we hope this work will inspire more research in the field"*.
  Reviewers roll their eyes
- Do not let one content role consume the conclusion's word budget.
  Keep the recap, limitations, and future directions balanced, adjusting sentence counts to the findings.

## Patterns

### Three-Beat Conclusion

```latex
% ✅ Good: recap → "Despite promising results..." → paired future work, ~210 words
\section{Conclusion}
\label{sec:conclusion}

In this work, a method was proposed for [task].
Task-relevant information was integrated into feature extraction, and an upsampler was designed for [supported function].
Evaluation on [benchmark] demonstrated [verified finding] under [conditions].

Despite these promising results, several limitations remain.
Current methods experience a significant drop in FPS when facing extreme upscaling factors, which hinders real-time deployment.
Moreover, the model's memory footprint is currently optimized for offline processing on a desktop GPU rather than on-board inference on resource-constrained hardware.
In addition, the proposed method relies on a fixed taxonomy, and adaptation to new scenarios with reduced data volumes has not yet been investigated.

Future research will therefore focus on developing strategies to maintain stable inference speed under extreme conditions.
Moreover, lightweight and memory-efficient architectures will be investigated to achieve real-time inference on edge devices, thereby substantially reducing the memory requirements.
In addition, adaptation to new scenarios with reduced data volumes will be explored to further improve the practicality and scalability of the method.
```

```latex
% ❌ Bad: 4 paragraphs, copies Introduction, vague wish close
\section{Conclusion}
% Paragraph 1: re-states the entire Introduction.
% Paragraph 2: re-lists contributions as bullets again.
% Paragraph 3: thanks reviewers.
% Paragraph 4: hopes the field progresses.
```

## Pivot Phrase: Why "Despite ... limitations remain"

| Variant | Acceptable? |
|---------|-------------|
| *"Despite these promising results, several limitations remain."* | ✅ Canonical |
| *"While the proposed method achieves strong empirical gains, several constraints remain."* | ✅ Acceptable paraphrase |
| *"Although ... there are still some shortcomings."* | ❌ Too colloquial |
| *"There is no doubt that our method is the best, however ..."* | ❌ Self-promotion + AI-flavored |
| Limitations never named | ❌ Reviewers will flag |

## Examples

### ✅ Good Limitations Beat

> "Despite these promising results, several limitations remain.
> Current methods experience a significant drop in FPS when facing extreme conditions, which hinders real-time deployment.
> Moreover, the model's memory footprint is currently optimized for offline processing on a desktop GPU rather than on-board inference on resource-constrained hardware."

### ✅ Good Future-Work Beat (paired parallelism)

> "Future research will therefore focus on developing strategies to maintain stable inference speed under extreme conditions.
> Moreover, lightweight and memory-efficient architectures will be investigated to achieve real-time inference on edge devices, thereby substantially reducing the memory requirements."

### ❌ Bad Limitations Beat (vague, no numbers)

> "Although our method is very effective, there are still some challenges.
> In the future, we will try to address them and improve the performance further.
> Hopefully our method can be applied to more scenarios."

## Beat Counters

| Beat | Marker phrase (any of) | Journal word count |
|------|------------------------|--------------------|
| Recap | "was proposed", "was designed", "extensive experiments demonstrate" | 60-90 words |
| Limitations | "Despite ... limitations remain" | 60-90 words |
| Future work | "Future ... will focus on", "will be investigated", "will be explored" | 60-90 words |

## Benefits

- **Reviewer closure**: A 3-beat conclusion reads complete, not evasive
- **Future-work anchor**: Each limitation pairs with a follow-up direction
- **Anti-repetition**: Restating from a different angle guards against the "Conclusion = Abstract" complaint
- **Pivot phrase signal**: Reviewers recognize *"Despite these promising results, several limitations remain"* as a deliberate, reader-respecting close

## Related Skills

- [rule-academic-writing-abstract-ieee](../abstract-ieee/SKILL.md) - Conclusion rephrases, never duplicates, the abstract
- [rule-academic-writing-human-writing-style](../human-writing-style/SKILL.md) - Avoid "novel" and "very effective" in the conclusion

## Remember

- Three beats: recap, limitation, future
- Introduce the limitations explicitly with a transition that fits the findings.
- Each limitation must pair with a future-direction sentence in the next beat
- ~200-260 words for journals.
  Shorter for conferences
- Never copy sentences from the abstract or introduction
