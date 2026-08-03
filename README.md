# Google Advanced Data Analytics Portfolio

Guided case study projects completed as part of the **Google Advanced Data Analytics Professional Certificate** (in progress), following the PACE framework (Plan, Analyze, Construct, Execute) used in professional data analytics work.

Three parallel business scenarios run across the full certificate:

- **Waze** - Predicting monthly user churn to improve retention
- **TikTok** - Classifying video submissions as claims or opinions to support content moderation
- **Automatidata** - Predicting NYC taxi fare amounts for the NYC TLC

---

## Project 1: Waze User Churn Prediction

**Business problem:** Waze needs to identify users likely to uninstall or stop using the app, enabling proactive retention campaigns before users churn.

**Dataset:** 14,999 users, 13 variables covering driving behavior, session activity, device type, and churn label

### Progress

| Phase | Focus | Status |
|---|---|---|
| Data Inspection & Profiling | Structural audit, missing value analysis, churn baseline | Complete |
| Exploratory Data Analysis | Distribution analysis, outlier detection, behavioral visualization | Complete |
| Hypothesis Testing | Two-sample t-test on device type vs. drive count | Complete |
| Regression Modeling | Predictive modeling | Upcoming |
| ML Classification | Final classification model | Upcoming |

### Key Findings

**Data Inspection:**
- 17.74% of users churned; 82.26% retained
- 700 missing values in label column - likely missing at random
- Churned users drove ~240% more km per driving day - a strong behavioral signal
- Device type shows no correlation with churn

**EDA:**
- Users who drove all 30 days had a **0% churn rate** vs. **40% for inactive users**
- Positive correlation between daily driving distance and churn
- User representation stable across all tenure lengths up to ~10 years
- Outliers identified in driven_km_drives, activity_days, and driving_days

**Hypothesis Testing:**
- Research question: Does device type significantly affect monthly drive count?
- Method: Two-sample Welch's t-test (a = 0.05)
- iPhone: mean 67.86 drives/month vs. Android: mean 66.23 drives/month
- t-statistic: 1.46, p-value: 0.1434 - fail to reject null hypothesis
- Device type is not a significant predictor - focus on behavioral features instead

---

## Project 2: TikTok Claims Classification

**Business problem:** TikTok needs to automate classification of user-submitted content as claims or opinions to prioritize content moderation resources at scale.

**Dataset:** ~19,000 videos with engagement metrics, author verification and ban status, and claim/opinion label

### Progress

| Phase | Focus | Status |
|---|---|---|
| Data Inspection & Profiling | Class balance, engagement baseline, variable relationships | Complete |
| Exploratory Data Analysis | Distribution analysis, Tableau Story visualization | Complete |
| Hypothesis Testing | Two-sample t-test on verification status vs. view count | Complete |
| Regression Modeling (Logistic) | Logistic regression to predict verified status | Complete |
| ML Classification | Final claims/opinions classifier | Upcoming |

### Key Findings

**Data Inspection:**
- Nearly balanced dataset: 50.3% claims, 49.7% opinions
- Claims average ~100x more views than opinions: 501,029 vs. 4,956 mean views
- Claims maintain ~33% like-per-view ratio vs. ~22% for opinions
- Banned/Under Review authors overwhelmingly associated with claim videos

**EDA:**
- Engagement metrics heavily right-skewed - tiny fraction of viral claim videos dominates traffic
- Clear behavioral boundaries separate claims and opinions across all metrics
- Visualizations produced in Python and Tableau (Tableau Story)

**Hypothesis Testing:**
- Research question: Does creator verification status significantly impact view count?
- Method: Two-sample Welch's t-test (a = 0.05)
- Unverified: mean 265,664 views vs. verified: mean 91,439 views
- t-statistic: -25.50, p-value: 2.61 x 10^-120 - null hypothesis rejected
- Unverified accounts average 3x more views - explained by higher volume of claim content
- verified_status confirmed as a key feature for the classification model

**Regression Analysis (Logistic Regression):**
- Target: predict whether a video creator is verified or not verified
- Class imbalance handled via upsampling (93.7% not verified → 50/50 balanced training set)
- Multicollinearity identified among engagement metrics - kept only video_like_count as representative
- Logistic regression on 5 features: video_duration_sec, video_like_count, text_length, claim_status, author_ban_status
- Overall accuracy: 63% on 7,154 test records
- Not verified: Precision 59%, Recall 87%, F1 0.70 - model catches most unverified accounts
- Verified: Precision 74%, Recall 38%, F1 0.51 - model misses many verified accounts
- Model is biased toward "not verified" - threshold tuning and non-linear models recommended as next steps

