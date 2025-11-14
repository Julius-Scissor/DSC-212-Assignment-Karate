# Karate Modularity Assignment

Author: Armaan-Singh 
Roll No.: IMS24041
Date: 2025-11-14

## Overview

This repository delivers a single, self-contained Jupyter notebook that implements recursive spectral modularity partitioning on Zachary's Karate Club network. The notebook performs the analysis end-to-end: it computes modularity-driven splits, records community assignments at each accepted split, and computes common node-level network metrics (degree centrality, betweenness, closeness, clustering coefficient) across iterations for longitudinal inspection.

## Scientific motivation

Community detection is a central problem in network science. Modularity measures how well a partition concentrates edges within groups relative to a random-graph baseline. The leading-eigenvector (spectral) approach finds bipartitions that locally improve modularity. Recursively applying this bipartitioning yields a hierarchical decomposition and an interpretable sequence of community refinements. Tracking node-level metrics through the recursion helps identify core versus boundary nodes and how node roles change as communities split.

## What the notebook implements

- Construction of the modularity matrix for a candidate node set, using degrees measured on the full network.
- Computation of the principal eigenvector of the modularity matrix and bipartition by the sign of its entries.
- Calculation of modularity gain ΔQ = (1/(4m)) sᵀ B s for the sign split; acceptance only when ΔQ > 0 and both parts are non-empty.
- Recursive splitting until no positive-gain splits remain (with an adjustable minimum part size parameter).
- Per-iteration recording of community assignments and node-level metrics for longitudinal analysis.
- Visualizations of the network colored by community assignment at each accepted split (embedded in the notebook).

## Reproducible instructions

1. Open a terminal in the repository root.

2. Create and activate a Python virtual environment, then install dependencies:
   - python -m venv .venv
   - source .venv/bin/activate    # macOS / Linux
   - .venv\Scripts\activate       # Windows (PowerShell)
   - pip install -r requirements.txt

3. Open and run the notebook:
   - jupyter lab DSC212_Karate_Modularity.ipynb
   - or
   - jupyter notebook DSC212_Karate_Modularity.ipynb

   Run all cells in order. The notebook performs the analysis and generates figures and CSV summaries inline and/or as files (the notebook writes its outputs when executed).

## Notes on results and interpretation

- The algorithm accepts only splits that produce a positive modularity gain; therefore the final partition is a greedy, hierarchical modularity-improving decomposition.
- Nodes that consistently show high centrality measures across iterations are structural cores; nodes whose betweenness increases before a split are frequently bridge-like.
- Use the notebook visualizations and the per-iteration metrics together to summarize how the network decomposes and how node roles evolve.
- The method is local and greedy (per split). It is appropriate for pedagogical demonstration and small-to-medium networks; for larger networks you may consider alternative implementations or optimizations.

## Parameters worth adjusting

- Minimum community size before attempting a split (stop_min_size).
- Minimal ΔQ threshold to avoid accepting splits with negligible improvement.
- Graph layout seed for reproducible visual placements.

## Reproducibility information

- Recommended Python: 3.9+
- Key packages are listed in requirements.txt. For full reproducibility include pip freeze output or the exact environment specification when submitting.

## Submission guidance

- The notebook is intended to be self-contained for grading. If your instructor requests exported artifacts (PNG images, CSVs), run the notebook and include those generated files in your submission package per your course instructions.

## References

- Newman, M. E. J. (2006). Modularity and community structure in networks. Proceedings of the National Academy of Sciences.
