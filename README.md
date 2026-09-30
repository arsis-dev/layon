# Layon

*From field records to visual stories.*

Layon turns ecological field data (forest inventories, plots, occurrences, traits) into predictions and generated visual pages. It combines tabular foundation models, which predict from tables without task-specific training, with generative UI, which builds the pages that tell what the data shows.

In French forestry, a *layon* is the path cut through the forest to reach and survey inventory plots. Layon follows that path from the field record to the story.

## Status

Early research project. There is no usable code yet; see [docs/VISION.md](docs/VISION.md) for the direction.

## Development

```bash
uv sync
uv run pytest
uv run ruff check .
```

## License

Layon is licensed under the [Apache License 2.0](LICENSE). See [NOTICE](NOTICE) for attributions.
