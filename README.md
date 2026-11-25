# Cyclistic Bike-Share: Turning Casual Riders into Members

*last updated: 25/11/2026*

**Python (pandas, NumPy, matplotlib, seaborn) · 5.8 million trips · June 2025 – May 2026**

> **The headline:** casual riders are not a different kind of customer. On weekends, members ride almost exactly like casual riders do. So Cyclistic should stop selling membership as a commuter product and sell it as **"one pass for your weekday trips and your weekend rides"**, launched in late spring at the lakefront stations where casual riders already are.

📄 [Business insight report (PDF)](20260820_Cyclistic_Business_Insight_Report.pdf) · 📓 [EDA notebook](01_Notebooks/04_eda.ipynb)

---

## Key findings

### 1. On weekends, members and casual riders ride the same way

![Hourly ride pattern, weekday vs weekend](04_images/01_Figures/01_hourly_weekday_vs_weekend.png)

- On **weekdays**, members show a clear commuting pattern, with peaks at 8 AM and 5 PM.
- On **weekends**, that pattern disappears. Member and casual riders follow almost the same curve, rising through the late morning and staying high until about 5 PM.
- Casual riders take **37.8%** of their rides at the weekend, compared with **23.6%** for members. At weekends, casual riders take **47%** of all rides, against 31% on weekdays.
- Casual rides are longer (median **11.2 min** vs **8.6 min** for members).

**So what:** members already use the service for leisure. The "membership = commuting" message leaves out how members actually ride, and it doesn't speak to casual riders at all.

### 2. Casual demand is highly seasonal

![Monthly rider mix](04_images/01_Figures/02_monthly_rider_mix.png)

- Casual riders account for **43%** of rides in June, July and August, but only **18%** in January.
- Members' monthly volumes vary too, but their daily pattern stays the same all year.

**So what:** the pool of casual riders to convert is largest in summer. A campaign has to be live before June, not during it.

### 3. Casual riders are concentrated at a few lakefront stations

![Top start stations by rider type](04_images/01_Figures/03_top_start_stations.png)

- All of casual riders' top 10 start stations are at the lakefront or major attractions. **Navy Pier** alone had **38,837** casual rides, about 1.7 times the busiest member station (22,514).
- Members' top stations are in the business district on weekdays. At weekends, three lakefront stations (DuSable Lake Shore Dr & North Blvd, Theater on the Lake, Navy Pier) enter their top 10.

**So what:** a small number of stations reaches a large share of casual riders, which makes a low-cost, measurable pilot possible.

---

## Recommendations

| # | Recommendation | Evidence | How to measure it |
|---|---|---|---|
| 1 | **Reposition membership** as one pass for weekday trips *and* weekend leisure, not commuting only | Finding 1: members' weekend curve matches casual riders' | Conversion rate of casual riders exposed to the new message vs the old one |
| 2 | **Launch in May**, ahead of the June–August peak | Finding 2: casual share of rides rises from 18% to 43% | Membership sign-ups in May–August vs the same period last year |
| 3 | **Pilot at the top casual stations** on weekend afternoons (12–5 PM), with a matched control group of stations | Finding 3: Navy Pier, DuSable Lake Shore Dr & Monroe St, Michigan Ave & Oak St | Sign-ups at pilot stations vs control stations (A/B test) |

---

## What makes this analysis reliable

A **rerunnable cleaning pipeline** across 12 monthly files (5,848,703 raw records → **5,842,803** clean):

| Check | Records | Decision |
|---|---|---|
| Schema consistency across 12 files | 12 files | Validated before merging |
| Duplicate ride IDs | 35 | Removed |
| End time before start time | 29 | Removed |
| Trips over 24 hours | 5,836 (0.10%) | **Investigated:** clustered at ~1,500 minutes, mostly missing end stations, classic bikes only. Treated as system artefacts and removed, with the rule documented |
| Trips under 1 minute | 161,323 (2.76%) | Checked by rider type, bike type and location; retained |
| Missing station names | ~21–22% of trips | Retained; station analysis treated as supporting evidence only |

## Limitations

- **Rides, not riders.** The data has no rider ID, so it can't show how many *people* are casual riders, how often the same person rides, or who later became a member. The recommendations are hypotheses to test, which is why each one has a measure.
- About 21–22% of trips have no station name (slightly more for casual riders' end stations), so station results describe trips with a recorded station only.
- The data is observational: it shows patterns, not causes.
- No pricing data, so the analysis can't say whether membership would actually be cheaper for a given casual rider.

**With more data, the next step would be:** a rider ID to count repeat casual riders (the most likely converts), and pricing data to show each of them what membership would save.

---

## Method

Raw CSVs → import & merge → validation → cleaning → feature engineering (date, month, day of week, hour, weekend flag, time-of-day period) → EDA comparing members and casual riders by volume, duration, day, hour, season, bike type and station.

## Project structure

```
00_Data/            raw, interim and processed data (not committed; see below)
01_Notebooks/
  01_import_merge.ipynb
  02_cleaning.ipynb
  03_feature_engineering.ipynb
  04_eda.ipynb
images/             key charts used in this README
20260820_Cyclistic_Business_Insight_Report.pdf
requirements.txt
```

## How to reproduce

1. Clone the repository and install the packages in `requirements.txt`.
2. Download the 12 monthly trip files (June 2025 – May 2026) from the [Divvy trip data page](https://divvy-tripdata.s3.amazonaws.com/index.html), unzip them and place the CSVs in `00_Data/00_Raw/`.
3. Run the notebooks in order, from `01_import_merge.ipynb` to `04_eda.ipynb`.

*Data provided by Motivate International Inc. under the Divvy data licence, as part of the Google Data Analytics Professional Certificate capstone.*