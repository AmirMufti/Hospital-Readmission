Predicting Patient Readmission Using Machine Learning Models

Overview
This project aims to predict patient outcomes using multiple machine learning models. The dataset consists of various medical and demographic features. The project explores Logistic Regression, Decision Tree, Random Forest, and XGBoost classifiers, evaluating their performance and identifying the most influential features affecting the outcomes.

Key Objectives
Build predictive models for patient outcomes.
Identify key features influencing patient outcomes.
Compare and evaluate model performances.

Dataset Description
The dataset contains medical and demographic attributes, including:
age" - age bracket of the patient
"time_in_hospital" - days (from 1 to 14)
"n_procedures" - number of procedures performed during the hospital stay
"n_lab_procedures" - number of laboratory procedures performed during the hospital stay
"n_medications" - number of medications administered during the hospital stay
"n_outpatient" - number of outpatient visits in the year before a hospital stay
"n_inpatient" - number of inpatient visits in the year before the hospital stay
"n_emergency" - number of visits to the emergency room in the year before the hospital stay
"medical_specialty" - the specialty of the admitting physician
"diag_1" - primary diagnosis (Circulatory, Respiratory, Digestive, etc.)
"diag_2" - secondary diagnosis
"diag_3" - additional secondary diagnosis
"glucose_test" - whether the glucose serum came out as high (> 200), normal, or not performed
"A1Ctest" - whether the A1C level of the patient came out as high (> 7%), normal, or not performed
"change" - whether there was a change in the diabetes medication ('yes' or 'no')
"diabetes_med" - whether a diabetes medication was prescribed ('yes' or 'no')
"readmitted" - if the patient was readmitted at the hospital ('yes' or 'no')

Models and Results
1. Logistic Regression
Accuracy: 60.96%
Simple linear model providing a baseline.
2. Decision Tree
Accuracy: 60.98%
A tree-based approach with max depth = 3 for interpretability.
3. Random Forest
Accuracy: 60.72%
An ensemble method providing better generalization.
4. XGBoost
Accuracy: 61.08%
Most accurate model leveraging gradient boosting.

Feature Importance
Key features influencing outcomes, as identified by XGBoost:
n_lab_procedures (18.3% importance)
Most significant feature affecting patient outcomes.
n_medications (14.3%)
Reflects treatment intensity.
time_in_hospital (9.5%)
Duration of stay impacts outcomes.
age (5.3%)
Older patients show distinct trends.
n_procedures (5.2%)
Indicates procedural complexity.
n_inpatient (5.0%)
Inpatient visit frequency.
Other diagnostic categories contribute incrementally to the model's decisions.

Tools and Libraries
Programming Language: Python
Libraries: pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn.

Conclusion
The project demonstrates that XGBoost outperforms other models, achieving the highest accuracy. The analysis highlights critical features like n_lab_procedures and n_medications, offering actionable insights for medical practitioners.
