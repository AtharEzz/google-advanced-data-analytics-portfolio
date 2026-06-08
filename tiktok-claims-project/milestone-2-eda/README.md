# Milestone 2: Exploratory Data Analysis & Interactive Visualizations

## 📊 Executive & Interactive Deliverables
To translate our raw exploratory data analysis into actionable stakeholder insights, this phase includes both an interactive visual dashboard and an executive-level presentation brief:

* 🔗 **[View the Live Interactive TikTok Insights Story on Tableau Public](https://public.tableau.com/views/TikTokinsights/Story1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**
* 🖥️ **[View the Visual Executive Summary Presentation (Google Slides)](https://docs.google.com/presentation/d/1Mi7BTLvxbU9S83fWtETL2KB8TdbRmmRz39MCKvjj_Fg/edit?usp=sharing)**

---

## 📝 Executive Summary

### 🔍 Issue / Problem
The TikTok data team is building a machine learning model to automate the classification of claims in user submissions. As an initial step, this phase focuses on organizing, structuring, and profiling the raw data to ensure its integrity for predictive modeling.

### ⚙️ Response
The team conducted an exploratory data analysis (EDA) to isolate baseline user interaction patterns. The analysis specifically cross-examined high-signal engagement metrics (views, likes, shares, and comments) against author moderation histories to identify distinct behavioral signatures between content types.

### ⚡ Impact
Data profiling revealed minimal missing values and a stark operational imbalance: claim videos command the overwhelming share of platform traffic and engagement. Future modeling pipelines will leverage targeted data imputation and robust engineering practices to handle these distributions without biasing the model.

### 💡 Key Insights
* **Engagement Disparity:** Engagement metrics are heavily right-skewed; a tiny fraction of highly viral videos drives the vast majority of platform traffic. Total views are overwhelmingly dominated by "claim" content, while "opinion" content remains low-engagement.
* **Behavioral Baseline:** Clear boundaries separate claim and opinion videos. Authors with an active "banned" or "under review" status are strongly associated with high-engagement claim videos, making historical moderation status a primary feature for upcoming predictive modeling.

---


### 1. Video View Counts by Content Classification
* **Insight:** Videos categorized as a "claim" consistently accumulate a high baseline of views, stretching up to nearly 1,000,000 views. Conversely, "opinion" videos remain heavily compressed at the bottom of the scale, indicating that subjective opinions rarely achieve viral velocity.

### 2. Distribution of Video Durations
* **Insight:** The content length (`video_duration_sec`) shows an almost perfectly flat, uniform distribution from 5 to 60 seconds. This proves video duration is completely independent of performance metrics and does not influence content classification.

### 3. Author Moderation Status Segments
* **Insight:** Active authors show an even split between claims and opinions. However, authors flagged as "banned" or "under review" are overwhelmingly associated with publishing "claim" videos, providing a definitive feature signature for future classification models.
