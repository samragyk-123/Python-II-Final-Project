# Healthcare Resources and Service Use Across China's Provinces (2011-2023)

**Research question:** How does healthcare resource availability (health personnel, hospital beds, facilities) vary across provinces in China, and how is it associated with the utilization of healthcare services (outpatient visits, inpatient discharges, bed utilization rate)?

**Main finding:** In 2019, provinces with more beds per 1,000 people had substantially more inpatient discharges per 1,000 (OLS slope ~33, R-squared = 0.63), while outpatient visits are concentrated in the East, where beds per person are lowest. These are associations, not causal effects.

## Repository structure

```
Python-II-Final-Project/
├── README.md
├── data_dictionary.md
├── data/
│   ├── raw/        # original files, never edited
│   └── clean/      # china_health_clean.csv (output of the notebook)
├── notebooks/
│   └── china_health_analysis.ipynb   # all cleaning + analysis code
├── figures/        # PNG figures used in the report
└── report/
    └── China_Healthcare_Resources_Report.pdf
```

## Data sources
- National Bureau of Statistics of China, provincial health statistics (data.stats.gov.cn), 31 provinces, 2011-2023.
- Provincial population: National Bureau of Statistics of China

See `data_dictionary.md` for every variable and unit.

## How to reproduce
1. Open `notebooks/china_health_analysis.ipynb` in Google Colab.
2. Run all cells top to bottom (Runtime > Run all). The notebook reads the raw CSVs directly from this repository, cleans them, merges population, builds per-capita variables, and runs the descriptive statistics, correlations, and regression.
3. The cleaned file is written to `data/clean/china_health_clean.csv`.

Python packages: `pandas`, `numpy`, `seaborn`, `matplotlib`, `statsmodels` (all preinstalled in Colab).

## Cleaning steps (summary)
1. Rename columns; fix province typos ("Shangai", "Guandong").
2. Drop 2024 (bed utilization missing for all provinces).
3. Merge provincial population; confirm no missing values.
4. Treat the "per 1,000 population" columns as totals and compute true per-capita measures.
5. Add a `Region` column (East / Central / West / Northeast).

## Limitations
Observational provincial data (association, not causation); possible confounding by age and income; ecological fallacy; only 31 provinces; COVID-19 distorts 2020-2022.
