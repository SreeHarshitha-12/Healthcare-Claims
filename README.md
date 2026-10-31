# Healthcare Claims Analytics

An end-to-end analytics project exploring healthcare admissions, insurance claims, billing patterns, medical conditions, and length of stay across **55,500 patient records**.

The project combines:

- **Python** for exploratory data analysis and visualisation
- **PostgreSQL** for reusable analytical queries
- **Tableau** for an interactive dashboard

## Project Highlights

- Compared claim volume, average billing, and total billed amount by insurance provider
- Ranked medical conditions by total healthcare cost
- Detected unusual billing values using statistical z-scores
- Analysed length of stay and cost per day
- Tracked monthly admission and billing trends with month-over-month changes
- Identified data-quality issues, including inconsistent name capitalisation and negative billing values

## Repository Structure

```text
.
├── data/
│   └── healthcare_dataset.csv       # Source dataset
├── python/
│   ├── healthcare_eda.ipynb         # Python EDA notebook
│   ├── admission_trends.png
│   ├── billing_distribution.png
│   ├── condition_analysis.png
│   └── los_admission_analysis.png
├── sql/
│   └── healthcare_analysis.sql      # PostgreSQL analysis queries
└── tableau/
    ├── healthcare_dashboard.html    # Dashboard export
    └── dashboard_screenshot.png
```

## Dataset

The CSV contains 55,500 synthetic healthcare records with fields covering:

- Patient demographics and blood type
- Medical condition and medication
- Admission and discharge dates
- Hospital and attending doctor
- Insurance provider
- Billing amount and room number
- Admission type and test results

The analysis uses the [Healthcare Dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset) from Kaggle. The data is included in this repository for reproducibility.

## Key Findings

- Five insurance providers contribute to the claims dataset, with broadly similar claim shares.
- Diabetes has the highest total billed amount among the six medical conditions.
- Billing amounts show a wide spread, with negative values requiring data-quality review.
- Length of stay reaches 30 days in the dataset; cost per day varies substantially across records.
- The data covers 61 months of admissions, enabling monthly volume and billing trend analysis.

## Getting Started

### Python EDA

Install the required Python packages:

```bash
pip install pandas matplotlib seaborn jupyter
```

Start Jupyter from the repository root:

```bash
jupyter notebook python/healthcare_eda.ipynb
```

The notebook loads `data/healthcare_dataset.csv`, performs exploratory analysis, and generates the charts stored in `python/`.

### PostgreSQL Analysis

The SQL script is written for PostgreSQL and expects the CSV to be loaded into a table named `patients`. Its queries demonstrate:

- Aggregations and summary statistics
- Common table expressions (CTEs)
- Ranking and window functions
- Month-over-month comparisons with `LAG`
- Length-of-stay calculations
- Billing anomaly detection with z-scores

After loading the data into PostgreSQL, run:

```bash
psql -d <database_name> -f sql/healthcare_analysis.sql
```

The CSV column names should be mapped to the snake_case names used by the queries, such as `billing_amount`, `medical_condition`, `date_of_admission`, and `discharge_date`.

### Tableau

Open `tableau/healthcare_dashboard.html` in a browser to view the exported dashboard. A preview image is available at `tableau/dashboard_screenshot.png`.

## Notes

- The dataset is synthetic and should not be used for clinical, insurance-pricing, or patient-care decisions.
- Billing anomalies are analytical flags, not confirmed fraud or billing errors.
- The SQL analysis uses PostgreSQL-specific functions such as `DATE_TRUNC`, `TO_CHAR`, and `STDDEV`.

## License

This repository is intended for educational and portfolio use. Review the original dataset's Kaggle licensing terms before redistributing the data.
