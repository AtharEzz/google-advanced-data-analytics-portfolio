# Salifort Motors Employee Retention - Capstone Project

Google Advanced Data Analytics Professional Certificate - Capstone Project (Course 7)

## Business Problem

Salifort Motors seeks to improve employee retention by identifying what makes employees likely to leave. Finding, interviewing, and training new employees is time-consuming and expensive — predicting at-risk employees early enables targeted intervention before they resign.

**Key question:** What factors are most likely to make an employee leave the company?

## Dataset

- **Source:** HR Analytics and Job Prediction dataset (Kaggle)
- **Size:** 15,000 rows, 10 features (after deduplication: 11,991 rows)
- **Target:** `left` (binary: 0 = stayed, 1 = left)
- **Class balance:** 83.4% stayed, 16.6% left

| Feature | Description |
|---|---|
| satisfaction_level | Employee-reported job satisfaction [0-1] |
| last_evaluation | Score of last performance review [0-1] |
| number_project | Number of projects contributed to |
| average_monthly_hours | Average monthly hours worked |
| tenure | Years with the company |
| work_accident | Whether employee had a workplace accident |
| promotion_last_5years | Whether promoted in the last 5 years |
| department | Employee's department |
| salary | Salary level (low/medium/high) |

## Model Results

### Validation Set Comparison

| Model | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|
| Logistic Regression (baseline) | 0.511 | 0.183 | 0.270 | 0.828 |
| Decision Tree | 0.925 | 0.930 | 0.927 | 0.972 |
| **Random Forest** | **0.979** | **0.917** | **0.947** | **0.988** |
| XGBoost | 0.981 | 0.930 | 0.955 | 0.993 |

### Holdout Test Set (Champion - Random Forest)

| Metric | Score |
|---|---|
| Precision | 0.989 |
| Recall | 0.922 |
| F1-Score | **0.955** |
| ROC-AUC | **0.979** |

**Champion model: Random Forest** - selected after validation set comparison. Evaluated once on the holdout test set to confirm true generalization.

## Key Findings

- **Dissatisfaction drives turnover:** Satisfaction level has the strongest negative correlation with churn (r = -0.35)
- **Bimodal overwork pattern:** Employees leave from two extremes - severe burnout (250+ hours/month, 6-7 projects) AND underutilization (fewer than 150 hours, 2 projects)
- **Tenure cliff at years 3-5:** Churn peaks at 45.4% attrition at year 5, then drops to near zero for 7+ year employees
- **Salary and promotion protect retention:** Turnover drops sharply with salary (Low: 20.5%, Medium: 14.6%, High: 4.8%); promotions reduce churn risk to ~4%
- **Department does not matter:** Overwork happens across all departments - systemic, not departmental

## Top Predictive Features (Random Forest)

1. last_evaluation
2. number_project
3. tenure
4. average_monthly_hours
5. salary
6. work_accident

## Why Logistic Regression Failed

Churn at Salifort Motors is not linear. Employees with extreme overwork AND employees with extreme underutilization both churn - logistic regression cannot draw a meaningful boundary between these opposing groups. Tree-based models easily separate them. (Logistic Regression recall: 0.183 vs Random Forest recall: 0.922)

## Ethical Considerations

- **Potential leakage features:** satisfaction_level and last_evaluation may reflect post-resignation sentiment rather than pre-resignation signals. The model should be retested without these features for real-world deployment
- **Supportive use only:** Model predictions must be used to help overworked staff, never to penalize or target employees
- **Employee anonymity:** Individual predictions should not be used to identify specific employees for punitive action

## Business Recommendations

1. **Cap monthly hours:** Limit to 200 hours/month and assign 3-5 projects per employee - eliminate extreme overwork cases
2. **Target 3-5 year staff:** Offer promotions and pay raises when employees reach their 3rd year to prevent the tenure-cliff churn peak
3. **Retrain without leakage data:** Test model performance without satisfaction_level and last_evaluation to ensure real-world validity
4. **Supportive interventions only:** Use model predictions to proactively help at-risk employees, not to penalize them

## Modeling Pipeline

1. Data cleaning: dropped 3,008 duplicate rows; standardized column names to snake_case
2. Outlier analysis: 824 long-tenure outliers retained (legitimate, not errors)
3. Feature engineering: created binary `overworked` feature (1 = average_monthly_hours > 175)
4. Strict 60/20/20 Train/Validation/Test split (stratified, random_state=42)
5. GridSearchCV with 5-fold CV for all candidate models (scoring: accuracy, precision, recall, F1, ROC-AUC; refit on ROC-AUC)
6. Champion selected on validation set; evaluated once on holdout test set

## Deliverables

- Activity__Course_7_Salifort_Motors_project_lab.ipynb - Full analysis and modeling notebook
- Capstone__executive_summary.pdf - One-page stakeholder executive summary

## Tools

Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn (LogisticRegression, DecisionTreeClassifier, RandomForestClassifier, GridSearchCV), XGBoost, Pickle
