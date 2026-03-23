# Automatidata NYC Taxi Analytics

An end-to-end analytics project based on the **2017 NYC Yellow Taxi** dataset developed as part of the **Google Advanced Data Analytics** program. The project moves from data inspection and exploratory analysis to statistical testing, fare prediction, and classification modeling for tipping behavior.

## Business problem

The goal of this project is to transform raw taxi trip data into insights and predictive tools that could support operational decisions. The analysis focuses on three main questions:

1. **Is the data reliable enough for analysis and modeling?**
2. **Can fare amount be estimated from trip-related features?**
3. **Can we predict which riders are more likely to leave a generous tip without using the result in unfair or harmful ways?**

## Project scope

This repository consolidates the work completed across the Automatidata workflow:

- **Course 1** — Data inspection and initial business understanding
- **Course 2** — Exploratory data analysis and visualization
- **Course 3** — Statistical testing
- **Course 4** — Multiple linear regression for fare prediction
- **Course 5** — Machine learning classification for generous tipping behavior

## Dataset

Main dataset:
- `2017_Yellow_Taxi_Trip_Data.csv`

Additional engineered-support file:
- `nyc_preds_means.csv`

> Place both CSV files inside the `data/` folder before running the notebooks.

### Observed data profile

- **22,699 rows × 18 columns**
- **0 missing values**
- 3 object columns:
  - `tpep_pickup_datetime`
  - `tpep_dropoff_datetime`
  - `store_and_fwd_flag`

### Data quality issues identified

- `total_amount` contains **negative values** and **extreme outliers**
- `RatecodeID` includes invalid values such as **99**
- `trip_distance` contains **0.00** values
- cash tips are structurally limited in `tip_amount`, so tip modeling must focus on card payments

## Key results

### Course 1 — Data inspection

- `payment_type` counts:
  - Card: **15,265**
  - Cash: **7,267**
  - No charge: **121**
  - Dispute: **46**
- Mean tip:
  - Card: **~2.73**
  - Cash: **0.00**
- Vendor distribution:
  - Vendor 1: **10,073**
  - Vendor 2: **12,626**

### Course 3 — Statistical analysis

A two-sample t-test was used to compare `fare_amount` between card and cash payments.

- **t ≈ 6.87**
- **p ≈ 6.8e-12**
- Mean fare:
  - Card: **~13.43**
  - Cash: **~12.21**

This suggests the difference is statistically significant in the sample.

### Course 4 — Fare prediction regression

Multiple linear regression was used to predict `fare_amount` based on engineered trip features.

- **R² ≈ 0.868**
- **MAE ≈ 2.13**
- **RMSE ≈ 3.79**

Most influential drivers:
- `mean_distance`
- `mean_duration`

### Course 5 — Generous tipper classification

The classification task predicts whether a rider leaves a **generous tip (≥20%)**.

- Modeling restricted to **card payments only**
- Final modeling dataset: **15,265 rows × 348 columns**
- Class balance: approximately **52.6% generous**

Model performance on test data:

**Random Forest**
- Accuracy: **~0.717**
- Precision: **~0.696**
- Recall: **~0.820**
- F1: **~0.753**

**XGBoost**
- F1: **~0.752**

Key variables:
- `VendorID`
- `passenger_count`
- `predicted_fare`
- `mean_distance`
- `mean_duration`

## Ethical considerations

This project explicitly avoids harmful uses of prediction outputs.

- The tip model should **not** be used to deny service or deprioritize riders.
- Since cash tipping is not fully observable in the dataset, any tipping model has important limitations.
- Threshold selection should reflect business costs carefully, especially if false positives could frustrate drivers.

## Repository structure

```text
automatidata-nyc-taxi-analytics/
├── data/
├── notebooks/
├── reports/
├── linkedin/
├── tableau/
├── interview/
├── images/
├── README.md
├── requirements.txt
└── .gitignore
```

## Notebooks

- `01_data_inspection.ipynb`
- `02_eda_visualization.ipynb`
- `03_statistical_testing.ipynb`
- `04_fare_prediction_regression.ipynb`
- `05_generous_tipper_classification.ipynb`
- `06_final_recommendations.ipynb`

## Tools used

- Python
- pandas
- numpy
- matplotlib
- seaborn
- scipy
- statsmodels
- scikit-learn
- xgboost
- Jupyter Notebook
- Tableau

## Tableau

Add your Tableau Public dashboard link here once published:

`PASTE_YOUR_TABLEAU_LINK_HERE`

## GitHub

Add your GitHub repository link here once published:

`PASTE_YOUR_GITHUB_LINK_HERE`

## How to run

1. Clone the repository
2. Place the CSV files in the `data/` folder
3. Install dependencies

```bash
pip install -r requirements.txt
```

4. Open the notebooks in order

## Notes

This repository was assembled from completed course deliverables and documented results. Where outputs are summarized in markdown, they reflect the validated results obtained during the project workflow.