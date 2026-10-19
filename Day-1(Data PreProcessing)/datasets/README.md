# ML Data Preprocessing Mastery Pack

All datasets in this pack are synthetic and created for educational practice. They intentionally contain a variety of data-quality issues. They are not real customer, employee, medical, or sensor records.

## Files
- `01_customer_churn_messy.csv` — mixed tabular data, missing values, outliers, inconsistent categories, duplicate rows.
- `02_housing_prices.csv` — skewed numerical features, price outliers, date parsing, categorical cleaning.
- `03_medical_appointments.csv` — imbalanced binary target, missingness, invalid ages/wait times, category inconsistencies.
- `04_retail_transactions.csv` — transaction data, date/time parsing, derived revenue, duplicates, invalid discounts/units.
- `05_employee_attrition.csv` — ordinal categories, missing values, sentinel values, invalid ratings and tenure.
- `06_student_performance.csv` — beginner-friendly numerical and categorical practice.
- `07_iot_sensor_timeseries.csv` — time series, missing readings, anomalies, timestamps; preserve chronological order.
- `08_survey_responses.csv` — ordinal survey responses, high-cardinality categories, placeholders, income missingness that is intentionally related to higher values.
- `all_datasets_workbook.xlsx` — all eight datasets, one per worksheet.
- `PRACTICE_ROADMAP.md` — suggested sequence and checklist.

## Recommended practice order
1. Begin with Dataset 06 (student performance).
2. Move to Dataset 01 (customer churn).
3. Practice dates, duplicates, and derived features with Dataset 04.
4. Practice outliers and skew with Dataset 02.
5. Practice category encoding and imbalanced classification with Dataset 03.
6. Practice ordinal features and sentinel values with Dataset 05.
7. Practice time-aware validation with Dataset 07.
8. Practice high-cardinality categories and missingness assumptions with Dataset 08.

## Techniques to practice
- Data inspection: shape, dtypes, info, describe, value counts
- Missing values: counts, percentages, patterns, row/column deletion, mean/median/mode/constant imputation, missing indicators, KNN imputation
- Hidden missing markers: `Unknown`, `N/A`, `-999`, and similar values (decide whether they are truly missing)
- Data quality: duplicates, inconsistent capitalization/whitespace, impossible values, invalid dates and units
- Outliers: IQR, z-score, visualization, capping/transformation/retention decisions
- Categorical features: one-hot, ordinal, frequency and leakage-safe target encoding
- Numerical features: standardization, min-max scaling, robust scaling, skew transformations
- Dates: parsing, extracting date parts, chronological splitting
- Feature engineering and selection
- Train/validation/test splits, stratification, grouping, time-based splits
- `Pipeline` and `ColumnTransformer`
- Leakage prevention and baseline evaluation

## Important
- Do not assume every unusual value is wrong. Investigate before changing it.
- Do not impute target labels casually.
- Split before fitting learned preprocessing steps. Fit imputation/scaling/encoding on training data only.
- For time series, don't randomly shuffle rows if it would let future information influence past predictions.
- Some columns are identifiers and should not automatically be used as predictive features.
- Dataset 08 intentionally has higher income values more likely to be missing. This is a teaching example of why simple imputation can be biased; the true missingness mechanism cannot generally be established from observed data alone.
