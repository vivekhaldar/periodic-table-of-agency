# AGENTS.md

## Purpose

This repository contains one authored artifact: **The Periodic Table of Agency**. It is a conceptual and interactive field chart for composing agentic systems from atomic operators.

The canonical deliverable is `index.html`.

## Design direction

- Preserve the industrial field-chart aesthetic: near-black drafting grid, warm off-white type, amber accent, condensed display typography, mono labels, and serif explanatory copy.
- Keep the interface editorial and diagrammatic. Do not convert it into a generic dashboard, card library, documentation theme, or framework-generated app.
- Maintain strong mobile behavior. Critical content and interactions must remain available below 640px.
- Respect reduced-motion preferences, keyboard focus, semantic headings, and readable contrast.

## Ontology invariants

- An atom is an irreducible **operator**, not an artifact, implementation modality, trigger condition, or already-composed mechanism.
- Bracket notation specializes an atom without creating a new one: `Tl[browse]`, `Vf[test]`, `Pl[revise]`.
- Keep category and member at different levels. If two candidates answer the same orthogonality question, they should not both be atoms.
- Dispatch retains the current execution context; Delegate creates a new agent context.
- Persist stores information; Checkpoint stores a resumable state of the run itself.
- Approval is an enforced human gate; Ask elicits missing information or preference.
- Branch fans out, Score ranks, and Merge synthesizes. Do not conflate them.
- Use only the documented bond types and strengths unless the legend, renderer, examples, and appendix are updated together.

## Source and reference rules

- Each atom must have one Harness Course link and one canonical reading in `references`.
- Do not modify the Harness Course repository from this project.
- Prefer primary papers, official technical documentation, or first-party engineering reports for readings.
- Formulas are schematic maps, not an executable grammar. Keep their left-to-right interpretation legible.

## Implementation constraints

- Keep the project zero-build and single-file unless Vivek explicitly approves an architectural change.
- Do not introduce a framework, package manager, bundler, analytics, or backend without approval.
- Avoid inline event-handler attributes; keep behavior in the existing script.
- Escape user- or data-derived HTML through the existing `esc` helper.
- Treat existing fonts as an external enhancement; the fallback stack must remain usable.

## Required synchronization

When adding, removing, or moving an atom, update all of the following:

1. Metadata and visible counts
2. Family filter labels
3. `atoms`
4. `references`
5. Orthogonality `questions`
6. Functional groups, molecules, and complexes using affected symbols
7. Appendix change notes and revision markers

Do not invent filler to reach a visually attractive element count.

## Verification

Before committing:

1. Parse the inline JavaScript with Node.
2. Confirm atomic numbers are unique and consecutive.
3. Confirm every atom has a reference and orthogonality question.
4. Confirm every formula token resolves to an atom, bond, strength, or documented complex placeholder.
5. Exercise every family filter.
6. Check at approximately 390px and 1440px viewport widths.
7. Confirm zero browser console errors and no page-level horizontal overflow.
8. Inspect `git diff --check` and `git status`; stage files explicitly by path.

## Git conventions

- Use `main` as the primary branch.
- Write concise imperative commit subjects.
- Do not commit local screenshots, browser traces, operating-system metadata, or generated test artifacts.
- Do not add AI attribution or co-author trailers to commits.
