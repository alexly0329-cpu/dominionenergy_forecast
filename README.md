#dc-load-forecast/
├── README.md
├── requirements.txt
├── Makefile
├── config.yaml                 # all assumptions live here
├── data/
│   ├── raw/                    # downloaded, never edited
│   ├── interim/
│   └── processed/
├── src/
│   ├── 01_ingest_load.py       # EIA-930 hourly demand
│   ├── 02_ingest_weather.py    # NOAA/Meteostat
│   ├── 03_baseline_forecast.py
│   ├── 04_pipeline_extract.py  # LLM-assisted extraction
│   ├── 05_pipeline_probability.py
│   ├── 06_monte_carlo.py
│   ├── 07_capital_rate_model.py
│   ├── 08_sensitivity.py
│   ├── 09_benchmark.py
│   └── utils.py
├── model/
│   └── capital_rate_model.xlsx # mirrors 07 for employer-friendly viewing
├── outputs/
│   ├── figures/
│   └── tables/
├── report/
│   ├── report.md (or .docx)
│   ├── deck.pptx
│   └── assumptions_register.csv
└── prompts/
    └── extraction_prompt.md

all: ingest baseline pipeline mc model sens bench
ingest: ; python src/01_ingest_load.py && python src/02_ingest_weather.py
baseline: ; python src/03_baseline_forecast.py
pipeline: ; python src/04_pipeline_extract.py && python src/05_pipeline_probability.py
mc: ; python src/06_monte_carlo.py
model: ; python src/07_capital_rate_model.py
sens: ; python src/08_sensitivity.py
bench: ; python src/09_benchmark.py
