# Replication Package — Sprint 2: Cost of Living Data

## Contents

```
/
├── README.md
├── FINDINGS.md            # Findings report (based on statistical analysis)
├── sprint_2.ipynb          # Analysis script (exported from Colab)
└── cost-of-living_v2.csv  # Dataset (Numbeo, via Kaggle)
```

---

## Environment

This notebook was written for **Google Colab**. No local installation is required.

All dependencies come pre-installed in Colab:

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Base plotting |
| `seaborn` | Statistical visualization |
| `scipy` | Q-Q plot and normality testing |

---

## How to Run

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Upload `sprint_2.py` via **File → Upload notebook** (or open it and paste the contents into a new notebook)
3. Upload `cost-of-living_v2.csv` to the Colab session storage by clicking the **folder icon** in the left sidebar → **Upload**
4. Confirm the file is at `/content/cost-of-living_v2.csv` (this is the path hardcoded in the script)
5. Run all cells in order: **Runtime → Run all**

---

## Dataset

- **Source:** [Kaggle — Global Cost of Living](https://www.kaggle.com/datasets/mvieira101/global-cost-of-living), originally scraped from [Numbeo](https://www.numbeo.com)
- **File:** `cost-of-living_v2.csv` (included in this package)
- **Size:** ~5,000 cities × 57 columns
- **Key filter applied:** Only rows where `data_quality == 1` are used in the analysis (~4,000 cities). Rows marked `0` have incomplete data and are excluded.

---

## What the Script Does

The analysis runs in five stages:

1. **Load and inspect** — reads the CSV, prints shape, and previews rows
2. **Rename columns** — maps short codes (`x1`–`x55`) back to human-readable names
3. **Filter for quality** — retains only complete records (`data_quality == 1`)
4. **Salary analysis** — descriptive statistics, histogram + KDE, Q-Q plot, country-level comparisons
5. **Multivariate exploration** — scatter plot (salary × rent × cappuccino cost), coefficient of variation across all columns, full correlation matrix with flagged strong correlations (r > 0.8) and inverse correlations (r < −0.4)

---

## Expected Outputs

Running all cells produces:

- Printed summary statistics (mean, median, std, skewness, kurtosis, IQR)
- 5 plots rendered inline:
  - Salary distribution histogram + KDE
  - Salary Q-Q plot
  - Average salary by country (top 20 / bottom 20)
  - Distribution of country-level average salaries
  - Scatter plot: salary × city-center rent, colored by cappuccino cost
  - Coefficient of variation bar chart (all columns)
  - Correlation heatmap (all numeric columns)
- Printed lists of strong positive and inverse correlations

---

## Notes

- All file paths are absolute Colab paths (`/content/...`). Do not change the CSV filename or location.
- City-level queries at the end of the script (e.g., New York) can be modified to inspect any city in the dataset.
