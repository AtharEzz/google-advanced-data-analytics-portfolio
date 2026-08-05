# Waze User Churn Project - Milestone 4: Regression Modeling (Logistic Regression)

Part of the Waze User Churn Prediction Project | Google Advanced Data Analytics Certificate - Course 4: Regression Analysis

## Business Problem

Build an explanatory model to identify why Waze users churn and which behavioral factors most strongly predict user loss, enabling Waze to design more targeted retention campaigns.

## Model Results

| Metric | Retained | Churned | Overall |
|---|---|---|---|
| Precision | 83% | 52% | |
| Recall | 98% | 9% | |
| F1-Score | 0.90 | 0.16 | |
| Accuracy | | | 82.4% |

**Test set size:** 3,575 records (stratified split)

## Feature Engineering

Two new features engineered before modeling:

**km_per_driving_day:** Mean distance driven per driving day (driven_km_drives / driving_days). Infinity values (from zero driving days) converted to 0.

**professional_driver:** Binary flag (1/0) for users with 60+ drives AND 15+ driving days in the last month. Key finding: professional drivers churn at only **7.6%** vs. **19.9%** for non-professionals - a strong predictive signal.

## Multicollinearity Handling

Correlation heatmap revealed severe multicollinearity among several variable pairs:
- sessions vs. drives: correlation = 0.997 (near-perfect - dropped sessions)
- activity_days vs. driving_days: correlation = 0.95 (dropped driving_days)

VIF calculated for all remaining features - all values under 5, confirming multicollinearity was adequately addressed before modeling.

## Modeling Pipeline

1. Dropped 700 rows with missing label values (confirmed missing at random from earlier EDA)
2. Capped outliers at 95th percentile for 7 variables (sessions, drives, total_sessions, total_navigations_fav1/fav2, driven_km_drives, duration_minutes_drives)
3. Engineered km_per_driving_day and professional_driver features
4. Encoded device as binary (iPhone=1, Android=0)
5. Encoded label as binary (churned=1, retained=0)
6. Removed highly correlated features (sessions, driving_days)
7. Verified VIF for remaining features (all under 5)
8. Verified logit linearity assumption via regplot of activity_days vs. log-odds
9. Stratified train/test split (75/25, random_state=42)
10. LogisticRegression (penalty=None, max_iter=1000)

## Key Findings

**Strongest predictors of churn:**
- activity_days: strongest negative correlation with churn (-0.30) - users who open the app regularly are significantly less likely to churn
- professional_driver: professional drivers churn at 7.6% vs. 19.9% for others

**Unexpectedly weak predictors:**
- driven_km_drives, duration_minutes_drives: near-zero correlation with churn (0.01-0.05) - long-distance drivers churn at the same rate as short-distance drivers
- total_navigations_fav1/fav2: very weak signal despite initial intuition

**Key limitation:**
The model achieves 82.4% accuracy but only 9% recall for churned users - it predicts "retained" for nearly everyone and benefits from the class imbalance (82.3% of users are retained). This model serves as an explanatory baseline rather than a reliable automated prediction system.

## Business Recommendations

- Focus retention campaigns on building regular daily app habits - frequency of engagement is a far stronger retention signal than total distance driven
- Professional drivers (high frequency, high engagement) are already well-retained (7.6% churn) - retention efforts should target occasional users instead
- Next modeling step: train Random Forest or XGBoost with SMOTE to address class imbalance and improve recall for churned users

## Deliverables

- Activity_Course_5_Waze_project_lab.ipynb - Logistic regression notebook
- Waze_Course_4_executive_summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, Scikit-learn (LogisticRegression, train_test_split, confusion_matrix, classification_report), Statsmodels (VIF), Matplotlib, Seaborn
