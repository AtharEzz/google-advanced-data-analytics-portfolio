# Automatidata - NYC Taxi Fare Prediction - Milestone 4: Regression Modeling

Part of the Automatidata NYC TLC Project | Google Advanced Data Analytics Certificate - Course 4: Regression Analysis

## Business Problem

The New York City TLC needed a model to predict taxi fare amounts before a ride begins. Accurate upfront fare estimates improve transparency for passengers and help drivers anticipate earnings for longer routes.

## Model Results

| Metric | Training Set | Test Set |
|---|---|---|
| R-squared | 0.84 | **0.87** |
| MAE | $2.19 | **$2.13** |
| MSE | 17.89 | 14.33 |
| RMSE | $4.23 | **$3.79** |

The model explains **86.8% of the variance** in taxi fares with a mean absolute error of $2.13 - suitable for upfront fare estimation in a passenger app.

## Feature Engineering

Three features were engineered from scratch before modeling, since raw columns would not be available at prediction time (before the ride starts):

**mean_distance:** For each unique pickup/dropoff location pair, calculated the mean trip distance across all historical trips with that same route, then mapped back to each row.

**mean_duration:** Same approach as mean_distance but for trip duration.

**rush_hour:** Binary feature (1/0) - weekday trips during 06:00-10:00 or 16:00-20:00. Weekends always return 0.

## Modeling Pipeline

1. Data cleaning - negative fares imputed to 0, outliers capped using Q3 + 6*IQR for fare_amount and duration
2. Feature selection - dropped columns not available at prediction time (actual duration, raw datetime, payment type, tip, tolls)
3. Train/test split - 80/20, random_state=0
4. StandardScaler fitted on training data only, applied to test data (no leakage)
5. LinearRegression trained on scaled features
6. Residual diagnostics - mean residual: -0.015 (near zero, no systematic bias)

## Feature Coefficients

| Feature | Coefficient | Interpretation |
|---|---|---|
| mean_distance | 7.14 | Strongest predictor - every ~3.57 miles adds ~$7.13 |
| mean_duration | 2.81 | Secondary - time adds to fare but less than distance |
| rush_hour | 0.12 | Very small effect |
| passenger_count | 0.03 | Negligible |
| VendorID_2 | -0.05 | Negligible |

## Key Insight

Trip distance is by far the biggest driver of taxi fares. Time of day and passenger count have minimal impact on the base fare amount. The model can predict fares before a ride starts using estimated route distance and duration inferred from historical data on the same pickup/dropoff pair.

## Business Recommendations

- Integrate into a passenger app as an upfront fare calculator - R² of 0.87 is reliable for estimation
- Share distance-based earnings data with drivers to help evaluate longer trips before accepting
- Combine with Milestone 3 finding: encourage card payments since card users pay higher fares on average

## Deliverables

- Course_4_Automatidata_Executive_Summary.ipynb - Regression modeling notebook
- Course_4_Automatidata_Executive_Summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, Scikit-learn (LinearRegression, StandardScaler, train_test_split), Matplotlib, Seaborn
