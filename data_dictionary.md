# Data Dictionary

Dataset: `data/clean/china_health_clean.csv` — 403 rows (31 provinces x 13 years, 2011-2023), 17 columns.
Unit of observation: one province in one year.

## Columns from the raw data (`data/raw/china_health_raw.xlsx - Sheet1.csv`)

| Variable | Raw column name | Description | Unit |
|---|---|---|---|
| `Year` | Year | Calendar year | 2011-2023 |
| `Province` | Province | Province-level administrative unit (31). Typos "Shangai" and "Guandong" corrected | text |
| `staff` | Health Personnel (per 1,000 population) | Total health personnel. Labelled "per 1,000" in the source but treated as a **total** | 10,000 persons |
| `beds` | Hospital Beds (per 1,000 population) | Total hospital beds. Labelled "per 1,000" in the source but treated as a **total** | 10,000 beds |
| `institutions` | Health Care Institutions (count) | Number of health care institutions | count |
| `visits` | Number of Visits (100 million) | Total outpatient visits | 100 million visits |
| `discharges` | Patients Discharged (10,000 person-times) | Total inpatient discharges | 10,000 person-times |
| `bed_util` | Hospital Bed Utilization Rate (%) | Share of bed capacity in use | percent |

## Merged-in variable (`data/raw/China province population - Sheet1.csv`)

| Variable | Description | Unit |
|---|---|---|
| `pop_10k` | Year-end resident population of the province | 10,000 persons |

## Derived variables (created in the notebook)

| Variable | Formula | Meaning | Unit |
|---|---|---|---|
| `beds_pc` | `beds / pop_10k * 1000` | Hospital beds per 1,000 people | beds per 1,000 |
| `staff_pc` | `staff / pop_10k * 1000` | Health personnel per 1,000 people | persons per 1,000 |
| `inst_pc` | `institutions / pop_10k` | Health care institutions per 10,000 people | institutions per 10,000 |
| `discharge_pc` | `discharges / pop_10k * 1000` | Inpatient discharges per 1,000 people | discharges per 1,000 |
| `visits_pc` | `visits * 10000 / pop_10k` | Outpatient visits per person per year | visits per person |
| `Region` | lookup by province | East, Central, West, or Northeast | category |

(`bed_util` is already a rate, so it is used as-is.)

## Region assignment
- **East:** Beijing, Tianjin, Hebei, Shanghai, Jiangsu, Zhejiang, Fujian, Shandong, Guangdong, Hainan
- **Central:** Shanxi, Anhui, Jiangxi, Henan, Hubei, Hunan
- **West:** Inner Mongolia, Guangxi, Chongqing, Sichuan, Guizhou, Yunnan, Xizang, Shaanxi, Gansu, Qinghai, Ningxia, Xinjiang
- **Northeast:** Liaoning, Jilin, Heilongjiang

## Missing data and cleaning notes
- 2024 was dropped: hospital bed utilization is missing for all provinces that year.
- No missing values remain in 2011-2023 (checked with `df.isna().sum()`).
- 2020-2022 are kept but flagged as COVID-affected years; the main regression uses 2019 (pre-COVID) and a 2023 comparison.
