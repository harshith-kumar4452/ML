## Topic: Data Preprocessing

**Goal:** Understand how to turn raw data into reliable model inputs, implement a preprocessing workflow in Python, and avoid common mistakes that lead to misleading model performance.

---

## 1. Learning Outcomes

By the end of Day 1, I should be able to:

- Inspect a dataset and understand its structure, data types, and quality.
- Identify and handle missing values.
- Detect outliers and decide whether they should be retained, transformed, capped, or corrected.
- Encode categorical variables appropriately.
- Explain normalization and standardization, and know when scaling matters.
- Split data correctly into training, validation, and test sets.
- Explain data leakage and prevent it with pipelines.
- Build a basic preprocessing pipeline using pandas and scikit-learn.
- Evaluate preprocessing choices using validation data and an appropriate metric.

---

## 2. Concepts to Cover

### A. Dataset Inspection and Exploratory Data Analysis (EDA)

- Rows, columns, features, and target variable
- Numerical vs. categorical features
- Data types and incorrect data types
- Dataset shape, column names, and summary statistics
- Unique values and category frequencies
- Duplicate rows and duplicate identifiers
- Invalid values, inconsistent units, and inconsistent formats
- Target distribution and class imbalance
- Correlation and feature relationships (introductory level)

**Useful tools:** `pandas`, `df.head()`, `df.info()`, `df.describe()`, `df.isna().sum()`, `df.nunique()`, `df.duplicated().sum()`, `value_counts()`

### B. Handling Missing Values

- What missing values represent: `NaN`, `None`, and blank values
- Finding and measuring missingness
- Row deletion vs. column deletion
- Mean imputation
- Median imputation
- Mode imputation
- Constant-value imputation
- K-Nearest Neighbors (KNN) imputation
- Missing-indicator features
- Choosing an imputation method based on the data
- Missingness patterns and when missingness itself may be informative

**Important points:**
- Do not automatically replace missing values with zero.
- The mean can be affected by extreme values; the median is more robust.
- Imputation values must be learned from training data only.
- KNN imputation can be sensitive to feature scales, distance choices, and dataset size.

### C. Handling Outliers

- What an outlier is
- Data errors vs. genuine extreme observations
- Interquartile range (IQR) method
- Z-score method
- Box plots and distribution plots
- Removing, capping, or retaining outliers
- Log and other transformations
- Robust scaling
- How outliers affect mean, standard deviation, and some models

**Important points:**
- An outlier is not automatically an error.
- Do not remove observations without understanding the problem and the evaluation goal.
- Fit any learned thresholds or transformations using training data only.

### D. Categorical Data Encoding

- Nominal vs. ordinal categories
- One-hot encoding
- Ordinal encoding
- Label encoding: where it is and is not appropriate
- Frequency/count encoding (introductory)
- Target encoding (introductory)
- Handling unseen categories
- High-cardinality categorical features

**Important points:**
- Arbitrary integer labels can create a false sense of order.
- Ordinal encoding is appropriate only when a meaningful order exists.
- Target encoding can leak target information unless performed carefully, for example with out-of-fold calculations.
- One-hot encoding may create many columns for high-cardinality features.

### E. Feature Scaling and Transformation

- Why features have different scales
- Standardization / Z-score scaling
- Min-max normalization
- Robust scaling
- Log transformation and skewed distributions
- When scaling is useful
- When scaling is usually unnecessary

**Know the model differences:**
- Scaling is often important for KNN, K-means, SVM, PCA, and many gradient-based models.
- Decision trees and most tree-based ensembles generally do not require standard scaling.
- Scaling does not automatically make every dataset or model better.

### F. Feature Extraction and Feature Engineering

- Difference between feature extraction and feature selection
- Creating useful features from dates, text, or existing columns
- Converting text into numerical representations (overview)
- Basic date features: year, month, day, weekday
- Domain knowledge and meaningful feature construction
- Avoiding features that would not be available at prediction time

**Scope for Day 1:** Understand the purpose and examples; study advanced text vectorization and dimensionality reduction on later days.

### G. Data Splitting and Validation

- Training, validation, and test sets
- Common split ratios and why they are not universal
- Random train/test split
- Stratified splitting for classification
- Time-based splitting for time-series problems
- Group-based splitting when records share users, patients, devices, etc.
- Cross-validation (introductory)
- Choosing a metric that matches the task

**Important points:**
- A random split is not suitable for every problem.
- Keep related records from leaking across splits when the task requires group-based validation.
- Do not repeatedly tune decisions against the final test set.

### H. Data Leakage — Highest Priority

- What data leakage means
- Leakage from preprocessing before splitting
- Leakage from target-derived features
- Leakage from future information
- Leakage across duplicate or related records
- Leakage during target encoding
- How scikit-learn pipelines help prevent leakage

**Core rule:**

1. Split the data.
2. Fit imputers, scalers, encoders, and other learned transformations on training data only.
3. Use those fitted transformations to process validation and test data.
4. Evaluate without allowing test information to influence model selection.

### I. `fit()`, `transform()`, and `fit_transform()`

- `fit()`: learn parameters or mappings from data
- `transform()`: apply learned parameters to data
- `fit_transform()`: fit and transform, commonly used on training data
- Why test data should not be independently fitted
- How `Pipeline` and `ColumnTransformer` organize preprocessing

### J. Reproducibility and Practical Workflow

- Setting `random_state` where appropriate
- Keeping preprocessing consistent between training and inference
- Avoiding manual transformations that cannot be reproduced
- Comparing a baseline with a preprocessed model
- Recording assumptions and decisions
- Understanding that preprocessing is task- and model-dependent

