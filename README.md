# Candidate defense presentation

Scientific defense presentation for the dissertation:

> Mathematical Modeling and Motion Planning for Robotic Manipulation of
> Deformable Linear Objects

The compiled deck contains **26 main slides and 7 backup slides**. Its structure
follows the two supplied defense templates: formulation and provisions first,
then each method followed immediately by its experimental evidence.

## Files

- main.tex — presentation source
- theme.tex — restrained white-and-blue academic layout
- speaker_notes.md — slide-by-slide talk track and timing
- assets/ — figures already localized for the presentation
- main.pdf — compiled 16:9 presentation

Several result slides intentionally reference the original dissertation figures
in ../thesis_phd_math/images/. This keeps the plots and experimental photographs
identical to the dissertation instead of recreating them as presentation graphics.

## Build

From defense_presentation/, run:

    latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex

The project uses pdfLaTeX and standard TeX Live packages. No Biber pass, network
access, external font, or shell escape is required. The adjacent
thesis_phd_math/ directory must remain available because the result figures are
read from it.

## Main-slide sequence

1. Title
2. Relevance and applications
3. Existing approaches and research gap
4. Goal, object, subject, and objectives
5. Research map: problem → limitation → result → verification → chapter
6. Provisions presented for defense
7. Ordered DLO state and Virtual Feature Points
8. Complete mass--spring DLO model
9. LI/ILI/ALI intermediary-shape planning
10. Diminishing-rigidity Jacobian
11. Constrained dual-arm shape control
12. Shape-control simulation design
13. Simulation results for point count \(N\)
14. ALI step-size \(\lambda\) study
15. Physical experimental setup
16. Physical U/L/S/M results
17. Opposite-concavity physical results
18. Global Cable Routing problem
19. Global Cable Routing numerical method
20. Complete-motion validation
21. Representative computed routes
22. Ten-scenario benchmark table
23. MuJoCo execution and error table
24. Main scientific results and established scope
25. Publications and implementation
26. Closing

## Evidence restored in the main deck

- Original U/L/S/M intermediary-profile figures.
- Original simulated final-shape figures for the point-count study.
- Exact statement that all 32 tasks completed, while six reached the iteration
  cap before the strict \(e_{\mathrm{mean}}<0.01L\) condition.
- Original \(\lambda\)-error and \(\lambda\)-iteration plots.
- Original KUKA setup photograph and physical final-shape overlays.
- Exact simulation-versus-physical U/L/S/M error table.
- Original opposite-concavity experimental sequences and error table.
- Representative GCR routes, the ten-scenario numerical table, and MuJoCo
  snapshots with scenario-by-scenario errors.

## Claim boundaries

- The mass--spring model includes length, bending, and damping forces. It is an
  evaluation model, not a separate novelty and not a parameter input to the
  controller.
- The controller uses the **diminishing-rigidity Jacobian**, not a method named
  “Geometric Jacobian.”
- The cable is marker-free; one gripper is marked only to establish point order.
- Physical experiments validate planar, obstacle-free shape control.
- Global Cable Routing is validated by C++ benchmarks and MuJoCo simulation; no
  physical routing experiment is claimed.
- All 10,000 tested GCR runs satisfied the stated predicates in the ten tested
  scenarios. This is empirical evidence, not a completeness guarantee.

## Backup slides

The seven backup slides cover abbreviations, detailed mass--spring forces, the
ALI construction, physical error histories, GCR admissibility, the complete
seven-column GCR benchmark, and final opposite-concavity overlays.
