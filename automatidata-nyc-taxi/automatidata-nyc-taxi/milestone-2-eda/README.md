# Automatidata - NYC Taxi Fare Prediction - Milestone 2: EDA

Part of the Automatidata NYC TLC Project | Google Advanced Data Analytics Certificate - Course 2: Go Beyond the Numbers

## Goal of This Milestone

Conduct exploratory data analysis to understand ride patterns, driver earnings, and trip costs. Identify data quality issues requiring cleaning before modeling, and create visualizations for stakeholder communication in both Python and Tableau.

## Key Findings

**Data Quality Issues Confirmed for Cleaning:**
- Negative fare and total amount values (down to -120.30) - billing errors
- Zero-distance trips that still recorded a cost
- Impossibly high fares (up to $1,200.29)
- Invalid RateCodeID values (e.g., 99) not in the data dictionary
- 49 drop-off location IDs with no recorded trips (out of 216 unique IDs)

**Trip Distribution:**
- 75% of all NYC taxi trips are under 3.06 miles long and cost $17.80 or less
- The vast majority of rides are short and affordable - extreme outliers heavily skew the mean

**Temporal Patterns:**
- Busiest months: March (2,049 rides) and October (2,027 rides)
- Slowest months: July (1,697 rides) and August (1,724 rides)
- Highest revenue days: Thursday ($57,182) and Friday ($55,819)
- Lowest revenue day: Sunday ($48,624)

**Tipping Behavior:**
- Solo passengers (1 person) tip slightly less on average ($1.85) than groups of 2 ($1.86) or 5 ($1.87)
- Passengers with 0 recorded passengers tip the most on average ($2.14) - likely a data entry issue
- Tips for rides with >$10 tip show no significant difference between vendors

**Visualizations Produced:**
- Boxplots and histograms for trip_distance, total_amount, and tip_amount
- Tip amount by vendor (stacked histogram)
- Mean tips by passenger count (bar chart with global mean reference line)
- Ride count by month and by day of week (bar charts)
- Total revenue by month and by day of week (bar charts)
- Mean trip distance by drop-off location (bar chart across 216 locations)
- Tableau scatter plot: trip_distance vs total_amount relationship

## Connection to Next Steps

These findings directly shape the modeling phase:
- Datetime columns converted to proper format in this notebook - trip duration can now be calculated as a feature
- Cleaning decisions documented: remove negative fares, filter zero-distance trips, handle RateCodeID=99
- trip_distance and total_amount confirmed as the two strongest modeling candidates
- A Tableau business dashboard is planned as the next deliverable

## Deliverables

- Activity_Course_3_Automatidata_project_lab.ipynb - EDA notebook with Python visualizations
- Course_2_Automatidata_Executive_Summary.pdf - Stakeholder executive summary with Tableau scatter plot

## Tools

Python, Pandas, NumPy, Matplotlib, Seaborn, Tableau
