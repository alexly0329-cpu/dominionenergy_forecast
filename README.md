# Dominion Energy Load Forecast

A probabilistic forecast of data center electricity demand in Dominion Energy Virginia's territory (PJM DOM zone), 2025–2035, and what serving it means for capital spending, rate base, customer rates and utility earnings.
Author: Alexandre Ly

## Project goal

1. **Baseline:** pulls hourly load (EIA-930) and weather. It removes existing data center load, then fits a weather-normalized model and validates it on held-out years.
2. **Pipeline:** converts a sourced, stage-tagged list of data center projects into probability-weighted load, using Low/Base/High scenarios and a Monte Carlo simulation with shared risk across projects.
3. **Capital and rates:** translates new load into accredited capacity (PJM FPR and ELCC), capital by technology, rate base, revenue requirement, rates and earnings, and compares the result against a no-new-data-center counterfactual.
4. **Risk:** runs a tornado sensitivity, a stranded-load stress test, and a GS-5-style large-load tariff (who pays).
5. **Report:** writes a Word report with every chart, table, assumption source and an MLA Works Cited list.

The repository supports:
- hourly and daily demand forecasting
- weather-informed adjustments
- probabilistic scenario generation
- capital rate modeling
- benchmarking against baseline forecasts

The core objective is to estimate future system load with uncertainty and translate those forecasts into capital planning inputs.

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── Makefile
├── config.yaml
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
├── src/
│   ├── 01_ingest_load.py
│   ├── 02_ingest_weather.py
│   ├── 03_baseline_forecast.py
│   ├── 04_pipeline_extract.py
│   ├── 05_pipeline_probability.py
│   ├── 06_monte_carlo.py
│   ├── 07_capital_rate_model.py
│   ├── 08_sensitivity.py
│   ├── 09_benchmark.py
│   └── utils.py
├── model/
│   └── capital_rate_model.xlsx
├── outputs/
│   ├── figures/
│   └── tables/
├── report/
│   ├── report.md
│   ├── deck.pptx
│   └── assumptions_register.csv
├── prompts/
│   └── extraction_prompt.md
└── .gitignore
```
## How to run
```text
pip install -r requirements.txt
jupyter lab

```
Open `dc_load_model.ipynb`, then use **Kernel → Restart Kernel and Run All Cells**.

- **Test run:** leave `SYNTHETIC = True` to run everything on generated test data. Outputs go to `*_synthetic/` folders.
- **Real run:** set `SYNTHETIC = False`, add a free EIA API key (https://www.eia.gov/opendata/register.php) and fill in the three input files. The notebook creates templates for them on its first run:
  - `data/raw/dc_historical_connected_mw.csv`: connected data center MW by year, with sources
  - `data/processed/pipeline.csv`: one row per project, with a source URL and a capacity quote
  - `data/raw/external_forecasts.csv`: official PJM / IRP forecasts used for benchmarking

## Outputs

| Folder | Contents |
|---|---|
| `outputs/tables/` | All result tables (CSV) |
| `outputs/figures/` | All charts (PNG) |
| `model/capital_rate_model.xlsx` | All tables in one workbook |
| `report/report.docx` | Full written report |

## Assumptions

Every input and its source is listed in Appendix A of the report. Inputs without a published source are labeled "Assumption", and the most influential ones are tested in the sensitivity analysis.

Do not commit your EIA API key.
