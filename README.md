# Google Advanced Data Analytics Portfolio

Guided case study projects completed as part of the **Google Advanced Data Analytics Professional Certificate** (in progress), following the PACE framework (Plan, Analyze, Construct, Execute) used in professional data analytics work.

Three parallel business scenarios run across the full certificate, with each course adding a new layer of analytical depth to the same ongoing project:

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
- 700 missing values in the label column; device distribution consistent across missing vs. non-missing rows - likely missing at random
- Churned users drove ~240% more km per driving day than retained users - a strong behavioral signal
- Device type (iPhone vs. Android) shows no correlation with churn

**EDA:**
- Users who drove all 30 days had a **0% churn rate** vs. **40% churn rate** for inactive users - app engagement frequency is the strongest churn signal
- Positive correlation between daily driving distance and churn - longer-distance drivers paradoxically more likely to churn
- User representation stable across all tenure lengths up to ~10 years
- Outliers identified in driven_km_drives, activity_days, and driving_days

**Hypothesis Testing:**
- Research question: Does device type (iPhone vs. Android) significantly affect monthly drive count?
- Method: Two-sample Welch's t-test (a = 0.05)
- iPhone: mean 67.86 drives/month vs. Android: mean 66.23 drives/month
- t-statistic: 1.46, p-value: 0.1434 - fail to reject null hypothesis
- Device type is not a significant predictor - focus modeling on behavioral features instead

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
| Regression Modeling | Predictive modeling | Upcoming |
| ML Classification | Final classification model | Upcoming |

### Key Findings

**Data Inspection:**
- Nearly balanced dataset: 50.3% claims, 49.7% opinions
- Claims average ~100x more views than opinions: 501,029 vs. 4,956 mean views
- Claims maintain ~33% like-per-view ratio vs. ~22% for opinions
- Banned/Under Review authors overwhelmingly associated with claim videos

**EDA:**
- Engagement metrics heavily right-skewed - tiny fraction of viral claim videos dominates platform traffic
- Clear behavioral boundaries separate claims and opinions across all metrics
- Visualizations produced in Python and Tableau (Tableau Story)

**Hypothesis Testing:**
- Research question: Does creator verification status significantly impact view count?
- Method: Two-sample Welch's t-test (a = 0.05)
- Unverified: mean 265,664 views vs. verified: mean 91,439 views
- t-statistic: -25.50, p-value: 2.61 x 10^-120 - null hypothesis rejected
- Counterintuitive finding: unverified accounts average 3x more views - explained by higher volume of claim content
- verified_status confirmed as a key feature for the classification model

---

## Project 3: Automatidata - NYC Taxi Fare Prediction

**Business problem:** The New York City Taxi and Limousine Commission (NYC TLC) needs a model to predict taxi fare amounts, enabling better fare transparency and trip planning for passengers.

**Dataset:** 408,294 taxi trips (22,699 sampled for analysis), 18 variables covering pickup/dropoff times, locations, distances, passenger counts, payment types, and fare components

### Progress

| Phase | Focus | Status |
|---|---|---|
| Data Inspection & Profiling | Structural audit, variable investigation, anomaly detection | Complete |
| Exploratory Data Analysis | EDA and Tableau visualization | Upcoming |
| Hypothesis Testing | Statistical testing | Upcoming |
| Regression Modeling | Fare prediction model | Upcoming |
| ML Classification | Advanced modeling | Upcoming |

### Key Findings

**Data Inspection:**
- Datetime columns stored as strings - conversion to proper datetime format required before analysis
- Negative fare and total amount values present (minimum: -120.30) - represent data errors requiring cleaning
- Extreme fare outlier identified: a 2.60-mile trip costing $1,200.29 - anomalous fare and tip combination
- Longest trips are not necessarily the most expensive - trip distance alone is insufficient for fare prediction
- Credit card tips average $2.73 vs. $0.00 for cash - cash tips not recorded in the system, creating a measurement gap
- Both vendors (Creative Mobile Technologies, VeriFone) have nearly identical mean total amounts (~$16.30)
- Trip distance and total_amount identified as the two strongest variables for predictive modeling

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
|
|- automatidata-nyc-taxi/
|   |- milestone-1-data-inspection/
|       |- Activity_Course_2_Automatidata_project_lab.ipynb
|       |- Course_1_Automatidata_executive_summary.pdf
|       |- Automatidata_project_proposal.docx
```

---

## Tools & Skills

Python (Pandas, NumPy, Matplotlib, Seaborn, SciPy), Tableau, statistical analysis, hypothesis testing, EDA, data cleaning, data visualization, stakeholder communication

**Certificate:** Google Advanced Data Analytics Professional Certificate (Coursera) - in progress
