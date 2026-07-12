# Automatidata - NYC Taxi Fare Prediction - Milestone 1: Data Inspection

Part of the Automatidata NYC TLC Project | Google Advanced Data Analytics Certificate - Course 1: Foundations of Data Science

## Business Problem

The New York City Taxi and Limousine Commission (NYC TLC) needs a model to predict taxi fare amounts before a trip begins. Accurate fare prediction enables:
- Better fare transparency for passengers before they enter a cab
- Improved trip planning and budgeting for regular commuters
- A foundation for detecting fare anomalies and billing errors at scale

## Dataset

- **Source:** NYC TLC 2017 Yellow Taxi Trip Data
- **Full dataset:** 408,294 trips, 18 variables
- **Analysis sample:** 22,699 trips
- **Key variables:** pickup/dropoff datetime, trip distance, passenger count, payment type, fare amount, tip amount, total amount, vendor ID, rate code, location IDs

## Goal of This Milestone

Inspect and understand the raw dataset to assess its readiness for EDA, visualization, and predictive modeling. Identify data quality issues that must be addressed before analysis can begin.

## Key Findings

**Data Quality Issues Identified:**
- `tpep_pickup_datetime` and `tpep_dropoff_datetime` stored as strings (object dtype) - must be converted to datetime format before any time-based analysis
- Negative values present in `fare_amount` and `total_amount` (minimum: -120.30) - represent billing errors or disputed trips requiring cleaning
- Zero-distance trips present in `trip_distance` - likely errors or cancelled trips

**Anomalies Found:**
- Extreme outlier: row 8476, a 2.60-mile trip with total_amount = $1,200.29 - extreme fare and tip combination, likely an error
- Second highest total: $450.30 for a trip lasting only 9 seconds - another anomalous record
- Longest trips are not necessarily the most expensive - trip distance alone insufficient for fare prediction

**Payment Behavior Insights:**
- 67.3% of trips paid by credit card (15,265), 32.0% by cash (7,267)
- Credit card average tip: $2.73 vs. cash average tip: $0.00 - cash tips not captured in the system, creating a systematic measurement gap that affects tip modeling
- Both vendors show nearly identical mean total amounts (Vendor 1: $16.30, Vendor 2: $16.32) - vendor type unlikely to be a useful predictive feature

**Variables Identified for Modeling:**
- `trip_distance` and `total_amount` identified as the two strongest candidate variables for the fare prediction model

## Next Steps

1. Convert datetime columns to proper datetime format
2. Handle negative fare and total amount values
3. Investigate and decide on outlier treatment strategy
4. Conduct full EDA with visualizations (Milestone 2)

## Deliverables

- `Activity_Course_2_Automatidata_project_lab.ipynb` - Data inspection notebook
- `Course_1_Automatidata_executive_summary.pdf` - Stakeholder executive summary
- `Automatidata_project_proposal.docx` - Project proposal and PACE strategy document

## Tools

Python, Pandas, NumPy
