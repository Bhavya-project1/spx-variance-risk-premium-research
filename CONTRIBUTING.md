# Contributing

This repository is an empirical research project. Contributions should improve the clarity, reproducibility, or validity of the analysis.

## Before changing the analysis

- State the research question or methodological issue being addressed.
- Keep the chronological train/test and walk-forward boundaries intact; do not introduce future information into historical signals.
- Distinguish observed market data from model-generated quantities and scenario assumptions.
- Document changes to model specifications, data definitions, trading assumptions, costs, and hedge rules.
- Do not present synthetic option prices or simulated P&L as historical executable results.

## Reproducibility

- Run the notebook from a clean kernel, from the first cell to the last.
- Record the run date, data sample, package versions, and any changed parameters.
- Preserve random seeds where stochastic procedures are used.
- Check that tables, plots, trade counts, and P&L reconciliations are consistent after a change.
- Explain any change in results caused by revised external data.

## Pull requests

Please include:

1. A concise description of the change and its motivation.
2. The cells or methods affected.
3. The validation performed and its outcome.
4. Any new limitations or assumptions introduced.

Avoid committing credentials, API tokens, private datasets, large temporary files, or local notebook checkpoints.
