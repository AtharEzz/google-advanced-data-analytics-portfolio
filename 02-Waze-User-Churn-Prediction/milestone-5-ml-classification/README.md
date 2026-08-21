# Waze User Churn Project - Milestone 5: ML Classification (Random Forest & XGBoost)

Part of the Waze User Churn Prediction Project | Google Advanced Data Analytics Certificate - Course 5: The Nuts and Bolts of Machine Learning

## Business Problem

Waze is losing active app users (churn), reducing engagement and revenue. The business lacked a system to identify which users were likely to leave before they stopped using the app. The dataset has severe class imbalance (far fewer churned users than retained), making it difficult to detect churn without generating too many false positives.

## Model Results

| Model | Set | Precision | Recall | F1 | Accuracy |
|---|---|---|---|---|---|
| RF | CV | 0.467 | 0.125 | 0.196 | 0.819 |
| XGB | CV | 0.421 | 0.171 | 0.243 | 0.811 |
| RF | Validation | 0.445 | 0.120 | 0.189 | 0.817 |
| XGB | Validation | 0.412 | 0.183 | 0.254 | 0.809 |
| **XGB (champion)** | **Test** | **0.412** | **0.185** | **0.256** | **0.809** |
| XGB threshold=0.40 | Test | 0.385 | 0.260 | 0.311 | 0.795 |
| XGB threshold=0.171 | Test | 0.306 | 0.501 | 0.380 | 0.710 |

**Champion model: XGBoost** - selected over Random Forest for higher recall on validation data (0.183 vs 0.120). XGBoost recall of 18.5% nearly doubled the logistic regression baseline from Milestone 4 (~9%).

## Feature Engineering

Six new features engineered before modeling - three of which ranked in the top 5 by XGBoost feature importance:

| Feature | Description |
|---|---|
| km_per_driving_day | Mean km driven per driving day (infinite values converted to 0) |
| percent_sessions_in_last_month | sessions / total_sessions |
| professional_driver | Binary: 1 if drives >= 60 AND driving_days >= 15 |
| total_sessions_per_day | total_sessions / n_days_after_onboarding |
| km_per_hour | driven_km_drives / (duration_minutes_drives / 60) |
| km_per_drive | driven_km_drives / drives (infinite values converted to 0) |
| percent_of_drives_to_favorite | (total_navigations_fav1 + fav2) / total_sessions |

## Top Features by XGBoost Importance

1. km_per_hour (F-score: 1163) - engineered
2. percent_sessions_in_last_month (1045) - engineered
3. n_days_after_onboarding (1042) - raw
4. total_navigations_fav1 (992) - raw
5. total_sessions_per_day (929) - engineered

6 of the top 10 features are engineered, confirming that feature engineering significantly improved model performance over using raw variables alone.

## Modeling Pipeline

1. Dropped 700 rows with missing label values (confirmed missing at random)
2. No outlier capping - tree-based models are resilient to outliers
3. Encoded device as binary (Android=0, iPhone=1)
4. Encoded label as binary (retained=0, churned=1)
5. Stratified train/validation/test split (60/20/20, random_state=42)
6. GridSearchCV with 5-fold CV, scoring=['precision','recall','f1','accuracy'], optimizing for recall
7. Final evaluation on held-out test set using champion XGBoost only

## Best Hyperparameters

**Random Forest:**
- max_depth=None, max_features=1.0, max_samples=1.0
- min_samples_leaf=2, min_samples_split=2, n_estimators=300

**XGBoost (champion):**
- learning_rate=0.1, max_depth=6
- min_child_weight=3, n_estimators=500

## Threshold Analysis

Default threshold (0.5) misses most churned users. Two alternative thresholds explored:

- **Threshold=0.40:** Recall 26.0%, Precision 38.5% - moderate improvement with acceptable precision loss
- **Threshold=0.171:** Recall 50.1%, Precision 30.6% - catches half of all churners; recommended for low-cost retention campaigns where false positives are acceptable

## Key Insights

- **km_per_hour is the strongest churn predictor** - users who drive longer distances per session are far more likely to stay engaged
- **User tenure and recent activity separate retained from churned users** - n_days_after_onboarding and percent_sessions_in_last_month are top signals
- **professional_driver has very low importance** - despite being a useful signal in logistic regression, the tree-based models found more informative patterns elsewhere
- **Device type is almost irrelevant** - confirming the Milestone 3 hypothesis test finding that device type does not significantly affect driving behavior

## Business Recommendations

- Use the model for low-cost exploratory campaigns (threshold=0.171 for 50% recall) - not major business decisions due to low precision
- Target retention campaigns toward users with declining daily session activity and falling km_per_hour metrics - these are early churn warning signals
- Avoid device-specific retention interventions - no evidence device type drives churn
- Next steps: threshold optimization, SMOTE for class imbalance, and production monitoring on a live user cohort

## Is This Model Production-Ready?

For major business decisions: No. With 18.5% recall at the default threshold, the model misses more than 80% of users who actually churn.

For low-cost exploratory campaigns: Yes. At adjusted thresholds it catches up to 50% of churners while still being twice as effective as the logistic regression baseline.

## Deliverables

- Activity_Course_6_Waze_project_lab.ipynb - RF and XGBoost modeling notebook
- Waze-Course-5-executive-summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, Scikit-learn (RandomForestClassifier, GridSearchCV, ConfusionMatrixDisplay, PrecisionRecallDisplay), XGBoost (XGBClassifier, plot_importance), Matplotlib, Seaborn
