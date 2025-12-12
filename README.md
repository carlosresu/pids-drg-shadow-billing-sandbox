# pids-drg-shadow-billing-sandbox

Exploratory RMarkdown notebooks that join DRG claim CSV exports into master tables for analysis and quality checks.

**Last Updated:** December 2025

---

## Progress Since June 2025

| Date | Milestone |
|------|-----------|
| **Jun-Aug 2025** | Initial ingest.Rmd with basic CSV joins |
| **Sep 2025** | Added composite key generation (`SERIES_LHIO_CLAIMNUMBER`) |
| **Oct 2025** | Added ingest_v2.Rmd with CF2/HCP source merging |
| **Nov 2025** | Added renv project for reproducible package versions |
| **Dec 2025** | Outputs master_table.csv and master_table_flat.csv |

### Current Status

- **Input:** DRG_INFO, DRG_PROCEDURE, DRG_DIAGNOSIS, DRG_WARNING_ERROR, DRG_TRAIL, DRG_RESULT CSVs
- **Output:** `data/master_table.csv`, `data/master_table_flat.csv`
- **Runtime:** data.table-based joins for performance

---

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
