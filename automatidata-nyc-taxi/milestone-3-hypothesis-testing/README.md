# Automatidata - NYC Taxi Fare Prediction - Milestone 3: Hypothesis Testing (A/B Test)

Part of the Automatidata NYC TLC Project | Google Advanced Data Analytics Certificate - Course 3: The Power of Statistics

## Research Question

Do customers who pay by credit card pay a higher average fare amount than customers who pay by cash?

## Business Context

Taxi drivers want to maximize their daily earnings. If credit card users consistently pay higher fares, encouraging card payments could directly increase driver revenue - without requiring any changes to the fare structure itself.

## Hypothesis

- **Null hypothesis (H0):** There is no difference in the average fare amount between credit card and cash customers
- **Alternative hypothesis (HA):** There is a statistically significant difference in average fare amount between credit card and cash customers

## Method

Two-sample Welch's t-test (equal_var=False) at significance level a = 0.05, comparing fare_amount for payment_type=1 (credit card) vs payment_type=2 (cash).

## Results

| Payment Type | Mean Fare Amount |
|---|---|
| Credit card (type 1) | $13.43 |
| Cash (type 2) | $12.21 |
| Difference | $1.22 |

**Test results:**
- t-statistic: 6.87
- p-value: 6.80 x 10^-12

**Decision:** Reject the null hypothesis. The p-value is far below 0.05 - credit card users pay statistically significantly higher fares than cash users.

## Key Insight

Credit card users pay on average $1.22 more per trip than cash users. This difference is statistically real, not random chance.

**Business recommendation:**
- Make the in-cab card payment screen fast and easy, with preset tipping buttons to encourage larger card transactions
- Share these findings with drivers to show that accepting cards leads to higher fares, which easily covers any small card processing fees

## Important Caveat

This A/B test has a real-world limitation worth noting: payment type is not randomly assigned - passengers choose how to pay based on their own habits. This means the higher credit card fares could partly reflect differences in the types of trips taken by card vs. cash users (e.g., longer trips, airport runs) rather than the payment method itself causing higher fares. A true experiment would randomly assign payment type, which is not realistic in practice. This finding is directionally useful but should be interpreted with this assumption in mind.

## Deliverables

- Activity__Course_4_Automatidata_project_lab.ipynb - A/B test notebook
- Course_3_Automatidata_Executive_Summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, SciPy (stats.ttest_ind)