---

## Project 3: Automatidata - NYC Taxi Fare Prediction

**Business problem:** The NYC Taxi and Limousine Commission needs a model to predict taxi fare amounts before a ride begins, enabling fare transparency and upfront pricing for passengers.

**Dataset:** 408,294 taxi trips (22,699 sampled), 18 variables covering pickup/dropoff times, locations, distances, passenger counts, payment types, and fare components

### Progress

| Phase | Focus | Status |
|---|---|---|
| Data Inspection & Profiling | Structural audit, variable investigation, anomaly detection | Complete |
| Exploratory Data Analysis | EDA, Python visualizations, Tableau scatter plot | Complete |
| Hypothesis Testing (A/B Test) | Payment type vs. fare amount | Complete |
| Regression Modeling | Multiple linear regression for fare prediction | Complete |
| ML Classification | Advanced modeling | Upcoming |

### Key Findings

**Data Inspection:**
- Datetime columns stored as strings - conversion required before analysis
- Negative fare values present (minimum: -120.30) - data errors requiring cleaning
- Extreme outlier: 2.60-mile trip costing $1,200.29
- Longest trips are not necessarily the most expensive
- Credit card tips average $2.73 vs. $0.00 for cash - cash tips not captured in system

**EDA:**
- 75% of all NYC taxi trips are under 3.06 miles and cost $17.80 or less
- Busiest months: March and October; slowest: July and August
- Highest revenue days: Thursday ($57,182) and Friday ($55,819); lowest: Sunday ($48,624)
- Tableau scatter plot built showing trip_distance vs total_amount relationship

**Hypothesis Testing (A/B Test):**
- Research question: Do credit card users pay higher fares than cash users?
- Method: Two-sample Welch's t-test (a = 0.05)
- Credit card: mean $13.43 vs. cash: mean $12.21
- t-statistic: 6.87, p-value: 6.80 x 10^-12 - null hypothesis rejected
- Credit card users pay statistically significantly higher fares ($1.22 more per trip on average)
- Caveat: payment type is not randomly assigned, so causation cannot be fully established

**Regression Modeling:**
- Engineered three features not available at prediction time: mean_distance, mean_duration (per pickup/dropoff pair), and rush_hour binary flag
- Multiple linear regression on 5 features with StandardScaler (fitted on train only)
- Test set R² = **0.87** - model explains 86.8% of fare variance
- Test set MAE = **$2.13**, RMSE = **$3.79**
- mean_distance is by far the strongest predictor (coefficient: 7.14) - distance drives fare price
- Rush hour has very little effect on base fare - NYC taxi meter is primarily distance-based
- Residual mean: -0.015 (near zero - no systematic bias)

---

## PACE Framework

All three projects follow the PACE framework:

- **Plan** - Define the business problem, understand stakeholder needs, assess data structure
- **Analyze** - Inspect, clean, and explore the data
- **Construct** - Build statistical tests, models, or visualizations
- **Execute** - Communicate findings to stakeholders via executive summaries

Each completed phase includes a Jupyter notebook (technical analysis) and an executive summary PDF (stakeholder communication).

---

## Repository Structure

```
google-advanced-data-analytics-portfolio/
|
|- 02-Waze-User-Churn-Prediction/
|   |- milestone-1-planning/
|   |- milestone-2-eda/
|   |- milestone-3-hypothesis-testing/
|
|- tiktok-claims-project/
|   |- milestone-1-planning/
|   |- milestone-2-eda/
|   |- milestone-3-hypothesis-testing/
|   |- milestone-4-regression-modeling/
|
|- automatidata-nyc-taxi/
|   |- milestone-1-data-inspection/
|   |- milestone-2-eda/
|   |- milestone-3-hypothesis-testing/
|   |- milestone-4-regression-modeling/
|       
```

---

## Tools & Skills

Python (Pandas, NumPy, Matplotlib, Seaborn, SciPy, Scikit-learn), Tableau, statistical analysis, hypothesis testing, A/B testing, feature engineering, multiple linear regression, EDA, data visualization, stakeholder communication

**Certificate:** Google Advanced Data Analytics Professional Certificate (Coursera) - in progress
