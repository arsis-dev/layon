# Vision

*From field records to visual stories.* Last updated: 2026-09-30.

An ecologist imports field data. Layon understands it, derives predictions from it, and generates the pages that tell what it shows.

## Three pillars

1. **Understand the tables** — detect the role of each column (taxon, measurement, coordinates, date…) and structure the dataset. Tabular foundation models are candidates for this step; to be measured.
2. **Predict** — trait imputation, allometry, growth, survival and distribution with tabular foundation models (Kumo Tabular, TabICL) running locally, including on Apple Silicon.
3. **Tell** — generate visualisation pages (maps, distributions, taxon sheets, summaries) with generative UI, from a component contract and verifiable evaluators.

## Early findings

A first benchmark of 12 public ecological tasks (tree allometry, growth, survival, mortality, biomass, species distribution; Panama, China, Cambodia, Catalonia, Finland and Sweden, Madagascar, Oregon), with folds grouped by plot, site or species, 3 seeds × 5 folds, against tuned and domain baselines:

- Kumo Tabular, used without training, has the best mean rank (2.33 over 12 tasks, CatBoost 3.33), **but its advantage over strong baselines is small and not statistically significant** (median gain +0.005 to +0.009; Wilcoxon p ≥ 0.2 against CatBoost, tuned gradient boosting, random forest and TabICLv2).
- It helps most on small datasets and fails on some tasks: a simple log-log allometric model wins on crown area and boreal growth, and gradient boosting wins on tree survival.
- This matches recent findings that tabular foundation models lose their edge under grouped (non-i.i.d.) validation. Whether taxonomy-aware preparation changes the picture, for instance for trait imputation, is the next question.
- Apple Silicon (MPS) support for the underlying NVIDIA library is being contributed upstream ([NVIDIA/structured-data-models#1031](https://github.com/NVIDIA/structured-data-models/issues/1031)).

## Principles

- Open source under Apache-2.0, in line with the scientific Python ecosystem.
- Generic: no regional assumptions in the data model or the interface.
- Local first: data and models stay on the user's machine.
- Honest signals: a prediction shows its uncertainty (quantiles); a generated page cites its data.
- Short milestones, each validated by real use before adding another layer.

## Open questions

- First real user and first use case to validate.
- Storage: DuckDB, or the tensor types of `structured-data-models`.
- Shape: library and CLI first, or a desktop app from the start.
