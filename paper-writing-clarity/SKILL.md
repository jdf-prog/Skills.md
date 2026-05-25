---
name: paper-writing-clarity
description: Use when writing, restructuring, or polishing academic papers, especially LaTeX manuscripts for benchmarks, agents, LLM evaluation, systems, NLP, or ML papers. Guides Codex to clarify the central research question, narrative spine, section logic, terminology, figure/table support, experiment organization, appendix triage, TODO handling, and compile checks before or during paper edits.
---

# Paper Writing Clarity

## Core Stance

Treat paper writing as argument design, not text polishing. First identify the paper's central research question, the contribution that answers it, and the evidence that supports it. Preserve the paper's real scope; do not invent claims, numbers, experiments, citations, or results.

For conceptual or structural rewrites, discuss the plan before editing unless the user explicitly asks to implement. Once implementation is requested, edit decisively, keep changes scoped, and compile or check the manuscript.

## Rewrite Workflow

1. Read the surrounding section, labels, figures, tables, and included files before editing.
2. Identify the section's job in the paper: motivation, benchmark design, method, evaluation, analysis, limitations, or appendix support.
3. State the proposed section logic in plain language when the change is substantial.
4. Edit around a clear main line rather than preserving accidental structure.
5. Move useful but non-core details to appendix instead of deleting them.
6. Compile or run lightweight LaTeX/reference checks after edits.

## Argument Structure

Make every section, subsection, and paragraph purpose-driven. The first sentence should make clear what the unit is trying to establish. Each paragraph should usually do one job: motivation, mechanism, evidence, or implication.

Prefer the flow `motivation -> mechanism -> why it matters`. If a paragraph starts carrying a new claim, split it or subordinate it clearly.

For benchmark or evaluation papers, make the core research question explicit: what capability is being tested, why existing benchmarks miss it, what the new benchmark or protocol measures, and what the results reveal.

Do not overuse opening anecdotes. Examples are useful only when they highlight the paper's own task properties. Prior-work gaps should be concrete, should name relevant papers or benchmarks when possible, and should connect naturally to a comparison table when one exists.

## Style Preferences

Write with clear hierarchy and visible purpose. Avoid formulaic phrasing such as "This work asks" if it makes the intro feel templated. Avoid long procedural lists in the main text unless the procedure itself is the contribution.

Highlight only key terms, not whole sentences. Use `\textbf{}` or `\textit{}` sparingly for terms that organize the argument.

Avoid clunky parenthetical references such as `(Figure 1, left)`. Prefer prose such as `as shown in \autoref{...}`. Use parentheses mainly for abbreviations or short clarifications.

Use consistent terminology throughout the manuscript. Once a canonical term is chosen, search for and replace unstable variants.

## Section Patterns

For an introduction, a strong default structure is:

1. Concrete prior-work landscape and gap.
2. The missing capability, setting, or evaluation target.
3. The proposed benchmark, method, or system, with numbered feature points if helpful.
4. The safety, reliability, or evaluation mechanism if central to the contribution.
5. The experimental protocol.
6. Main empirical findings.
7. Higher-level insights from analysis.

For benchmark or dataset sections, organize around reader questions:

1. What is being evaluated?
2. How are tasks collected or constructed?
3. How is execution made valid and safe?
4. How are outputs or traces judged?

For experiment sections, use a clear hierarchy:

1. `Experimental Setup`: models, harness, metrics, data splits, and implementation details that affect interpretation.
2. `Main Results`: headline metric first, then model ranking, domain variation, and efficiency or cost if available.
3. `Analysis` or `Trace-Level Diagnosis`: explain why results look the way they do.

Each analysis paragraph should correspond to a figure, table, or clearly marked missing-analysis TODO. Failure analysis can live inside trace-level diagnosis when it explains mechanisms rather than merely listing errors.

## Terminology Discipline

Create a short canonical-term list for the paper. Coordinate names across intro, method, experiments, captions, appendix, and tables.

Prefer metric names that match the actual computation. For example, use `success rate` for binary task pass/fail averages, not `accuracy`, unless the paper truly defines accuracy.

Avoid overclaiming environment properties. If the method only controls a scoped risk, name the scope precisely instead of using broad terms such as `safe sandbox`.

When renaming a concept, search the full manuscript for old terms, including captions, table rows, appendix text, and reproducibility checklists.

## Figures and Tables

Every main-text figure or table should support a main claim. If it is useful but not central, move it to appendix and reference it briefly.

Put the headline result table near the main-results text, not in a benchmark or setup section. Keep long fine-grained tables, extended model panels, per-model breakdowns, and case studies in appendix unless they are central to the argument.

Use `\autoref{...}` consistently for figures and tables. Check for duplicate labels, stale references, and labels whose target moved after restructuring.

Captions should state what the reader should learn, not just describe the visual.

## TODO Handling

Do not fill unknown values from intuition. Preserve missing facts visibly.

Use red TODOs for missing factual values, validation numbers, citations, or concrete experimental results. Use blue TODOs for planned analysis. Blue TODOs should be at most 1-3 sentences and state what analysis is needed, why it matters, and what artifact should be added.

When results are incomplete, write around the current evidence honestly and mark the planned extension rather than making the current table carry claims it cannot support.

## Appendix Triage

Move the following out of the main text unless they are central:

- prompt calibration algorithms
- full schemas
- long annotation instructions
- extended model panels
- fine-category result tables
- per-model failure breakdowns
- long case studies
- repeated implementation details

Do not delete useful material merely because it disrupts the main narrative. Move it, compress it, or cite it from the main text.

## LaTeX Checks

Before editing, inspect structure and references with `rg`, including section titles, labels, figure/table refs, and terminology variants.

After editing, compile the main LaTeX file when feasible. Then check for undefined references, multiply defined labels, old terminology, misplaced appendix material, and stale figure/table references.

For layout-only requests, keep edits minimal: adjust table size, figure width, placement, spacing, or `\hspace` before rewriting content.
