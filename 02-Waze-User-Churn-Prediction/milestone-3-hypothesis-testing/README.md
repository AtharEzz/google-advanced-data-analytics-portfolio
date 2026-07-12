# Waze User Churn Project - Milestone 3: Hypothesis Testing

Part of the Waze User Churn Prediction Project | Google Advanced Data Analytics Certificate - Course 3: The Power of Statistics

## Research Question

Does device type (iPhone vs. Android) significantly affect the number of drives per month among Waze users?

## Why This Matters

Waze leadership requested this analysis to determine whether building device-specific app updates could help reduce churn. If iPhone and Android users behave differently, device type should be prioritized as a feature in the churn prediction model and potentially addressed with tailored product changes.

## Hypothesis

- **Null hypothesis (H0):** There is no difference in the mean number of drives between iPhone and Android users
- **Alternative hypothesis (HA):** There is a statistically significant difference in the mean number of drives between iPhone and Android users

## Method

Two-sample Welch's t-test at significance level a = 0.05, with equal_var=False to avoid assuming equal variances between the two device groups.

## Results

| Group | Mean Monthly Drives |
|---|---|
| iPhone users | 67.86 |
| Android users | 66.23 |
| Difference | 1.63 |

**Test results:**
- t-statistic: 1.46
- p-value: 0.1434

**Decision:** Fail to reject the null hypothesis. The p-value (0.1434) is above the 0.05 significance level - the difference in mean drives between device types is not statistically significant.

## Key Insight

The 1.63 drive difference between iPhone and Android users is just random sampling variation, not a real behavioral difference. This is a valuable "negative" result - it directly answers a business question and prevents wasted effort.

## Business Recommendation

- Do not build device-specific app features to boost drive counts - the data does not support this investment
- Treat device type as a low-priority control variable in the churn prediction model, not a primary feature
- Redirect modeling focus toward behavioral features (app engagement days, km driven per session) which showed much stronger churn signals in the EDA phase

## Connection to Previous Findings

This result is consistent with the Data Inspection finding (Milestone 1) that device type showed no correlation with churn. The hypothesis test provides statistical confirmation of that earlier observation, closing the loop between exploratory and inferential analysis.

## Deliverables

- Activity_Course_4_Waze_project_lab.ipynb - Hypothesis testing notebook
- Waze_Course_3_executive_summary.pdf - Stakeholder-ready executive summary

## Tools

Python, SciPy (stats.ttest_ind), Pandas, NumPy
