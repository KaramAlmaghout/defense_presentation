# Candidate defense presentation

This folder is a self-contained, Overleaf-ready Beamer project for the dissertation
“Mathematical Modeling and Motion Planning for Robotic Manipulation of Deformable
Linear Objects.”

The compiled deck contains 27 main slides planned for 23 minutes 45 seconds and seven
appendix slides. Its visual language combines the row-based research-landscape diagram
from slide 2 of `Thesis presentation.pdf` with the restrained blue academic styling of
`presentation2.pdf`.

## Files

- `main.tex` — complete presentation, including hidden `\note{...}` timing cues
- `theme.tex` — colors, typography, footer, blocks, and reusable diagram styles
- `publications.bib` — BibTeX records used to typeset the publication citations
- `speaker_notes.md` — rehearsable slide-by-slide talk track and cumulative timing
- `assets/` — local copies of all figures used by the presentation
- `main.pdf` — compiled presentation

No network access, external font, or shell escape is required. The publication slide is
generated from `publications.bib` using a compact author--title--venue citation format
with the Biber backend.

## Build locally

From this folder, run:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

The project uses pdfLaTeX and standard TeX Live packages (`beamer`, `tikz`,
`pgfplots`, `mathtools`, `biblatex`, and `appendixnumberbeamer`). `latexmk`
automatically invokes Biber when the bibliography data change.

## Use in Overleaf

1. Upload this entire folder as a new project, or zip the folder and choose
   **New Project → Upload Project**.
2. Set `main.tex` as the main document.
3. Select **pdfLaTeX** as the compiler.
4. Compile. All figure paths are relative to `assets/`, so no path editing is needed.

## Defense structure

The main narrative is:

1. application problem and research gap;
2. formal mathematical formulation, goal, and independent research methodologies;
3. ordered marker-free state reconstruction with Virtual Feature Points;
4. length-feasible ALI paths and geometry-based constrained shape control;
5. Global Cable Routing with ordered swept-transition feasibility;
6. computational, physical, and independent simulation evidence;
7. four principal statements, scientific significance, publications, and conclusions.

Five scientific novelty results are identified explicitly in the main narrative. The
detailed correspondence to specialty 1.2.2 is retained as the first appendix slide for
committee discussion.

Claim boundaries are deliberately explicit: the mass–spring model is a validation
instrument rather than a claimed novelty; physical experiments validate shape control;
GCR is validated computationally and in MuJoCo; and 10,000 successful tested routing
runs are reported as empirical evidence, not as a universal guarantee.