---

## 3. Topics Beginners Often Ignore — Do Not Skip These

These deserve special attention because they can quietly damage model performance or make evaluation misleading.

1. **Data leakage:** Can make validation scores look much better than real-world performance.
2. **Correct validation strategy:** Time, groups, and class imbalance can make random splitting misleading.
3. **Missingness indicators:** The fact that a value is missing may itself contain useful information.
4. **Outliers are not always errors:** Rare observations may be important, especially in fraud or anomaly detection.
5. **Feature scaling depends on the model:** It is important for distance-based methods but often unnecessary for tree models.
6. **Encoding can introduce false order:** Integer labels do not automatically represent meaningful numerical relationships.
7. **High-cardinality features:** One-hot encoding can produce a huge feature space.
8. **Unseen categories at inference time:** The pipeline should handle categories not observed during training.
9. **Duplicate and related records:** They can cause overly optimistic validation results.
10. **Target leakage through features:** A feature may indirectly reveal the answer or use information from the future.
11. **Metric selection:** Accuracy, MAE, RMSE, precision, recall, and other metrics answer different questions.
12. **Preprocessing is not always beneficial:** Add a step because it addresses a real issue, not just because it is common.

---

## 4. Suggested Study Order

Use this sequence to build understanding without jumping between unrelated topics.

- [ ] 1. Dataset inspection and basic EDA
- [ ] 2. Data types, duplicates, invalid values, and target distribution
- [ ] 3. Missing values and imputation methods
- [ ] 4. Outlier detection and handling
- [ ] 5. Categorical encoding
- [ ] 6. Scaling and numerical transformations
- [ ] 7. Feature extraction vs. feature selection
- [ ] 8. Train/validation/test splitting
- [ ] 9. Data leakage and correct preprocessing order
- [ ] 10. `fit()`, `transform()`, `fit_transform()`, `Pipeline`, and `ColumnTransformer`
- [ ] 11. Implement a complete workflow
- [ ] 12. Test understanding with questions and review mistakes

---

## 5. Practical Implementation Checklist

Use a small tabular dataset with numerical and categorical columns, plus some missing values.

- [ ] Inspect its shape, columns, data types, and summary statistics.
- [ ] Identify missing values and duplicate rows.
- [ ] Inspect numerical distributions and possible outliers.
- [ ] Identify categorical columns and their cardinality.
- [ ] Separate features (`X`) from the target (`y`).
- [ ] Split the data before fitting learned preprocessing steps.
- [ ] Build a numerical pipeline with imputation and, if needed, scaling.
- [ ] Build a categorical pipeline with imputation and encoding.
- [ ] Combine them with `ColumnTransformer`.
- [ ] Combine preprocessing and a baseline model with `Pipeline`.
- [ ] Evaluate using a metric suitable for the task.
- [ ] Verify that preprocessing is fitted only on training data.
- [ ] Record the baseline score and any changes made.

### Suggested Python libraries

- `pandas` — inspect and manipulate tabular data
- `numpy` — numerical operations
- `matplotlib` / `seaborn` — visualize distributions and outliers
- `scikit-learn` — splitting, imputers, encoders, scalers, pipelines, and metrics

---

## 6. Questions I Should Be Able to Answer

- [ ] What is data preprocessing, and why is it necessary?
- [ ] What is the difference between a feature and a target?
- [ ] When might median imputation be preferable to mean imputation?
- [ ] Why should missing values not always be replaced with zero?
- [ ] How can I detect outliers, and why should I investigate them before removing them?
- [ ] What is the difference between standardization and min-max scaling?
- [ ] Which models are sensitive to feature scaling?
- [ ] What is the difference between nominal and ordinal categorical data?
- [ ] Why can label encoding be inappropriate for nominal categories?
- [ ] What is the difference between feature extraction and feature selection?
- [ ] Why must preprocessing be fitted on training data only?
- [ ] What is data leakage? Give at least two examples.
- [ ] When should I use stratified, group-based, or chronological splitting?
- [ ] What do `fit()`, `transform()`, and `fit_transform()` do?
- [ ] Why are `Pipeline` and `ColumnTransformer` useful?
- [ ] How do I know whether a preprocessing step actually improves the model?

---

## 7. Day 1 Completion Criteria

Day 1 is complete when I can:

- [ ] Explain the main preprocessing concepts in my own words.
- [ ] Identify which preprocessing methods suit a given data problem.
- [ ] Build a working scikit-learn preprocessing pipeline.
- [ ] Explain how the workflow prevents data leakage.
- [ ] Evaluate a simple baseline model.
- [ ] Summarize three mistakes I will avoid in future ML projects.

---

## 8. Notes and Reflection

**Concepts I understood well:**

_Write notes here._

**Concepts I need to revisit:**

_Write notes here._

**Mistakes or surprises:**

_Write notes here._

**One thing I learned today:**

_Write notes here._

**Day 1 status:** Not started / In progress / Completed

---

## Final Reminder

The goal is not to memorize every preprocessing technique. The goal is to understand **what problem each technique solves, when to use it, when not to use it, and how to apply it without leakage**.

For Day 1, prioritize EDA, missing values, encoding, scaling, validation, and especially data leakage. Advanced feature engineering, text vectorization, and dimensionality reduction can be studied in more depth on later days.
"""

out = Path("/mnt/data/day_1_ml_data_preprocessing.md")
out.write_text(content, encoding="utf-8")
print(f"Created: {out}")
