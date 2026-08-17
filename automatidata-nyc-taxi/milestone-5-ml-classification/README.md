# Automatidata - NYC Taxi - Milestone 5: ML Classification (Random Forest & XGBoost)

Part of the Automatidata NYC TLC Project | Google Advanced Data Analytics Certificate - Course 5: The Nuts and Bolts of Machine Learning

## Business Problem

Taxi drivers depend on tips for income, but predicting which passengers will not tip creates serious risks: drivers might refuse rides to certain passengers, leading to service discrimination and unfair treatment based on pickup location or passenger profile.

**Revised objective:** Instead of predicting non-tippers, predict generous tippers (tip >= 20% of fare). This framing gives drivers positive opportunity signals without creating incentives to discriminate against passengers.

## Model Results

| Model | Precision | Recall | F1 | Accuracy |
|---|---|---|---|---|
| Random Forest (CV) | 0.659 | 0.855 | 0.744 | 0.690 |
| Random Forest (test) | 0.628 | 0.868 | 0.729 | 0.660 |
| XGBoost (CV) | 0.692 | 0.800 | 0.742 | 0.708 |
| **XGBoost (test)** | **0.686** | **0.807** | **0.741** | **0.704** |

**Champion model: XGBoost** - chosen for higher precision and accuracy on test data. Higher precision means fewer false positives (fewer cases where the model incorrectly predicts a generous tip), which is the more important error to minimize in this use case.

## Ethical Considerations (Plan Stage)

The original task asked for a model to predict passengers who would NOT tip, to alert drivers in advance. This raised serious ethical concerns:

- Drivers could refuse or deprioritize rides to predicted non-tippers, creating service discrimination
- Passengers in certain pickup zones could face longer wait times or ride refusals based on model predictions
- The model would be making predictions about individuals' behavior before they've done anything

**Decision:** Shifted the objective to predicting generous tippers instead - a positive signal rather than a negative flag. This still helps drivers anticipate higher earnings without creating conditions for discriminatory service.

## Feature Engineering

**Target variable:**
- `tip_percent` = tip_amount / (total_amount - tip_amount), rounded to 3 decimal places
- `generous` = 1 if tip_percent >= 0.20, else 0
- Class balance: 52.6% generous, 47.4% not generous (nearly balanced - no resampling needed)

**Data filtering:**
- Credit card payments only (15,265 rows) - cash tips recorded as $0.00, making them unusable for tip modeling

**Pre-trip features only (no post-trip leakage):**
- `mean_duration` - estimated trip duration from Milestone 4 regression outputs
- `mean_distance` - estimated trip distance from Milestone 4 regression outputs
- `predicted_fare` - estimated fare from Milestone 4 regression outputs
- `day` - day of week (one-hot encoded)
- `month` - abbreviated month name (one-hot encoded)
- `am_rush` - binary: pickup between 06:00-10:00
- `daytime` - binary: pickup between 10:00-16:00
- `pm_rush` - binary: pickup between 16:00-20:00
- `nighttime` - binary: pickup between 20:00-06:00
- `PULocationID`, `DOLocationID` - pickup/dropoff location (one-hot encoded)
- `RatecodeID`, `VendorID` - encoded as categorical
- `passenger_count`

**Columns dropped (post-trip or leakage risk):** fare_amount, tip_amount, total_amount, trip_distance, tip_percent, tolls_amount, actual datetime columns, payment_type

## Modeling Pipeline

1. Filter to credit card payments only
2. Engineer tip_percent and generous target variable
3. Engineer time-of-day binary features (4 bins) using custom functions
4. Extract day of week and month from datetime
5. Convert RatecodeID, VendorID, PULocationID, DOLocationID to string, then one-hot encode with pd.get_dummies (drop_first=True) - 347 total features
6. Train/test split: 80/20, stratified, random_state=42
7. GridSearchCV with 5-fold CV for both Random Forest and XGBoost
8. Evaluate F1 as primary metric, with precision, recall, and accuracy tracked

## Hyperparameters (Best)

**Random Forest:**
- max_depth=10, max_features=3, max_samples=0.7
- min_samples_leaf=1, min_samples_split=4, n_estimators=300

**XGBoost:**
- learning_rate=0.01, max_depth=10
- min_child_weight=6, n_estimators=500

## Key Insights

- **False positives dominate both models** - predicting a generous tip when the passenger doesn't give one. XGBoost reduces these errors more than Random Forest.
- **XGBoost outperforms Random Forest** on precision and accuracy - the better choice when minimizing false positive predictions matters
- The model is a starting tool, not a production-ready system. Threshold tuning (raising above 0.5) would improve precision further at the cost of some recall
- Future improvement: collect real-time traffic, weather, and passenger history features

## Deliverables

- Activity_Course_6_Automatidata_project_lab.ipynb - RF and XGBoost modeling notebook
- Automatidata-Executive-Summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, Scikit-learn (RandomForestClassifier, GridSearchCV, confusion_matrix, classification_report), XGBoost (XGBClassifier), Matplotlib, Pickle
