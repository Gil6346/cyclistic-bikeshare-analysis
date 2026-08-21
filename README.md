# Cyclistic-Bikeshare-Analysis

## Overview

- Google Data Analytics Professional Certificate Capstone Project.
- This project analyses Cyclistic bike share usage to understand how annual members and casual riders use the service differently, with the aim of identifying opportunities to increase annual memberships.

## Project Status

- Completed on 20/08/2026

## Business Task

- How do annual members and casual riders use Cyclistic bikes differently?

- The analysis focus on differences in temporal usage patterns, ride duration, seasonal trends and station usage patterns.

## Dataset

- The analysis used 12 months of Cyclistic historical trip data.
- The analysis period is between June 2025 to May 2026.
- After cleaning, the analysis-ready-dataset contains 5.8 millions of valid trip records.

## Methodology
Raw CSV files

  ↓

Import & Merge

  ↓

Data Validation

  ↓

Cleaning

  ↓

Feature Engineering

  ↓

EDA

  ↓

Business Insights

  ↓

Recommendations

### Data Preparation
- The 12 monthly datasets were combined into a single dataset, after validating schema consistency across all files.
### Cleaning
- Datetime fields were converted to datetime format.
- Ride duration was introduced - calculated from start and end timestamps.
- Records with duplicate ride IDs were removed.
- Records with negative trip duration were removed.
- Records last longer than 24 hours were removed, due to unusual patterns observed.
- Records with missing start station or end station name were retained, station-level analysis was considered as a secondary analysis, the level of missingness was also documented as a limitation. 
### Feature Engineering
- Additional variables were derived to support temporal analysis, including ride date, month, day of week, hour of day, weekend status and time-of-day period.
### Exploratory Data Analysis
- Exploratory analysis compared annual members and casual riders across ride volume, ride duration, day of week, hour of day, weekend/weekday behaviour, bike type, monthly seasonality and starting-station patterns.
- Aggregation such as count, proportions, mean and median ride duration were used to identify differences between rider groups.
## Key Findings
1. Distinct usage pattern
- Members show stronger weekday commuting-like peaks, while casual riders show greater afternoon and weekend activity.
2. Ride duration
- Casual riders take longer trips on average than members.
3. Weekend behaviour
- Casual riders show substantially higher activity and longer ride duration on weekends.
- Members' weekend usage becomes more similar to casual riders' afternoon-oriented pattern, suggesting membership does not imply commuter-like-only usage.
4. Seasonality
- Both rider groups show higher ride volumes during warmer months and substantially lower activity during winter.
5. Station patterns
- Casual riders' high volume stations are more concentrated around recreational areas and lakefront, while members' usage is more concentrated around downtown and mixed-use areas.
## Business Recommendations
1. Distinct usage occasions
- Target casual riders during high usage weekend and afternoon periods and emphasise the flexibility of membership.
2. Seasonality
- Launch or increase membership campaigns ahead of and during warmer or high demand months.
3. Spatial targeting
- Prioritse high volume casual rider stations and nearby recreational destinations for targeted membership campaign tests and evaluate campaign performance.
## Limitations
- Approximately 21-22% of station name information is missing.
- Observational data does not establish causal relationships.
- Rider intent and membership conversion are not directly observed.
- Therefore, recommendations should be treated as hypotheses for targeted testing, rather than guaranteed drivers for membership conversion.
## Tools
- Python
- pandas
- NumPy
- Matplotlib
- seaborn
- Jupyter Notebook
- Git/GitHub
## Project Structure
00_Data/

├── 00_Raw/

├── 01_Interim/

└── 02_Processed/

01_Notebooks/

├── 01_import_merge.ipynb

├── 02_cleaning.ipynb

├── 03_feature_engineering.ipynb

└── 04_EDA.ipynb

20260820_Cyclistic_Business_Insight_Report.pdf

README.md

requirements.txt
## How to Reproduce
1. Clone the repository.
2. Install the required Python packages listed in "requirements.txt".
3. Download the original raw Cyclistic CSV files from [HERE](https://divvy-tripdata.s3.amazonaws.com/index.html).
4. Unzip the folders and place the raw CSV files in "00_Data/00_Raw/".
5. Run the notebooks in numberical order:
- "01_import_merge.ipynb"
- "02_cleaning.ipynb"
- "03_feature_engineering.ipynb"
- "04_eda.ipynb"