# Vision

*From field records to visual stories.* Last updated: 2026-09-30.

An ecologist imports field data. Layon understands it, derives predictions from it, and generates the pages that tell what it shows.

## Three pillars

1. **Understand the tables** — detect the role of each column (taxon, measurement, coordinates, date…) and structure the dataset. A tabular foundation model used without any training already improves role detection from column values over a gradient-boosting baseline (macro-F1 0.60 → 0.68 on 2,540 annotated ecological columns).
2. **Predict** — trait imputation, allometry, growth, survival and distribution with tabular foundation models (Kumo Tabular, TabICL) running locally, including on Apple Silicon.
3. **Tell** — generate visualisation pages (maps, distributions, taxon sheets, summaries) with generative UI, from a component contract and verifiable evaluators.

## Early findings

A first benchmark of 18 ecological tasks, with folds grouped by plot, site or taxon:

- Kumo Tabular, without training, beats HistGradientBoosting on 16 of 18 tasks. The median gain is small (+0.014 R² or macro-F1) but clear on small datasets (303 trees: R² 0.78 vs 0.61).
- **Taxonomy matters most**: adding genus and family raises wood-density imputation for species absent from the context from R² 0.10 to 0.40. Ecology-aware preparation is worth more than a bigger model.
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
