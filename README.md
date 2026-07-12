# Google Advanced Data Analytics Portfolio

Guided case study projects completed as part of the **Google Advanced Data Analytics Professional Certificate** (in progress), following the PACE framework (Plan, Analyze, Construct, Execute) used in professional data analytics work.

Two parallel business scenarios run across the full certificate, with each course adding a new layer of analytical depth to the same ongoing project:

- **Waze** - Predicting monthly user churn to improve retention
- **TikTok** - Classifying video submissions as claims or opinions to support content moderation

---

## Project 1: Waze User Churn Prediction

**Business problem:** Waze needs to identify users likely to uninstall or stop using the app, enabling proactive retention campaigns before users churn.

**Dataset:** 14,999 users, 13 variables covering driving behavior, session activity, device type, and churn label

### Progress

| Phase | Focus | Status |
|---|---|---|
| Data Inspection & Profiling | Structural audit, missing value analysis, churn baseline | Complete |
| Exploratory Data Analysis | Distribution analysis, outlier detection, behavioral visualization | Complete |
| Statistical Testing | Hypothesis testing | Upcoming |
| Regression Modeling | Predictive modeling | Upcoming |
| ML Classification | Final classification model | Upcoming |

### Key Findings

**Data Inspection:**
- 17.74% of users churned; 82.26% retained
- 700 missing values in the label column; device distribution consistent across missing vs. non-missing rows - likely missing at random, not systematic bias
- Churned users drove ~240% more km per driving day than retained users - a strong behavioral signal
- Device type (iPhone vs. Android) shows no correlation with churn

**EDA:**
- Users who drove all 30 days in the month had a **0% churn rate** vs. **40% churn rate** for inactive users - app engagement frequency is the strongest early churn signal identified
- Positive correlation between daily driving distance and churn - longer-distance drivers are paradoxically more likely to churn, suggesting a distinct high-usage but low-satisfaction profile
- User representation is stable across all tenure lengths up to ~10 years - churn is not concentrated in newer or older users
- Outliers identified in `driven_km_drives`, `activity_days`, and `driving_days` - flagged for handling before modeling

---

## Project 2: TikTok Claims Classification

**Business problem:** TikTok needs to automate the classification of user-submitted content as either "claims" (verifiable factual statements that require moderation review) or "opinions" (subjective expressions), to prioritize content moderation resources efficiently at scale.

**Dataset:** ~19,000 videos with engagement metrics (views, likes, shares, comments), author verification and ban status, and claim/opinion label

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
- Dataset is nearly balanced: 50.3% claims, 49.7% opinions - no class imbalance concern for modeling
- Claims accumulate ~100x more views than opinions: mean views for claims = 501,029 vs. opinions = 4,956
- Claims maintain a ~33% like-per-view ratio vs. ~22% for opinions - higher relative engagement per view
- Authors flagged as "Banned" or "Under Review" are overwhelmingly associated with claim videos (share counts: 17,774-19,018), while active authors are predominantly associated with opinion videos (share counts: 108-124)

**EDA:**
- Engagement metrics are heavily right-skewed: a tiny fraction of highly viral videos drives the vast majority of platform traffic, overwhelmingly from claim content
- Clear behavioral boundaries separate claim and opinion videos across all engagement metrics
- Author moderation status confirmed as a primary candidate feature for the upcoming classification model
- Visualizations produced in both Python (Matplotlib/Seaborn) and Tableau (Tableau Story)

**Hypothesis Testing:**
- Research question: Does creator verification status significantly impact video view count?
- Method: Two-sample Welch's t-test (α = 0.05) - chosen because it does not assume equal variances between groups
- Unverified accounts: mean 265,664 views vs. verified accounts: mean 91,439 views
- t-statistic: -25.50, p-value: 2.61 x 10^-120 - null hypothesis rejected
- Counterintuitive finding: unverified accounts average nearly 3x more views than verified ones - explained by their higher volume of claim videos, which drive massive view spikes
- `verified_status` confirmed as a key feature for the upcoming classification model

---

## PACE Framework

Both projects follow the PACE framework used in professional data analytics:

- **Plan** - Define the business problem, understand stakeholder needs, assess data structure
- **Analyze** - Inspect, clean, and explore the data
- **Construct** - Build statistical tests, models, or visualizations
- **Execute** - Communicate findings to stakeholders via executive summaries

Each completed phase includes a Jupyter notebook (technical analysis) and an executive summary PDF (stakeholder communication), reflecting the dual technical and communication deliverables expected in real analytics roles.

---

## Repository Structure

```
google-advanced-data-analytics-portfolio/
|
|- 02-Waze-User-Churn-Prediction/
|   |- milestone-1-planning/
|   |   |- Activity_Course_2_Waze_project_lab.ipynb
|   |   |- Milestone_1_Executive_Summary.pdf
|   |   |- Waze_project_proposal.pdf
|   |   |- waze_dataset.csv
|   |
|   |- milestone-2-eda/
|       |- Waze_Exploratory_Data_Analysis.ipynb
|       |- Waze_Course_2_executive_summary.pdf
|
|- tiktok-claims-project/
|   |- milestone-1-planning/
|   |   |- Activity_Course_1_TikTok_project_lab.ipynb
|   |   |- TikTok_Course_1_executive_summary.pdf
|   |   |- Data_Dictionary.pdf
|   |
|   |- milestone-2-eda/
|   |   |- EDA_TikTok_project_lab.ipynb
|   |   |- TikTok_Course_2_executive_summary.pdf
|   |   |- Tableau_Story.pdf
|   |
|   |- milestone-3-hypothesis-testing/
|       |- Activity_Course_4_TikTok_project_lab.ipynb
|       |- TikTok_Course_3_executive_summary.pdf
```

---

## Tools & Skills

Python (Pandas, NumPy, Matplotlib, Seaborn, SciPy), Tableau, statistical analysis, hypothesis testing, EDA, data visualization, stakeholder communication

**Certificate:** Google Advanced Data Analytics Professional Certificate (Coursera) - in progress
