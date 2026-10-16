# Hospital Readmission Prediction

Binary classification of whether a diabetic patient is readmitted to hospital, using demographic, clinical and medication features. The project compares four classifiers and reports which features drive their predictions, with an explicit comparison to a naive baseline.

**Dataset:** [Hospital Readmissions on Kaggle](https://www.kaggle.com/datasets/dubradave/hospital-readmissions), 25,000 patient records, 17 columns.

## Key results

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Logistic Regression | 0.610 | 0.630 | 0.411 | 0.497 |
| Decision Tree (max depth 3) | 0.610 | 0.600 | 0.509 | 0.551 |
| Random Forest | 0.607 | 0.595 | 0.516 | 0.553 |
| XGBoost | 0.611 | 0.622 | 0.438 | 0.514 |

**Baseline:** predicting "not readmitted" for everyone scores **0.530** accuracy, because the classes are roughly 53% / 47%. All four models beat that baseline by about 8 points, which is a real but modest signal.

**Reading the table:** the four models are within about half a percentage point of each other on accuracy, so no model is clearly better. Random Forest has the best recall and F1, which may matter more than accuracy if missing a likely readmission is costly. XGBoost has the highest accuracy only by a margin well inside run-to-run noise.

### Most influential features (XGBoost gain importance)

| Feature | Importance |
|---|---|
| `n_lab_procedures` | 18.3% |
| `n_medications` | 14.3% |
| `time_in_hospital` | 9.5% |
| `age` | 5.3% |
| `n_procedures` | 5.2% |
| `n_inpatient` | 5.0% |

Diagnosis-category features each contribute a smaller share. Importance from a tree model shows what the model uses, not what causes readmission.

## Data

| Column | Description |
|---|---|
| `age` | Age bracket |
| `time_in_hospital` | Length of stay, 1 to 14 days |
| `n_lab_procedures`, `n_procedures`, `n_medications` | Counts during the stay |
| `n_outpatient`, `n_inpatient`, `n_emergency` | Visits in the year before admission |
| `medical_specialty` | Specialty of the admitting physician |
| `diag_1`, `diag_2`, `diag_3` | Diagnosis categories (circulatory, respiratory, diabetes, etc.) |
| `glucose_test`, `A1Ctest` | High, normal, or not performed |
| `change`, `diabetes_med` | Whether diabetes medication changed / was prescribed |
| `readmitted` | **Target:** `yes` or `no` |

Data quality notes from the EDA:

- No missing values in the numeric columns. A small number of rows have a missing `diag_1`; these keep their `diag_2` and `diag_3` values.
- The visit-count columns (`n_outpatient`, `n_inpatient`, `n_emergency`) are heavily right-skewed with long tails. Extreme records were inspected and kept, since no errors were found.
- Pairwise correlations between the features are weak, so all features were retained.

## Method

1. EDA, including distribution plots, outlier inspection and correlation checks.
2. Feature encoding (one-hot for categoricals) and min-max scaling.
3. Training of Logistic Regression, Decision Tree, Random Forest and XGBoost on a train/test split.
4. Comparison on accuracy, precision, recall and F1, with a majority-class baseline.
5. Feature-importance analysis for the tree-based models.

The full analysis is in `Hospital Readmission.ipynb`.

## Limitations

- The signal is modest. Accuracy is about 61% against a 53% baseline, so these models should not be used to make individual clinical decisions.
- This is a single dataset with a single train/test split. Results have not been checked across multiple splits or on external data.
- The dataset is an extract and does not include the full clinical history, so the models cannot account for many factors that drive real readmissions.

## Repository contents

| File | Purpose |
|---|---|
| `Hospital Readmission.ipynb` | Full analysis: EDA, feature engineering, model training and evaluation |
| `README.md` | This document |

## Reproduce

Download the dataset from Kaggle, place the CSV in the project folder, then open the notebook. Requires `pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib` and `seaborn`.
