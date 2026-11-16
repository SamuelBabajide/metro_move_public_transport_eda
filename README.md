# Optimizing Public Transit Operations

### MetroMove Transit Solutions: An Exploratory Data Analysis of Public Transportation

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Charts-3F4F75?logo=plotly&logoColor=white)

An end-to-end exploratory data analysis (EDA) of 1,000 public transport trip records across four transport modes (Bus, Train, Ferry and Tram). The project takes a messy, inconsistent and incomplete raw dataset, cleans and imputes it into an analysis-ready table, and then uses univariate, bivariate and multivariate visualisations to uncover patterns in passenger demand, fares, routes and revenue that can drive operational decisions.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Business Background](#2-business-background)
3. [Problem Statement & Objective](#3-problem-statement--objective)
4. [Project Goals & Deliverables](#4-project-goals--deliverables)
5. [Repository Structure](#5-repository-structure)
6. [Tools and Technologies](#6-tools-and-technologies)
7. [Dataset Description](#7-dataset-description)
8. [Data Cleaning & Transformation](#8-data-cleaning--transformation)
9. [Missing Value Imputation](#9-missing-value-imputation)
10. [Descriptive Summary Statistics](#10-descriptive-summary-statistics)
11. [Outlier Detection](#11-outlier-detection)
12. [Exporting the Cleaned Dataset](#12-exporting-the-cleaned-dataset)
13. [Visualisation Approach & Colour Palette](#13-visualisation-approach--colour-palette)
14. [Univariate Analysis](#14-univariate-analysis)
15. [Bivariate Analysis](#15-bivariate-analysis)
16. [Multivariate Analysis](#16-multivariate-analysis)
17. [Key Insights Summary](#17-key-insights-summary)
18. [Conclusions & Recommendations](#18-conclusions--recommendations)
19. [Limitations](#19-limitations)
20. [Future Work](#20-future-work)
21. [How to Run This Project](#21-how-to-run-this-project)
22. [Author & Contact](#22-author--contact)

---

## 1. Project Overview

| Item | Detail |
|---|---|
| **Organisation** | MetroMove Transit Solutions (multi-city public transport provider) |
| **Project type** | Exploratory Data Analysis (EDA) capstone |
| **Dataset** | `Public_Transport_Trips_EDA.xlsx`: 1,000 trips × 12 raw columns |
| **Transport modes** | Bus, Train, Ferry, Tram |
| **Stations** | Airport, Central, Downtown, North Station, South Point, West End |
| **Core workflow** | Data exploration → cleaning & transformation → imputation → descriptive statistics → outlier checks → univariate, bivariate & multivariate visualisation → recommendations |
| **Outputs** | Cleaned dataset (`data_saved.xlsx`), commented Jupyter notebook, 22-slide presentation |

**Headline numbers (after cleaning):**

| Avg Fare | Avg Trip Duration | Avg Passengers per Trip | Total Trips | Total Revenue |
|:---:|:---:|:---:|:---:|:---:|
| **£25.36** | **94.8 min** | **49** | **1,000** | **≈ £1.25m** |

---

## 2. Business Background

### 2.1 About MetroMove Transit Solutions

MetroMove Transit Solutions is a public transportation service provider operating across multiple cities and managing thousands of daily trips by:

 🔴 **Bus**
 🟢 **Train**
 🔵 **Ferry**
 🟡 **Tram**

**Mission:** efficient, affordable and timely transportation, powered by data.

### 2.2 The Challenge

- A large volume of trip data is collected across operations.
- Records are messy, inconsistent and incomplete, which blocks insight.
- There is little visibility into trip performance and passenger behaviour.
- Fare patterns are not yet understood well enough to support pricing optimisation.
- A new data-driven initiative needs a clean analytical foundation to build on.

---

## 3. Problem Statement & Objective

**Problem statement.** MetroMove has collected a large volume of trip data but lacks insight into trip performance, passenger behaviour and fare patterns because the records are messy, inconsistent and incomplete. As part of its new data-driven initiative, the company wants to clean, explore and summarise its trip records to identify the inefficiencies and patterns that can drive operational improvements.

**Why it matters for decision-making.** Effective operational decisions rely on understanding how passengers use the network, how each transport mode performs, and how trip characteristics shape the customer experience. None of that is possible until the underlying data can be trusted.

**Rationale for an EDA.** Before any modelling or pricing work, the business needs a single, clean, well-understood version of its trip data. EDA delivers exactly that: it fixes the data, describes it, and surfaces the patterns worth acting on.

---

## 4. Project Goals & Deliverables

**Goals**

1. Clean and preprocess the raw trip data.
2. Discover patterns through exploratory data analysis.
3. Communicate data-driven insights within a real-world transportation context.

**Deliverables**

| # | Deliverable | Description |
|:---:|---|---|
| 1 | **Data Cleaning** | Casing and whitespace fixes, date engineering, and group-median imputation of missing values |
| 2 | **Data Exploration** | Shape, data types, unique counts and sample inspection |
| 3 | **Descriptive Statistics** | Mean, median, mode, range, variance and standard deviation for all numeric columns |
| 4 | **EDA Visualisations** | Univariate, bivariate and multivariate Plotly charts |
| 5 | **Jupyter Notebook** | Fully commented notebook with inline observations, plus a supporting slide deck |

---

## 5. Repository Structure

```
MetroMove-Public-Transport-EDA/
│
├── public_transport_script.ipynb       # Main analysis notebook
├── Public_Transport_Trips_EDA.xlsx     # Raw dataset (input)
├── data_saved.xlsx                     # Cleaned dataset (generated by the notebook)
├── requirements.txt                    # Python dependencies
│
├── presentation/
│   └── MetroMove_EDA_Presentation.pptx # Stakeholder slide deck (22 slides)
│
├── images/                             # Static chart exports used in this README
│   ├── 01_missing_values.png
│   ├── 02_outlier_boxplot.png
│   ├── 03_fare_distribution.png
│   ├── 04_mode_distribution.png
│   ├── 05_passenger_distribution.png
│   ├── 06_weekly_demand.png
│   ├── 07_fare_vs_duration.png
│   ├── 08_fare_by_mode.png
│   ├── 09_station_od_heatmap.png
│   ├── 10_revenue_station_mode.png
│   ├── 11_avg_fare_mode_day.png
│   └── 12_trips_passengers_mode_day.png
│
└── README.md
```

> **Note:** The notebook reads `Public_Transport_Trips_EDA.xlsx` and writes `data_saved.xlsx` using relative paths, so keep the notebook and both Excel files in the same folder.

---

## 6. Tools and Technologies

| Category | Tools |
|---|---|
| Language | Python 3.12 |
| Environment | Jupyter Notebook (Anaconda) |
| Data wrangling | `pandas`, `numpy` |
| Excel I/O | `openpyxl` (engine behind `pd.read_excel` / `to_excel`) |
| Missing-data visualisation | `missingno` |
| Static plotting | `matplotlib`, `seaborn` |
| Interactive plotting | `plotly.express`, `plotly.figure_factory`, `plotly.graph_objects` |
| Static chart export (optional) | `kaleido` |

```python
import numpy as np
import pandas as pd
import missingno as msno
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import plotly.figure_factory as ff
import plotly.graph_objects as go
```

---

## 7. Dataset Description

### 7.1 Data Dictionary

| Column | Type (raw) | Description | Known issues in raw data |
|---|---|---|---|
| `Trip_ID` | object | Unique identifier for each trip (e.g. `TRIP0001`) | None |
| `Mode_of_Transport` | object | Type of transport: Bus, Train, Ferry or Tram | Inconsistent casing (9 raw labels for 4 modes, e.g. `bus` vs `Bus`) |
| `Departure_Station` | object | Station where the trip starts | Leading/trailing whitespace (7 raw values for 6 stations) |
| `Arrival_Station` | object | Station where the trip ends | Inconsistent casing (e.g. `airport` vs `Airport`) |
| `Departure_Time` | datetime | Time the trip departed | Needs rounding for time-of-day analysis |
| `Passenger_Count` | float | Number of passengers on the trip | 100 missing values (10%) |
| `Fare_Amount` | float | Amount paid per passenger for the trip (£) | 100 missing values (10%) |
| `Trip_Duration_Minutes` | float | Duration of the trip in minutes | 100 missing values (10%) |
| `Trip_Date` | datetime | Date on which the trip occurred | Needs consistent formatting |
| `Day_of_Week` | object | Day of the week on which the trip occurred | None |
| `Unnamed: 10` | float | Excel export artefact | Completely empty (0 non-null) |
| `Unnamed: 11` | object | Excel export artefact | 299 stray values with no analytical meaning |

### 7.2 Initial Data Profile

**Shape:** `(1000, 12)`, so 1,000 trips and 12 columns, of which 10 carry data and 2 are export artefacts.

**Unique values per column (raw):**

| Column | Unique values |
|---|---:|
| Trip_ID | 1,000 |
| Mode_of_Transport | 9 |
| Departure_Station | 7 |
| Arrival_Station | 7 |
| Departure_Time | 1,000 |
| Passenger_Count | 100 |
| Fare_Amount | 901 |
| Trip_Duration_Minutes | 175 |
| Trip_Date | 42 |
| Day_of_Week | 7 |

**Sample inspection** (`raw_data.sample(7)`) immediately exposed the quality problems: mixed-case mode labels (`bus`, `train`, `Ferry`), lower-case station names (`airport`) and stray values in `Unnamed: 11`.

### 7.3 Data Quality Issues Identified

| # | Issue | Columns affected | Impact if left unfixed |
|:---:|---|---|---|
| 1 | Empty / stray export columns | `Unnamed: 10`, `Unnamed: 11` | Noise in every downstream table |
| 2 | Inconsistent casing | `Mode_of_Transport`, `Arrival_Station` | One mode or station counted as several categories |
| 3 | Leading/trailing whitespace | `Departure_Station` | False-duplicate station and route counts |
| 4 | Missing values (10% each) | `Passenger_Count`, `Fare_Amount`, `Trip_Duration_Minutes` | Biased totals and averages; broken revenue calculation |
| 5 | Raw date/time formats | `Departure_Time`, `Trip_Date` | Hard to read and to analyse by hour or date |

#### Chart 1: Count of Complete Values per Column

<img width="1117" height="450" alt="image" src="https://github.com/user-attachments/assets/8ce0fc01-a795-4bb6-8f50-07feb3254024" />

*The bar chart confirms 900 of 1,000 values present in `Passenger_Count`, `Fare_Amount` and `Trip_Duration_Minutes`, a fully empty `Unnamed: 10`, and a sparsely populated `Unnamed: 11`.*

---

## 8. Data Cleaning & Transformation

All cleaning is applied to a copy (`data = raw_data.copy()`) so the raw table is never modified. The steps run in the order below. Imputation (Section 9) runs **before** the date engineering, because the arrival-date logic needs a complete trip duration for every record.

### 8.1 Dropping Unnamed Columns

```python
data = data.drop(columns=['Unnamed: 10', 'Unnamed: 11'])
```

**Why:** both are Excel export artefacts. `Unnamed: 10` is completely empty, and `Unnamed: 11` only holds stray values with no meaning in a trip record.

### 8.2 Stripping Whitespace from Categorical Columns

```python
cat_cols = ['Mode_of_Transport', 'Departure_Station', 'Arrival_Station']
data[cat_cols] = data[cat_cols].apply(lambda col: col.astype(str).str.strip())
```

**Why:** trailing spaces in `Departure_Station` made the same station appear as two different values (7 raw values for 6 real stations), which would inflate route counts. Stripping all three categorical columns guards against the same issue anywhere else.

### 8.3 Standardising Categorical Casing

```python
data[cat_cols] = data[cat_cols].apply(lambda col: col.str.title())
```

**Why:** `Title Case` gives every value a single spelling (`bus`, `Bus` → `Bus`; `airport` → `Airport`). Applying it to **both** station columns means departure and arrival names match exactly (for example `North Station` in both), which keeps the origin-destination analysis aligned.

**Result:** 9 raw mode labels → **4 modes**; 7 raw departure values → **6 stations**; arrival names now match departure names.

### 8.4 Date & Time Transformation

```python
departure_dt_raw = pd.to_datetime(data['Departure_Time'])
trip_date = pd.to_datetime(data['Trip_Date']).dt.normalize()

# Round departure time to the nearest whole hour, e.g. 17:53 -> 18:00
data['Departure_Time'] = departure_dt_raw.dt.round('h').dt.strftime('%H:00')

# Format the trip date as DD-MMM-YYYY, e.g. 01-Jan-2024
data['Trip_Date'] = trip_date.dt.strftime('%d-%b-%Y')
```

**Why:** an hourly `Departure_Time` is easier to group for time-of-day analysis, and a single readable date format (`DD-MMM-YYYY`) keeps reporting consistent.

### 8.5 Arrival Date Engineering (Overnight Trips)

A trip that leaves late in the evening can arrive after midnight, so its arrival date differs from its trip date. A new `Arrival_Date` column captures this:

```python
# Full departure timestamp = trip date + exact time of day the trip left
time_of_day = departure_dt_raw - departure_dt_raw.dt.normalize()
departure_timestamp = trip_date + time_of_day

# Arrival timestamp = departure timestamp + (imputed) trip duration
arrival_timestamp = departure_timestamp + pd.to_timedelta(data['Trip_Duration_Minutes'], unit='m')

# Calendar date rolls forward one day when the trip passes midnight
data['Arrival_Date'] = arrival_timestamp.dt.strftime('%d-%b-%Y')
```

**Why this approach:**
- It uses the **exact** departure time (before rounding), so a trip leaving at 23:40 for 30 minutes is correctly dated to the next day.
- It runs **after imputation**, so all 1,000 trips have a real duration rather than a placeholder.
- *Example:* departs 22:30 on 05-Jan-2024, lasts 120 minutes → `Arrival_Date = 06-Jan-2024`.

**Final cleaned schema:** 1,000 rows × 11 columns (the 10 original data columns plus `Arrival_Date`), with **0 missing values**.

---

## 9. Missing Value Imputation

### 9.1 Imputation Strategy & Rationale

Three numeric columns each had exactly **100 missing values (10%)**. Each gap is filled with the **median of the most specific matching group**, followed by a **`Mode_of_Transport`-level fallback** for any group that had no observed value to take a median from.

**Why group medians:**
- The **median** is robust to skew and extreme values, unlike the mean.
- **Grouping** borrows information from similar trips (same mode, route or day), so imputed values respect the structure of the data instead of flattening everything to one global number.
- The **fallback** guarantees no record is left empty when a fine-grained group is sparse.

| Column | Primary grouping | Fallback | Post-processing |
|---|---|---|---|
| `Passenger_Count` | Mode × Day of Week × Departure Station | Mode | Cast to `int` |
| `Trip_Duration_Minutes` | Mode × Departure Station × Arrival Station | Mode | Cast to `int` |
| `Fare_Amount` | Mode × Departure Station × Arrival Station | Not required | Kept as `float` |

### 9.2 Passenger_Count

```python
data["Passenger_Count"] = data["Passenger_Count"].fillna(
    data.groupby(["Mode_of_Transport", "Day_of_Week", "Departure_Station"])
        ["Passenger_Count"].transform("median"))

# Fallback for any remaining gaps
data["Passenger_Count"] = data["Passenger_Count"].fillna(
    data.groupby("Mode_of_Transport")["Passenger_Count"].transform("median"))

data['Passenger_Count'] = data['Passenger_Count'].astype(int)
```

**Rationale:** average passengers per trip are similar across modes (about 46 to 51), so day of week and origin station add the extra context needed for a closer estimate. Casting to `int` keeps passenger counts whole.

### 9.3 Trip_Duration_Minutes

```python
data["Trip_Duration_Minutes"] = data["Trip_Duration_Minutes"].fillna(
    data.groupby(["Mode_of_Transport", "Departure_Station", "Arrival_Station"])
        ["Trip_Duration_Minutes"].transform("median"))

# Fallback for any remaining gaps
data["Trip_Duration_Minutes"] = data["Trip_Duration_Minutes"].fillna(
    data.groupby("Mode_of_Transport")["Trip_Duration_Minutes"].transform("median"))

data['Trip_Duration_Minutes'] = data['Trip_Duration_Minutes'].astype(int)
```

**Rationale:** trip length is driven by the route travelled, so mode plus origin and destination is the natural grouping. No observed duration has a fractional part, so the column is stored as an integer.

### 9.4 Fare_Amount

```python
data["Fare_Amount"] = data["Fare_Amount"].fillna(
    data.groupby(["Mode_of_Transport", "Departure_Station", "Arrival_Station"])
        ["Fare_Amount"].transform("median"))
```

**Rationale:** fares range from £0.50 to £49.95, and route-level grouping reflects fixed per-route pricing. Every route group contained observed fares, so all 100 gaps were filled at this level and no fallback was needed.

### 9.5 Alternative Methods Considered

**KNN imputation** and **regression imputation** were considered but not used. The numeric columns show near-zero correlation with each other (for example, fare vs trip duration r ≈ −0.05), so a model-based method would have little signal to learn from and would not outperform simple, transparent group medians.

### 9.6 Post-Imputation Validation

`data.info()` after cleaning confirms **1,000 non-null values in every column**:

| Column | Non-null | Dtype |
|---|---:|---|
| Trip_ID | 1000 | object |
| Mode_of_Transport | 1000 | object |
| Departure_Station | 1000 | object |
| Arrival_Station | 1000 | object |
| Departure_Time | 1000 | object |
| Passenger_Count | 1000 | int |
| Fare_Amount | 1000 | float64 |
| Trip_Duration_Minutes | 1000 | int |
| Trip_Date | 1000 | object |
| Day_of_Week | 1000 | object |
| Arrival_Date | 1000 | object |

---

## 10. Descriptive Summary Statistics

### 10.1 Summary Table

Calculated on the cleaned dataset (after imputation):

| Metric | Passenger_Count | Fare_Amount (£) | Trip_Duration_Minutes |
|---|---:|---:|---:|
| Count | 1,000 | 1,000 | 1,000 |
| **Mean** | 48.96 | 25.36 | 94.76 |
| **Median** | 48.00 | 25.45 | 97.00 |
| **Mode** | 47 | 31.32 | 100 |
| Minimum | 1 | 0.50 | 5 |
| 25th percentile | 26.00 | 13.63 | 53.75 |
| 75th percentile | 70.00 | 37.03 | 135.00 |
| Maximum | 99 | 49.95 | 179 |
| **Range** | 98 | 49.44 | 174 |
| **Variance** | 725.99 | 195.48 | 2,414.46 |
| **Standard Deviation** | 26.94 | 13.98 | 49.14 |

**Observations:**
- For all three metrics the **mean and median are almost equal**, which points to roughly symmetric distributions with no strong skew.
- The quartiles are spread evenly between the minimum and maximum, consistent with the **near-uniform distributions** seen in the univariate charts.
- Fares sit between £0.50 and £49.95, trips last between 5 minutes and just under 3 hours, and loads range from a single passenger to 99.

### 10.2 Headline KPIs

| Avg Fare | Avg Duration | Avg Passengers | Total Trips |
|:---:|:---:|:---:|:---:|
| **£25.36** | **94.8 min** | **49 riders** | **1,000** |

---

## 11. Outlier Detection

```python
plt.figure(figsize=(6, 4))
sns.boxplot(data=data)
plt.title("Outlier Detection Across Dataset")
plt.show()
```

#### Chart 2: Outlier Detection Across Dataset, Numerical Columns - Boxplot

<img width="512" height="357" alt="image" src="https://github.com/user-attachments/assets/dada61a0-9393-43f8-a7ff-c3e3e00af09e" />

**Findings:** using the standard 1.5 × IQR rule, no value in any numeric column falls outside the whiskers:

| Column | Q1 | Q3 | IQR | Lower fence | Upper fence | Observed min / max | Outliers |
|---|---:|---:|---:|---:|---:|---|:---:|
| Passenger_Count | 26.0 | 70.0 | 44.0 | −40.0 | 136.0 | 1 / 99 | None |
| Fare_Amount | 13.63 | 37.03 | 23.40 | −21.48 | 72.13 | 0.50 / 49.95 | None |
| Trip_Duration_Minutes | 53.75 | 135.0 | 81.25 | −68.13 | 256.88 | 5 / 179 | None |

**Decision:** all 1,000 records are retained. No capping, trimming or transformation is required.

---

## 12. Exporting the Cleaned Dataset

```python
data.to_excel('data_saved.xlsx', index=False)
```

The cleaned, imputed table is saved as `data_saved.xlsx` so that it can be reused for reporting, dashboards or modelling without re-running the cleaning steps.

---

## 13. Visualisation Approach & Colour Palette

All analysis charts are built in **Plotly** for interactivity (hover tooltips, zoom, toggling series). Two fixed palettes keep the colours consistent across every chart:

```python
color_map = {
    "Bus":   "#E63946",  # vivid red
    "Ferry": "#457B9D",  # steel blue
    "Train": "#2A9D8F",  # teal
    "Tram":  "#E9C46A"   # golden amber
}

type_colors = {
    "Workday": "#457B9D",  # steel blue
    "Weekend": "#E63946"   # vivid red
}
```

| Mode | Colour |
|---|---|
| Bus | ![#E63946](https://placehold.co/15x15/E63946/E63946.png) `#E63946` |
| Ferry | ![#457B9D](https://placehold.co/15x15/457B9D/457B9D.png) `#457B9D` |
| Train | ![#2A9D8F](https://placehold.co/15x15/2A9D8F/2A9D8F.png) `#2A9D8F` |
| Tram | ![#E9C46A](https://placehold.co/15x15/E9C46A/E9C46A.png) `#E9C46A` |

> **Note on GitHub rendering:** GitHub does not render interactive Plotly output inside notebooks. The static PNGs in `images/` are what readers see here. To export them, install `kaleido` and call `fig.write_image("images/<name>.png", scale=2)` after each `fig.show()`.

---

## 14. Univariate Analysis

*Examining individual variables in isolation: distributions, shapes and spread.*

### 14.1 Distribution of Fare Amounts (Histogram & KDE)

```python
fig = ff.create_distplot([data['Fare_Amount'].dropna()], ['Fare Amount'],
                         bin_size=2, show_rug=False, curve_type='kde')
```

#### Chart 3: Distribution of Fare Amounts (Histogram & KDE)

<img width="1516" height="491" alt="image" src="https://github.com/user-attachments/assets/3ef3b7ea-ade0-4bfb-83c8-d98d00faa2e0" />


**💡 Insight:** fares spread fairly evenly from £0.50 to £49.95 (mean £25.36, median £25.45), with no dominant price point. This points to **fixed fare bands per route** rather than dynamic or distance-based pricing.

### 14.2 Distribution of Mode of Transport (Donut Chart)

```python
transport_counts = data['Mode_of_Transport'].value_counts().reset_index()
fig_donut = px.pie(transport_counts, values='Count', names='Mode_of_Transport',
                   hole=0.4, color='Mode_of_Transport', color_discrete_map=color_map)
```

#### Chart 4: Distribution of Mode of Transport

<img width="1520" height="492" alt="image" src="https://github.com/user-attachments/assets/736a2587-9401-4ad2-9367-a617e14f47ba" />


| Mode | Trips | Share |
|---|---:|---:|
| Bus | 332 | 33.2% |
| Ferry | 287 | 28.7% |
| Train | 243 | 24.3% |
| Tram | 138 | 13.8% |

**💡 Insight:** Bus carries the largest share of trips, followed by Ferry and Train. **Tram trails at 13.8%**, which raises the question of whether route coverage, capacity or passenger preference is holding it back.

### 14.3 Distribution of Passenger Counts (Histogram)

```python
fig_passengers = px.histogram(data, x='Passenger_Count', nbins=30,
                              color_discrete_sequence=['#457B9D'])
```

#### Chart 5: Distribution of Passenger Counts (Histogram)

<img width="1517" height="487" alt="image" src="https://github.com/user-attachments/assets/47c817ea-668b-4885-8049-c55d852d822e" />

**💡 Insight:** passenger counts are spread evenly across the full 1 to 99 range (mean 49, median 48), so **no single load level dominates**. Trips are as likely to run light as they are to run full.

---

## 15. Bivariate Analysis

*Exploring relationships between pairs of variables: trends, correlations and patterns.*

### 15.1 Transit Demand Across the Week (Bar Chart)

```python
day_count = data.groupby('Day_of_Week').size().reset_index(name='Trip_Count')
day_count['Day_Type'] = day_count['Day_of_Week'].apply(
    lambda d: 'Workday' if d in ['Monday','Tuesday','Wednesday','Thursday','Friday'] else 'Weekend')
```

#### Chart 6: Transit Demand Across the Week (Workday vs Weekend)

<img width="1517" height="481" alt="image" src="https://github.com/user-attachments/assets/51caa633-292e-4387-b9b4-b7aea2c2b641" />

| Day | Trips | Type |
|---|---:|---|
| Sunday | 167 | Weekend |
| Tuesday | 147 | Workday |
| Saturday | 146 | Weekend |
| Monday | 142 | Workday |
| Friday | 142 | Workday |
| Wednesday | 138 | Workday |
| Thursday | 118 | Workday |

**💡 Insight:** **Sunday is the busiest day** (167 trips) and **Thursday the quietest** (118). Saturday (146) sits just below the weekday peak on Tuesday (147). Weekend demand is at least as strong as weekday demand, which matters for staffing and fleet scheduling.

### 15.2 Fare Amount across Trip Duration (Density Heatmap)

```python
fig = px.density_heatmap(data, x='Trip_Duration_Minutes', y='Fare_Amount',
                         nbinsx=20, nbinsy=20, color_continuous_scale='Blugrn')
```

#### Chart 7: Fare Amount Distribution across Trip Duration

<img width="1376" height="617" alt="image" src="https://github.com/user-attachments/assets/4cd5a239-f98c-4735-8e31-07e4886e4c20" />

**💡 Insight:** trips are scattered evenly across the grid with no diagonal band, and the correlation between fare and duration is effectively zero (**r ≈ −0.05**). **Longer trips do not cost more**, which suggests pricing is set by route rather than by time or distance.

### 15.3 Fare Amount across Modes of Transport (Boxplot)

```python
fig_box_v = px.box(data, x='Mode_of_Transport', y='Fare_Amount',
                   color='Mode_of_Transport', color_discrete_map=color_map,
                   category_orders={'Mode_of_Transport': ['Train', 'Bus', 'Tram', 'Ferry']},
                   points='outliers')
```

#### Chart 8: Fare Amount Distribution across Modes of Transport

<img width="587" height="467" alt="image" src="https://github.com/user-attachments/assets/8ba21723-c30b-40d8-8b40-b926f10249ff" />

| Mode | Median Fare | Min | Max |
|---|---:|---:|---:|
| Train | £26.61 | £1.10 | £49.95 |
| Bus | £26.31 | £0.51 | £49.88 |
| Tram | £25.75 | £0.72 | £49.57 |
| Ferry | £23.17 | £0.50 | £49.86 |

**💡 Insight:** median fares are close for Train, Bus and Tram, with **Ferry the cheapest** at the median. Every mode spans almost the full £0.50 to £50 range, so pricing looks **largely mode-neutral**.

### 15.4 Trip Volumes Across Stations (Origin-Destination Heatmap)

```python
route_summary = data.groupby(['Departure_Station', 'Arrival_Station']).size().reset_index(name='Trip_Volume')
heatmap_matrix = route_summary.pivot_table(index='Arrival_Station', columns='Departure_Station',
                                           values='Trip_Volume', aggfunc='sum', fill_value=0)
```

#### Chart 9: Trip Volumes Across Stations

<img width="772" height="470" alt="image" src="https://github.com/user-attachments/assets/cde05b3e-1bee-4c7f-94e9-ad401e45a76f" />

**💡 Insight:**
- **All 36 station pairs are served**, so there are no unused routes.
- **Central is the busiest origin** (208 departures) and **Airport the busiest destination** (213 arrivals). The single busiest route is North Station → Airport (44 trips).
- Routes **into North Station are the thinnest**, with South Point → North Station the weakest at just 8 trips, followed by Airport → North Station at 13.

---

## 16. Multivariate Analysis

*Combining three or more variables to surface complex operational patterns.*

### 16.1 Total Revenue by Departure Station & Transport Mode (Stacked Clustered Bar Chart)

```python
data['Revenue'] = data['Fare_Amount'] * data['Passenger_Count']
multivariate_revenue = (data.groupby(['Departure_Station', 'Mode_of_Transport'])['Revenue']
                            .sum().reset_index(name='Total_Revenue'))
```

#### Chart 10: Total Revenue by Departure Station and Transport Mode

<img width="1372" height="652" alt="image" src="https://github.com/user-attachments/assets/8fecacc6-3adc-41af-9756-19bd1ffba237" />

| Departure Station | Bus | Ferry | Train | Tram | **Total** |
|---|---:|---:|---:|---:|---:|
| Central | £103.3k | £71.2k | £68.7k | £49.9k | **£293.0k** |
| Airport | £62.3k | £64.2k | £53.2k | £23.0k | **£202.6k** |
| North Station | £63.0k | £48.4k | £57.5k | £31.1k | **£200.0k** |
| Downtown | £72.6k | £53.1k | £46.9k | £23.0k | **£195.6k** |
| West End | £54.0k | £63.0k | £49.3k | £28.8k | **£195.0k** |
| South Point | £57.3k | £59.5k | £24.6k | £20.9k | **£162.2k** |
| **Total** | **£412.4k** | **£359.3k** | **£300.2k** | **£176.6k** | **≈ £1.25m** |

**💡 Insight:** **Central is the top revenue station for every mode**, and Bus from Central is the single largest segment (£103k). Bus leads overall revenue as the most-used mode. Airport, North Station, Downtown and West End form a close second tier, while South Point trails, mainly because of weak Train and Tram revenue.

### 16.2 Average Fare by Transport Mode & Day of the Week (Heatmap)

```python
avg_fare_data = data.groupby(['Mode_of_Transport', 'Day_of_Week'])['Fare_Amount'].mean().reset_index()
heatmap_pivot = avg_fare_data.pivot(index='Mode_of_Transport', columns='Day_of_Week', values='Fare_Amount')
```

#### Chart 11: Average Fare Amount by Transport Mode and Day of the Week

<img width="1371" height="722" alt="image" src="https://github.com/user-attachments/assets/dc9120f8-74f7-49c9-89f3-71e287008e96" />

| Mode | Mon | Tue | Wed | **Thu** | Fri | Sat | Sun |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bus | £27.5 | £26.3 | £22.2 | **£28.4** | £25.9 | £26.0 | £23.7 |
| Ferry | £26.3 | £23.5 | £25.6 | **£28.1** | £22.6 | £22.3 | £23.0 |
| Train | £25.0 | £23.9 | £27.8 | **£28.1** | £27.1 | £24.7 | £27.0 |
| Tram | £25.1 | £23.5 | £24.4 | **£30.4** | £24.6 | £24.4 | £27.2 |

**💡 Insight:** **Thursday has the highest average fare for every mode** (£28.1 to £30.4), even though it is the quietest day for trips (118). This could reflect demand-based pricing on high-commuter days, or an artefact worth investigating with the pricing team.

### 16.3 Trip Count & Total Passengers by Transport Mode & Day of the Week (Dual-Metric Heatmap)

```python
aggregated_data = data.groupby(['Mode_of_Transport', 'Day_of_Week']).agg(
    Total_Passengers=('Passenger_Count', 'sum'),
    Trip_Count=('Trip_ID', 'count')).reset_index()
```

Each cell shows **trip count** with **total passengers** in brackets. Colour intensity follows total passengers, and a second colour bar shows the trip-count scale.

#### Chart 12: Trip Count & Total Passenger Count by Transport Mode and Day of the Week

<img width="1512" height="567" alt="image" src="https://github.com/user-attachments/assets/85f72f0c-016d-4f52-8df4-0e59f1d7a26f" />

| Mode | Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|---|---|---|---|---|---|---|---|
| Bus | 54 (2,609) | 47 (2,470) | 47 (2,229) | 36 (1,612) | 50 (2,318) | 46 (2,350) | **52 (2,768)** |
| Ferry | 35 (1,821) | 47 (2,611) | 37 (1,774) | 38 (2,173) | 40 (1,618) | 45 (2,443) | 45 (1,953) |
| Train | 26 (1,365) | 36 (1,680) | 33 (1,727) | 35 (1,667) | 33 (1,355) | 37 (1,830) | 43 (1,517) |
| Tram | 27 (1,415) | 17 (844) | 21 (1,016) | **9 (465)** | 19 (1,133) | 18 (858) | 27 (1,341) |

**💡 Insight:** Bus is busiest on **Monday by trips (54)** and **Sunday by passengers (2,768, the highest of any cell)**. Ferry overtakes Bus on Thursday. **Tram on Thursday is the quietest cell** (9 trips, 465 passengers), and Tram is the lightest mode on most days. This supports both the weekend-capacity and tram-coverage recommendations.

---

## 17. Key Insights Summary

| # | Theme | Finding |
|:---:|---|---|
| 1 | **Pricing** | Fares are spread evenly (£0.50 to £49.95), unrelated to trip duration (r ≈ −0.05) and broadly similar across modes, so pricing appears route-fixed and mode-neutral. |
| 2 | **Mode share** | Bus leads with 33.2% of trips; Tram trails at 13.8%. |
| 3 | **Weekly demand** | Sunday is the peak day (167 trips) and Thursday the trough (118). |
| 4 | **Thursday fares** | Thursday has the highest average fare for every mode despite the lowest volume. |
| 5 | **Network** | All 36 station pairs are served. Central is the main origin hub; Airport is the main destination; routes into North Station are thinnest. |
| 6 | **Revenue** | Total revenue is about £1.25m. Central generates the most revenue for every mode, and Bus is the top-earning mode (£412k). |
| 7 | **Load** | Passenger counts are spread evenly from 1 to 99 per trip, with no dominant load level. |
| 8 | **Data quality** | All missing values and naming inconsistencies were resolved; no outliers required treatment. |

---

## 18. Conclusions & Recommendations

| Recommendation | Evidence | Suggested action |
|---|---|---|
| 🔴 **Pricing Strategy** | Fares are route-fixed and mode-neutral, with no link to trip duration | Explore dynamic or distance-based pricing to capture more revenue on longer routes |
| 🔵 **Weekend Capacity** | Sunday records the highest trip volume of the week (167 trips) and the highest Bus passenger total | Add Bus and Tram capacity on Sundays to protect the passenger experience |
| 🟢 **Tram Network Expansion** | Tram holds only 13.8% of trips and is the lightest mode on most days | Run a route-coverage analysis before making capacity decisions |
| 🟡 **Low-Volume Route Opportunities** | Every station pair is served, but some are thin (South Point → North Station: 8 trips; Airport → North Station: 13) | Review frequency, timing and promotion on the weakest routes, especially into North Station |
| 🔷 **Data Quality Foundation** | Casing, whitespace and missing-value issues all had to be fixed before analysis | Introduce a data governance framework (validation at entry, controlled vocabularies for modes and stations) to prevent recurrence |

The most operationally urgent actions are **weekend capacity planning** and a **review of tram network coverage**.

---

## 19. Limitations

- **Median imputation reduces variance.** Filling 10% of three columns with group medians slightly understates the true spread of those variables.
- **Revenue is an estimate.** Revenue is calculated as `Fare_Amount × Passenger_Count`, which assumes every passenger on a trip paid the recorded fare (no concessions, passes or discounts).
- **Hourly rounding.** `Departure_Time` is rounded to the nearest hour, which is ideal for time-of-day grouping but loses minute-level precision. `Arrival_Date` is calculated from the unrounded time to avoid this.
- **Limited time window.** The data covers 42 trip dates, so seasonal patterns cannot be assessed.
- **Descriptive, not causal.** EDA reveals patterns and associations; it does not prove why they occur. Recommendations should be validated with operational data and stakeholders.

---

## 20. Future Work

- **Time-of-day analysis:** use the cleaned hourly `Departure_Time` to identify peak hours by mode and station.
- **Correlation matrix:** add an explicit correlation heatmap of all numeric features to document the near-zero relationships formally.
- **Route-level profitability:** combine trip volume, load and revenue per route to rank routes by efficiency.
- **Pricing experiments:** model the revenue impact of distance-based or demand-based fares.
- **Investigate Thursday pricing:** confirm with the pricing team whether higher Thursday fares are policy or a data artefact.
- **Interactive dashboard:** publish the key charts in Power BI, Tableau or Streamlit for ongoing monitoring.
- **Automated data-quality checks:** codify the cleaning rules as validation tests in the ingestion pipeline.

---

## 21. How to Run This Project

**1. Clone the repository**

```bash
git clone https://github.com/<your-username>/MetroMove-Public-Transport-EDA.git
cd MetroMove-Public-Transport-EDA
```

**2. Create an environment and install dependencies**

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate

pip install -r requirements.txt
```

Suggested `requirements.txt`:

```text
numpy
pandas
openpyxl
missingno
matplotlib
seaborn
plotly
kaleido
jupyter
```

**3. Launch the notebook**

```bash
jupyter notebook public_transport_script.ipynb
```

**4. Run all cells**

Use **Kernel → Restart & Run All**. The notebook will load `Public_Transport_Trips_EDA.xlsx`, clean and impute the data, save `data_saved.xlsx`, and render every chart.

**5. (Optional) Export charts for this README**

```python
fig.write_image("images/03_fare_distribution.png", scale=2)
```

---

## 22. Author & Contact

**Samuel Babajide**
Data Scientist | Data Quality & Governance | Applied Analytics

- 💼 LinkedIn: [Add your LinkedIn URL]
- 🐙 GitHub: [Add your GitHub profile URL]
- 🌐 Portfolio: [Add your portfolio URL]

---

<p align="center"><i>Data cleaned · Patterns discovered · Insights delivered</i></p>
