# Google Advanced Data Analytics Portfolio

Guided case study projects completed as part of the **Google Advanced Data Analytics Professional Certificate** (in progress), following the PACE framework (Plan, Analyze, Construct, Execute) used in professional data analytics work.

Each course applies a new set of analytical skills to one of two ongoing business scenarios: predicting user churn for **Waze** (navigation app) and classifying user claims for **TikTok**. Each milestone builds on the previous one, simulating a real end-to-end analytics project.

---

## Project 1: Waze User Churn Prediction

**Business problem:** Waze's data team needs to identify users likely to uninstall or stop using the app (churn), in order to improve retention strategies.

**Dataset:** 14,999 users, 13 variables (driving behavior, device type, session data, churn label)

| Milestone | Focus | Key Deliverables |
|---|---|---|
| 1 — Planning | Initial data inspection & profiling | Executive summary, missing value analysis, churn rate baseline |
| 2 — EDA | Exploratory data analysis & visualization | Executive summary, distribution analysis, outlier detection, churn behavior visualization |
| 3+ | Statistical testing, modeling | Upcoming |

**Key findings (Milestone 1 — Data Inspection):**
- 17.74% of users churned; 82.26% retained
- 700 missing values in the label column; device distribution consistent across missing vs. non-missing rows — likely missing at random
- Churned users drove ~240% more km per driving day than retained users
- Device type (iPhone vs. Android) not correlated with churn

**Key findings (Milestone 2 — EDA):**
- Users who drove all 30 days had a **0% churn rate** vs. **40% churn rate** for inactive users — app engagement frequency is the strongest early churn signal identified
- Positive correlation between daily driving distance and churn — longer-distance drivers are more likely to churn
- User representation stable across all tenure lengths up to ~10 years
- Outliers identified in `driven_km_drives`, `activity_days`, and `driving_days` — flagged for handling before modeling

---

## Project 2: TikTok Claims Classification

**Business problem:** TikTok needs to automate the classification of user-submitted content as either "claims" (verifiable factual statements) or "opinions" (subjective expressions), to prioritize content moderation resources efficiently.

**Dataset:** ~19,000 videos with engagement metrics (views, likes, shares, comments), author status, and claim/opinion label

| Milestone | Focus | Key Deliverables |
|---|---|---|
| 1 — Planning & Inspection | Initial data structuring and variable analysis | Executive summary, class balance check, engagement comparison by claim status |
| 2+ | EDA, statistical testing, modeling | Upcoming |

**Key findings (Milestone 1):**
- Dataset is nearly balanced: **50.3% claims, 49.7% opinions** — no class imbalance issue for modeling
- Claims accumulate **~100x more views** than opinions: mean views for claims = 501,029 vs. opinions = 4,956 — a striking engagement gap suggesting claims spread virally
- Claims maintain a ~33% like-per-view ratio vs. ~22% for opinions — higher relative engagement per view as well
- **Author ban status is a strong proxy signal**: authors flagged as "Banned" or "Under Review" are heavily associated with claim videos (share counts: 17,774–19,018), while active/good-standing authors are predominantly associated with opinion videos (share counts: 108–124)
- These patterns suggest author status and engagement metrics could serve as powerful features in a future classification model

---

## Framework

Both projects follow the **PACE** framework:
- **Plan** — Define the problem, understand stakeholder needs, assess the data
- **Analyze** — Inspect, clean, and explore the data
- **Construct** — Build statistical models or visualizations
- **Execute** — Communicate findings to stakeholders via executive summaries

Each milestone includes a Jupyter notebook (analysis) and an executive summary PDF (stakeholder communication) — reflecting the dual technical/communication deliverables of real analytics work.

---

## Tools & Skills

Python (Pandas, NumPy, Matplotlib, Seaborn), statistical analysis, EDA, data visualization, stakeholder communication

**Certificate:** Google Advanced Data Analytics Professional Certificate (Coursera) — in progress
