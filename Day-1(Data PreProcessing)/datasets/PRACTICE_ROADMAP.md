# Preprocessing Practice Roadmap

## Level 1 — Beginner
### Dataset 06: Student performance
- [ ] Inspect dimensions, types, and summary statistics
- [ ] Identify missing values using `isnull()` and `isnull().sum()`
- [ ] Calculate missing percentages
- [ ] Compare row deletion, mean/median imputation, and mode/constant imputation
- [ ] Identify numeric and categorical columns
- [ ] One-hot encode nominal features and ordinal-encode `stress_level` only with an explicit order
- [ ] Scale numerical features
- [ ] Split data before fitting preprocessors

## Level 2 — Core tabular preprocessing
### Dataset 01: Customer churn
- [ ] Find duplicate records and investigate them
- [ ] Inspect numeric outliers and invalid support-ticket counts
- [ ] Clean whitespace and inconsistent binary labels
- [ ] Build numerical and categorical pipelines
- [ ] Use `churn` as target; exclude identifiers
- [ ] Evaluate with appropriate classification metrics

### Dataset 02: Housing prices
- [ ] Explore skewed distributions
- [ ] Investigate area and price outliers
- [ ] Parse dates and clean categories
- [ ] Compare standard and robust scaling
- [ ] Use a regression metric such as MAE or RMSE

## Level 3 — Data quality and evaluation
### Dataset 03: Medical appointments
- [ ] Investigate invalid age and waiting-time values
- [ ] Handle class imbalance in evaluation
- [ ] Choose stratified validation where appropriate
- [ ] Do not use appointment IDs as features without justification

### Dataset 04: Retail transactions
- [ ] Parse timestamps
- [ ] Check duplicate transactions
- [ ] Investigate negative units and discounts above 100%
- [ ] Recompute revenue only after checking the business definition
- [ ] Create date-derived features without leakage

### Dataset 05: Employee attrition
- [ ] Investigate `-999` and `Unknown`
- [ ] Treat job level as ordinal only if the order is justified
- [ ] Investigate satisfaction scores outside the expected range
- [ ] Compare missing indicators and imputation choices

## Level 4 — Advanced considerations
### Dataset 07: IoT sensor time series
- [ ] Preserve chronological order
- [ ] Identify gaps and sensor-specific anomalies
- [ ] Use time-based validation
- [ ] Avoid filling future values into past observations when this would leak information

### Dataset 08: Survey responses
- [ ] Handle high-cardinality `region_code`
- [ ] Decide how to treat `Unknown` and `N/A`
- [ ] Inspect missingness patterns by observed variables
- [ ] Discuss why income missingness may be informative
- [ ] Explain why MNAR cannot generally be proven from observed data alone

## Final project
- [ ] Choose one dataset
- [ ] Write a preprocessing plan before coding
- [ ] Build a `ColumnTransformer` and `Pipeline`
- [ ] Fit transformations on training data only
- [ ] Compare a baseline with a justified preprocessing workflow
- [ ] Document every cleaning decision and its reason
