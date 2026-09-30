# Vision

*From field records to visual stories.* Last updated: 2026-09-30.

An ecologist imports field data. Layon understands it, derives predictions from it, and generates the pages that tell what it shows.

## Three pillars

1. **Understand the tables** — detect the role of each column (taxon, measurement, coordinates, date…) and structure the dataset. Tabular foundation models are candidates for this step; to be measured.
2. **Predict** — trait imputation, allometry, growth, survival and distribution with tabular foundation models (Kumo Tabular, TabICL) running locally, including on Apple Silicon.
3. **Tell** — generate visualisation pages (maps, distributions, taxon sheets, summaries) with generative UI, from a component contract and verifiable evaluators.

## Early findings

Measured with [Syntype](https://github.com/syntype/syntype), an open benchmark of tabular models on ecological data (grouped validation, domain and machine-learning baselines, leakage-audited targets):

- **Species traits** (8 traits from AusTraits, COMBINE, TetrapodTraits and AVONET; species or whole genera held out): Kumo Tabular, used without any training, is best on all 8 traits and in all 4 databases. Against CatBoost the median gain is +0.021 R² (8/8 traits, Wilcoxon p = 0.008, the smallest p possible with 8 traits); the edge narrows but holds when whole genera are held out (6/8). Taxonomy matters: removing genus, family and order drops some traits sharply (seed mass 0.82 → 0.55).
- **Forest inventories** (11 tasks: allometry, growth, survival, mortality, distribution; plots or sites held out): the advantage is small and not significant; log-log allometry and gradient boosting win some tasks.
- A light ecological fine-tuning of the small Kumo model (800 steps, leave-one-database-out) brought no measurable gain; model size mattered more.

Trait imputation for poorly studied species is therefore the first use case worth validating with ecologists.

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
