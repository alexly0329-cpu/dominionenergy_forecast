# Dominion Energy Load Forecast

This project develops and evaluates load forecasts for Dominion Energy demand and related capital planning scenarios. It combines historical load data, weather inputs, baseline forecasting, probabilistic pipeline outputs, Monte Carlo simulation, and capital-rate modeling.

## Project goal

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

all: ingest baseline pipeline mc model sens bench
ingest: ; python src/01_ingest_load.py && python src/02_ingest_weather.py
baseline: ; python src/03_baseline_forecast.py
pipeline: ; python src/04_pipeline_extract.py && python src/05_pipeline_probability.py
mc: ; python src/06_monte_carlo.py
model: ; python src/07_capital_rate_model.py
sens: ; python src/08_sensitivity.py
bench: ; python src/09_benchmark.py
