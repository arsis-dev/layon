# Vision

*From field records to visual stories.* Last updated: 2026-09-30.

An ecologist imports field data. Layon understands it, derives predictions from it, and generates the pages that tell what it shows.

## Three pillars

1. **Understand the tables** — detect the role of each column (taxon, measurement, coordinates, date…) and structure the dataset. Tabular foundation models are candidates for this step; to be measured.
2. **Predict** — trait imputation, allometry, growth, survival and distribution with tabular foundation models (Kumo Tabular, TabICL) running locally, including on Apple Silicon.
3. **Tell** — generate visualisation pages (maps, distributions, taxon sheets, summaries) with generative UI, from a component contract and verifiable evaluators.

## Early findings

Measured with [Syntype](https://github.com/syntype/syntype), an open benchmark of tabular models on ecological data. Version 0.1 is a first pass: an independent review found issues that are being fixed (see the Syntype README), so these findings are provisional.

- **Species traits — a first signal on 4 databases.** On AusTraits, COMBINE, TetrapodTraits and AVONET, Kumo Tabular used without any training scored best on every trait tested, with species or whole genera held out. The evidence is limited: few independent targets (some overlap between databases), a row cap that favours in-context models, and no phylogenetic imputation baseline yet. It is a direction to test, not a general result.
- **Forest inventories — inconclusive.** Several v0.1 forest tasks were ill-defined (harvest counted as mortality, modelled heights, near-identity growth targets). The suite is being rebuilt; no conclusion can be drawn yet.

Trait imputation for poorly studied species remains the first use case worth validating with ecologists.

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
