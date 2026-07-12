# TikTok Claims Classification - Milestone 3: Hypothesis Testing

Part of the TikTok Claims Classification Project | Google Advanced Data Analytics Certificate - Course 3: The Power of Statistics

## Research Question

Does a TikTok video creator's verification status significantly impact the video's view count?

## Hypothesis

- **Null hypothesis (H₀):** There is no difference in mean video view count between verified and unverified accounts
- **Alternative hypothesis (H₁):** There is a statistically significant difference in mean video view count between verified and unverified accounts

## Method

Two-sample Welch's t-test was selected over a standard t-test because it does not assume equal variances between the two groups - appropriate here given the large difference in group sizes and spread.

- Significance level: α = 0.05
- Groups: verified accounts (n = 1,228) vs. unverified accounts (n = 17,856)

## Results

| Group | Mean Video View Count |
|---|---|
| Not Verified | 265,664 |
| Verified | 91,439 |
| Difference | 174,225 |

**Test results:**
- t-statistic: -25.50
- p-value: 2.61 × 10⁻¹²⁰

**Decision:** Reject the null hypothesis. The p-value is far below the 0.05 significance level, confirming the view count difference between verified and unverified accounts is statistically significant, not due to random chance.

## Key Insight

The result is counterintuitive: unverified accounts average nearly **3x more views** than verified accounts. This connects directly to the Course 2 EDA finding that unverified/banned accounts are overwhelmingly associated with claim videos, and claim videos drive massive view spikes compared to opinion videos.

This confirms that `verified_status` should be included as a feature in the upcoming classification model - not because verification directly causes higher views, but because it serves as a proxy signal for the type of content (claims vs. opinions) that drives platform engagement.

## Business Recommendation

TikTok should monitor unverified accounts closely. Because unverified accounts drive the biggest view spikes through claim content, ensuring this high-traffic content complies with platform safety guidelines is a priority for trust and safety teams.

## Deliverables

- `Activity_Course_4_TikTok_project_lab.ipynb` - Hypothesis testing notebook
- `TikTok_Course_3_executive_summary.pdf` - Stakeholder-ready executive summary

## Tools

Python, SciPy (stats.ttest_ind), Pandas, NumPy
