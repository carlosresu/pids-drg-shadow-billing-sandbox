# Shadow billing sandbox (PIDS DRG)

Exploratory RMarkdown notebooks that join DRG claim CSV exports into master tables for analysis and quality checks.

## Data expected (place in `data/`)
- `DRG_INFO.csv`, `DRG_PROCEDURE.csv`, `DRG_DIAGNOSIS.csv`, `DRG_WARNING_ERROR.csv`, `DRG_TRAIL.csv`, `DRG_RESULT.csv`
- Optional enrichments: `CLAIMS HCP.csv`, `CLAIMS JAN TO JULY 2025.csv`

## Notebooks
- `ingest.Rmd` – baseline ingest/joins; builds composite key `SERIES_LHIO_CLAIMNUMBER` and writes `data/master_table.csv` and `data/master_table_flat.csv`.
- `ingest_v2.Rmd` – variant that also merges CF2/HCP sources and compares against the master.

## Running
Open in RStudio or render non-interactively:

```bash
Rscript -e "rmarkdown::render('ingest.Rmd')"
```

Use the bundled `renv/` project (or run `renv::restore()`) to install locked package versions; notebooks rely primarily on `data.table`. Outputs land under `data/`; rerun after refreshing the source CSVs.
