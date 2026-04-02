# Predicting Bridge Structural Health and Failure Risk
### Supervised Machine Learning | National Bridge Inventory 2023

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-orange?style=flat&logo=scikit-learn)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-yellow?style=flat&logo=googlecolab)
![Records](https://img.shields.io/badge/Records-621%2C581-green?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)

---

## Table of Contents

1. [About This Project](#about-this-project)
2. [About the Organisation](#about-the-organisation)
3. [About the Dataset](#about-the-dataset)
4. [All 123 Columns](#all-123-columns-in-the-raw-dataset)
5. [Columns Used](#columns-used-in-this-project)
6. [Target Variable](#target-variable)
7. [Project Scope and Goals](#project-scope-and-goals)
8. [Results and Findings](#results-and-findings)
9. [How to Run This Project](#how-to-run-this-project)
10. [Tools Used](#tools-used)
11. [About Me](#about-me)
12. [References](#references)

---

## About This Project

Every day, millions of people drive over bridges without knowing whether the
structure beneath them is in good condition or quietly getting worse. The United
States inspects over 620,000 public bridges every year and records each inspection
in a federal database. That data exists — but it has not been widely used to
forecast which bridges are heading toward poor condition before the next inspector
arrives.

This project asks: can a machine learning model look at a bridge's age, physical
size, traffic load, and maintenance history — and predict how bad its structural
condition is likely to be?

To answer that, I built a supervised machine learning pipeline using the 2023
National Bridge Inventory. The pipeline covers the complete workflow: loading and
cleaning 621,581 inspection records, exploring patterns in the data, engineering
new features, training and comparing six regression models, and producing a ranked
list of bridges predicted to be approaching structural failure — all without using
any live inspection data as a model input.

This is my first supervised machine learning project, built as part of a portfolio
that applies data science to real engineering problems across four sectors:
infrastructure, healthcare, oil and gas, and automotive systems.

---

## About the Organisation

The **Federal Highway Administration (FHWA)** is the US government agency
responsible for the safety of the country's highway network. It runs the
**National Bridge Inspection Program**, which requires every public bridge in the
US to be physically inspected at least once every two years by a certified engineer.

Each inspection produces a detailed record submitted to the federal government.
These records form the National Bridge Inventory — one of the most comprehensive
infrastructure datasets available anywhere in the world. It is updated annually
and released to the public at no cost.

| | |
|---|---|
| FHWA Website | [https://www.fhwa.dot.gov](https://www.fhwa.dot.gov) |
| Bridge Programme | [https://www.fhwa.dot.gov/bridge](https://www.fhwa.dot.gov/bridge) |
| NBI Programme Overview | [https://www.fhwa.dot.gov/bridge/nbi.cfm](https://www.fhwa.dot.gov/bridge/nbi.cfm) |

---

## About the Dataset

| | |
|---|---|
| **Name** | National Bridge Inventory (NBI) |
| **Year** | 2023 |
| **Published by** | Federal Highway Administration, US Department of Transportation |
| **File format** | Comma-separated text file (.txt) with single-quote text qualifier |
| **Total records** | 621,581 bridge inspection records |
| **Total columns** | 123 |
| **Coverage** | All 50 US states, Washington D.C., federal agencies, tribal governments, and US territories |
| **Update frequency** | Annually |

> **This dataset is free and publicly available.** The NBI is released as open
> government data under US federal open data policy. Anyone can download and use
> it at no cost.
>
> **Download it here:**
> [https://www.fhwa.dot.gov/bridge/nbi/ascii2023.cfm](https://www.fhwa.dot.gov/bridge/nbi/ascii2023.cfm)

---

## All 123 Columns in the Raw Dataset

The NBI file contains 123 columns covering a bridge's identity, location, physical
dimensions, structural components, condition ratings, load capacity, traffic data,
and inspection history. The full list is provided here so anyone reading this
project can see exactly what the raw data contains.

<details>
<summary>Click to expand — all 123 columns</summary>

| # | Column Name | Description |
|---|-------------|-------------|
| 0 | `STATE_CODE_001` | Numeric FIPS code identifying the US state |
| 1 | `STRUCTURE_NUMBER_008` | Unique ID assigned to each bridge |
| 2 | `RECORD_TYPE_005A` | Record type indicator |
| 3 | `ROUTE_PREFIX_005B` | Route signing prefix |
| 4 | `SERVICE_LEVEL_005C` | Service level of the route |
| 5 | `ROUTE_NUMBER_005D` | Route number |
| 6 | `DIRECTION_005E` | Direction of traffic flow |
| 7 | `HIGHWAY_DISTRICT_002` | Highway district code |
| 8 | `COUNTY_CODE_003` | County code |
| 9 | `PLACE_CODE_004` | Place code |
| 10 | `FEATURES_DESC_006A` | What the bridge crosses — a river, road, railway, etc. |
| 11 | `CRITICAL_FACILITY_006B` | Whether the bridge serves a critical facility |
| 12 | `FACILITY_CARRIED_007` | The road or route the bridge carries |
| 13 | `LOCATION_009` | Location description |
| 14 | `MIN_VERT_CLR_010` | Minimum height clearance above the bridge deck |
| 15 | `KILOPOINT_011` | Position of the bridge along the route |
| 16 | `BASE_HWY_NETWORK_012` | Whether the bridge is on the base highway network |
| 17 | `LRS_INV_ROUTE_013A` | Linear referencing system route identifier |
| 18 | `SUBROUTE_NO_013B` | Sub-route number |
| 19 | `LAT_016` | Latitude coordinate |
| 20 | `LONG_017` | Longitude coordinate |
| 21 | `DETOUR_KILOS_019` | How far traffic would detour if the bridge closed |
| 22 | `TOLL_020` | Whether the bridge charges a toll |
| 23 | `MAINTENANCE_021` | Which agency is responsible for maintenance |
| 24 | `OWNER_022` | Which agency owns the bridge |
| 25 | `FUNCTIONAL_CLASS_026` | Classification of the road the bridge carries |
| 26 | `YEAR_BUILT_027` | Year the bridge was originally constructed |
| 27 | `TRAFFIC_LANES_ON_028A` | Number of traffic lanes on the bridge |
| 28 | `TRAFFIC_LANES_UND_028B` | Number of traffic lanes passing under the bridge |
| 29 | `ADT_029` | Average Daily Traffic — vehicles crossing per day |
| 30 | `YEAR_ADT_030` | Year the traffic count was recorded |
| 31 | `DESIGN_LOAD_031` | The load the bridge was originally designed to carry |
| 32 | `APPR_WIDTH_MT_032` | Width of the approach road in metres |
| 33 | `MEDIAN_CODE_033` | Type of median on the bridge |
| 34 | `DEGREES_SKEW_034` | Angle at which the bridge crosses what it spans |
| 35 | `STRUCTURE_FLARED_035` | Whether the bridge deck widens toward one end |
| 36 | `RAILINGS_036A` | Condition of the bridge railings |
| 37 | `TRANSITIONS_036B` | Condition of the approach transitions |
| 38 | `APPR_RAIL_036C` | Condition of the approach guardrail |
| 39 | `APPR_RAIL_END_036D` | Condition of the guardrail end treatments |
| 40 | `HISTORY_037` | Whether the bridge has historical significance |
| 41 | `NAVIGATION_038` | Whether the bridge has navigation clearance requirements |
| 42 | `NAV_VERT_CLR_MT_039` | Vertical clearance for water navigation in metres |
| 43 | `NAV_HORR_CLR_MT_040` | Horizontal clearance for water navigation in metres |
| 44 | `OPEN_CLOSED_POSTED_041` | Whether the bridge is open, closed, or weight-restricted |
| 45 | `SERVICE_ON_042A` | Type of traffic the bridge carries |
| 46 | `SERVICE_UND_042B` | Type of traffic passing under the bridge |
| 47 | `STRUCTURE_KIND_043A` | Material the bridge is made from |
| 48 | `STRUCTURE_TYPE_043B` | Structural design type |
| 49 | `APPR_KIND_044A` | Material of the approach spans |
| 50 | `APPR_TYPE_044B` | Design type of the approach spans |
| 51 | `MAIN_UNIT_SPANS_045` | Number of sections in the main structural unit |
| 52 | `APPR_SPANS_046` | Number of approach spans |
| 53 | `HORR_CLR_MT_047` | Minimum side clearance under the bridge in metres |
| 54 | `MAX_SPAN_LEN_MT_048` | Length of the longest single span in metres |
| 55 | `STRUCTURE_LEN_MT_049` | Total length of the bridge in metres |
| 56 | `LEFT_CURB_MT_050A` | Width of the left footpath or kerb in metres |
| 57 | `RIGHT_CURB_MT_050B` | Width of the right footpath or kerb in metres |
| 58 | `ROADWAY_WIDTH_MT_051` | Width of the driving surface in metres |
| 59 | `DECK_WIDTH_MT_052` | Full deck width from edge to edge in metres |
| 60 | `VERT_CLR_OVER_MT_053` | Minimum clearance height above the bridge |
| 61 | `VERT_CLR_UND_REF_054A` | Reference point for measuring underclearance height |
| 62 | `VERT_CLR_UND_054B` | Minimum height clearance below the bridge in metres |
| 63 | `LAT_UND_REF_055A` | Reference point for measuring side clearance below |
| 64 | `LAT_UND_MT_055B` | Minimum side clearance on the right below the bridge |
| 65 | `LEFT_LAT_UND_MT_056` | Minimum side clearance on the left below the bridge |
| 66 | `DECK_COND_058` | Condition of the bridge deck — the surface vehicles drive on (0–9) |
| 67 | `SUPERSTRUCTURE_COND_059` | Condition of the structural parts above the deck — beams, girders (0–9) |
| 68 | `SUBSTRUCTURE_COND_060` | Condition of the parts below the deck — piers and abutments (0–9) |
| 69 | `CHANNEL_COND_061` | Condition of the waterway channel and bank protection |
| 70 | `CULVERT_COND_062` | Condition rating for drainage culvert structures (0–9) |
| 71 | `OPR_RATING_METH_063` | Method used to calculate the operating load rating |
| 72 | `OPERATING_RATING_064` | Maximum load the bridge can carry under normal use |
| 73 | `INV_RATING_METH_065` | Method used to calculate the inventory load rating |
| 74 | `INVENTORY_RATING_066` | Maximum load allowed for routine daily traffic |
| 75 | `STRUCTURAL_EVAL_067` | Inspector's overall evaluation of structural adequacy |
| 76 | `DECK_GEOMETRY_EVAL_068` | Evaluation of the deck width and geometry |
| 77 | `UNDCLRENCE_EVAL_069` | Evaluation of clearance height below the bridge |
| 78 | `POSTING_EVAL_070` | Evaluation of whether the bridge should be weight-posted |
| 79 | `WATERWAY_EVAL_071` | Evaluation of how well the waterway channel flows |
| 80 | `APPR_ROAD_EVAL_072` | Evaluation of the approach road alignment |
| 81 | `WORK_PROPOSED_075A` | Type of repair or improvement work being planned |
| 82 | `WORK_DONE_BY_075B` | Who will carry out the proposed work |
| 83 | `IMP_LEN_MT_076` | Length of the planned improvement in metres |
| 84 | `DATE_OF_INSPECT_090` | Date of the most recent physical inspection |
| 85 | `INSPECT_FREQ_MONTHS_091` | How often the bridge is inspected, in months |
| 86 | `FRACTURE_092A` | Whether fracture-critical inspection is required |
| 87 | `UNDWATER_LOOK_SEE_092B` | Whether underwater inspection is required |
| 88 | `SPEC_INSPECT_092C` | Whether a special inspection is required |
| 89 | `FRACTURE_LAST_DATE_093A` | Date of the last fracture-critical inspection |
| 90 | `UNDWATER_LAST_DATE_093B` | Date of the last underwater inspection |
| 91 | `SPEC_LAST_DATE_093C` | Date of the last special inspection |
| 92 | `BRIDGE_IMP_COST_094` | Estimated cost of bridge improvement work |
| 93 | `ROADWAY_IMP_COST_095` | Estimated cost of roadway improvement work |
| 94 | `TOTAL_IMP_COST_096` | Total estimated project cost |
| 95 | `YEAR_OF_IMP_097` | Year the improvement is planned |
| 96 | `OTHER_STATE_CODE_098A` | State code for bridges shared across state borders |
| 97 | `OTHER_STATE_PCNT_098B` | Each state's share of responsibility for a border bridge |
| 98 | `OTHR_STATE_STRUC_NO_099` | The other state's structure number for the same bridge |
| 99 | `STRAHNET_HIGHWAY_100` | Whether the bridge is on a strategic military highway |
| 100 | `PARALLEL_STRUCTURE_101` | Whether a parallel bridge structure exists nearby |
| 101 | `TRAFFIC_DIRECTION_102` | Direction of traffic flow |
| 102 | `TEMP_STRUCTURE_103` | Whether the bridge is a temporary structure |
| 103 | `HIGHWAY_SYSTEM_104` | Whether the bridge is on the national highway system |
| 104 | `FEDERAL_LANDS_105` | Whether the bridge is on federal land |
| 105 | `YEAR_RECONSTRUCTED_106` | Year of the most recent major reconstruction |
| 106 | `DECK_STRUCTURE_TYPE_107` | How the deck is constructed |
| 107 | `SURFACE_TYPE_108A` | Type of wearing surface on the deck |
| 108 | `MEMBRANE_TYPE_108B` | Type of waterproofing membrane under the surface |
| 109 | `DECK_PROTECTION_108C` | How the deck is protected from corrosion |
| 110 | `PERCENT_ADT_TRUCK_109` | Percentage of daily traffic that are trucks |
| 111 | `NATIONAL_NETWORK_110` | Whether the bridge is on the national truck network |
| 112 | `PIER_PROTECTION_111` | Type of pier protection against collision or scour |
| 113 | `BRIDGE_LEN_IND_112` | Bridge length classification indicator |
| 114 | `SCOUR_CRITICAL_113` | Whether the bridge foundations are vulnerable to erosion |
| 115 | `FUTURE_ADT_114` | Projected future average daily traffic |
| 116 | `YEAR_OF_FUTURE_ADT_115` | Year the projected traffic figure applies to |
| 117 | `MIN_NAV_CLR_MT_116` | Minimum navigation clearance in metres |
| 118 | `FED_AGENCY` | Federal agency code |
| 119 | `SUBMITTED_BY` | The state or agency that submitted the record |
| 120 | `BRIDGE_CONDITION` | Overall condition category — Good, Fair or Poor |
| 121 | `LOWEST_RATING` | The lowest condition score across all inspected components (0–9) |
| 122 | `DECK_AREA` | Total deck surface area in square metres |

</details>

---

## Columns Used in This Project

16 of the 123 columns were selected. The selection was guided by a civil engineering
perspective: what would a maintenance planner know about a bridge before dispatching
an inspection team? The answer is things like its age, physical dimensions, the
load it was built to carry, and how much traffic it handles — not the inspection
scores themselves.

| Column | What it is |
|--------|------------|
| `STATE_CODE_001` | Which US state the bridge is in |
| `STRUCTURE_NUMBER_008` | Unique bridge ID |
| `YEAR_BUILT_027` | Year originally built |
| `ADT_029` | Average number of vehicles crossing per day |
| `MAIN_UNIT_SPANS_045` | How many sections make up the main structural unit |
| `STRUCTURE_LEN_MT_049` | Total length in metres |
| `DECK_COND_058` | Condition score of the bridge deck — *loaded for analysis only, not used in models* |
| `SUPERSTRUCTURE_COND_059` | Condition score of the beams and girders above the deck — *same as above* |
| `SUBSTRUCTURE_COND_060` | Condition score of the piers and abutments below the deck — *same as above* |
| `CULVERT_COND_062` | Used only to separate culverts from highway bridges during cleaning |
| `OPERATING_RATING_064` | Maximum safe load the bridge can carry |
| `INVENTORY_RATING_066` | Maximum load allowed for routine daily traffic |
| `YEAR_RECONSTRUCTED_106` | Year of the most recent major rebuild |
| `PERCENT_ADT_TRUCK_109` | What percentage of daily traffic are trucks |
| `BRIDGE_CONDITION` | Government overall label — Good, Fair, or Poor |
| `LOWEST_RATING` ⭐ | **The target — the lowest condition score across all bridge components (0–9)** |

> **Why were the deck, superstructure, and substructure scores excluded from
> model training?**
>
> `LOWEST_RATING` is literally the lowest of those three scores. If those columns
> were fed into the model as inputs, it would be like handing a student the answer
> sheet before the exam — the model would score perfectly but would not have learned
> anything real. In machine learning, this is called **data leakage**: when
> information that directly reveals the answer is accidentally included as a feature.
> Those three columns were kept for the exploratory analysis stage only and were
> never passed to any model.

---

## Target Variable

**`LOWEST_RATING`** is the condition score of the single worst-rated structural
component on each bridge. A bridge can have a perfect deck and solid foundations,
but if its superstructure is deteriorating, that lowest score defines its overall
safety status. The FHWA uses this exact logic in its official bridge classification
system.

| Score | Meaning | FHWA Category |
|-------|---------|---------------|
| 9 | Excellent | Good |
| 8 | Very Good | Good |
| 7 | Good | Good |
| 6 | Satisfactory | Fair |
| 5 | Fair | Fair |
| 4 | Poor | Poor |
| 3 | Serious | Poor |
| 2 | Critical | Poor |
| 1 | Imminent Failure | Poor |
| 0 | Failed | Poor |

Scores of **4 and below are classified as structurally deficient** by the FHWA.
This is a formal designation meaning the bridge has at least one component in poor
enough condition to require close attention. Being structurally deficient does not
automatically mean a bridge is unsafe to cross — but it does mean it needs
maintenance intervention.

---

## Project Scope and Goals

**Primary goal:** Build a model that predicts `LOWEST_RATING` using only the
physical and operational features a planner would have available before an
inspection — and produce a ranked list of bridges predicted to be at or below the
structural deficiency threshold.

**Learning goal:** Work through six regression models in order of complexity,
understand what each one adds over the previous, and compare them using three
standard evaluation metrics.

### Steps Followed

```
1. Data Loading          Load 16 of 123 NBI columns from Google Drive
2. Data Cleaning         Fix data types, remove bad entries, fill missing values
3. Structure Separation  Split highway bridges from culverts before any analysis
4. Exploration (EDA)     Understand distributions, age trends, traffic effects, correlations
5. Feature Engineering   Create four new calculated columns from existing ones
6. Model Training        Train six regression models, increasing in complexity
7. Evaluation            Compare all six models on R², MAE and RMSE
8. At-Risk Report        Rank bridges predicted at Poor or worse condition, by state
```

### The Four Engineered Features

Rather than using the raw columns directly, four new features were created to give
the models more useful signals:

| Feature | How It Is Calculated | Why It Was Created |
|---------|---------------------|---------------------|
| `BRIDGE_AGE` | 2023 − year built | Age in years is more meaningful to a model than a calendar year like "1974" |
| `YEARS_SINCE_RENO` | 2023 − year reconstructed (or bridge age if never rebuilt) | Two 60-year-old bridges are very different if one was rebuilt 5 years ago |
| `LOAD_RATIO` | Inventory rating ÷ operating rating | How close is the permitted daily load to the maximum structural capacity? |
| `TRAFFIC_AGE` | Daily traffic × bridge age | Captures the compounded stress of high traffic on an old bridge — neither alone tells the full story |

### The Six Models

| # | Model | What It Does Differently |
|---|-------|--------------------------|
| 1 | Simple Linear Regression | Uses bridge age only — sets the performance baseline |
| 2 | Multiple Linear Regression | Uses all 10 features — the full straight-line model |
| 3 | Polynomial Regression (degree 2) | Creates squared versions of features to fit curved relationships |
| 4 | Ridge Regression | Applies a penalty to prevent over-reliance on any single feature |
| 5 | Lasso Regression | Can reduce the weight of unimportant features all the way to zero |
| 6 | ElasticNet | Combines the penalties of Ridge and Lasso in a single model |

---

## Results and Findings

### 1. How Bridge Conditions Are Distributed

![Condition Distribution](visuals/target_distribution.png)

The left chart shows how many bridges have each condition score from 0 to 9. The
tallest bars sit at scores 5, 6, and 7 — meaning most US highway bridges are in
the Fair to Good range. Scores 8 and 9 (near-perfect condition) are relatively
rare, as are scores 0 to 2 (critically deteriorated — those bridges are typically
already closed or under emergency repair).

The right chart groups those scores into the three official FHWA categories. Of the
474,880 highway bridges in the dataset:

- **51.0%** are in **Fair** condition (242,166 bridges)
- **40.8%** are in **Good** condition (193,638 bridges)
- **8.2%** are in **Poor** condition (39,076 bridges)

The Fair majority is worth noting. A Fair bridge is not immediately dangerous, but
it has components that are showing wear. Without proactive maintenance, a large
portion of that 51% will slide into the Poor category in coming years.

---

### 2. Does Age Affect Condition?

![Age vs Condition](visuals/age_vs_condition.png)

Yes — clearly. The scatter plot on the left shows 10,000 randomly sampled bridges.
Each dot is one bridge; the x-axis is how old it is, the y-axis is its condition
score. Older bridges (right side) have more dots at lower scores. Newer bridges
(left side) are clustered near scores 7 and 8.

The line chart on the right is cleaner: it groups bridges by the decade they were
built and shows the average condition score per decade. Bridges built before 1900
average around 5.0 (Fair). Bridges built in the 1990s and 2000s average close to
7.5 (Good to Very Good). The red dashed line marks the Poor threshold at 4 — pre-
1900 bridges are approaching it on average.

This confirms that age is the single strongest physical predictor of condition —
and it is the feature the model learns the most from.

---

### 3. Does Traffic Volume Affect Condition?

![Traffic vs Condition](visuals/traffic_vs_condition.png)

The relationship here is less straightforward than expected. The box plots on the
left group bridges into four traffic bands and show the spread of condition scores
in each band. The median (middle line in each box) is similar across all four
categories — around 6 to 7 in each group.

Bridges carrying very high daily traffic actually score slightly higher on average
than low-traffic bridges. This is likely because major crossings on busy routes
receive more maintenance funding, more frequent inspections, and get rebuilt more
often than small rural bridges.

The scatter plot on the right shows truck percentage against condition score. No
strong pattern is visible — bridges with high truck traffic are not consistently
worse rated than those with low truck traffic when looked at on this axis alone.
The combined `TRAFFIC_AGE` feature (daily traffic multiplied by age) proved more
useful to the model than either traffic variable on its own.

---

### 4. What Correlates Most With Condition?

![Correlation Heatmap](visuals/correlation_heatmap.png)

The heatmap shows the statistical relationship between every pair of columns.
Each cell contains a number between −1 and +1. Green means the two columns tend to
rise and fall together (positive correlation). Red means when one goes up, the
other tends to go down (negative). Yellow means no clear relationship.

For the target column (`LOWEST_RATING`), the key findings are:

- The three component scores (deck, superstructure, substructure) have very high
  correlations of 0.79–0.83 with the target. This was expected and confirms the
  data leakage risk — those scores cannot be used as model inputs.
- `YEAR_BUILT_027` shows +0.54 — newer bridges score better. Confirmed.
- `INVENTORY_RATING_066` and `OPERATING_RATING_064` show +0.36 and +0.33 —
  higher-capacity bridges tend to be in better condition, reflecting that they are
  typically newer and better maintained.
- `ADT_029` (daily traffic) shows only +0.02 — essentially no linear relationship
  on its own, consistent with the traffic charts above.

The heatmap also shows that `OPERATING_RATING_064` and `INVENTORY_RATING_066`
are 0.89 correlated with each other. When two features are this closely related,
a standard linear model can behave unpredictably — Ridge regularisation was applied
specifically to handle this.

---

### 5. Does Reconstruction Help?

![Renovation Effect](visuals/renovation_effect.png)

Yes, measurably. The three charts examine the `YEARS_SINCE_RENO` feature from
different angles.

The left chart shows the distribution of years since last reconstruction across all
bridges. Most bridges have not been rebuilt recently — the distribution has a long
tail. The red dashed line shows the average of about 39 years.

The middle chart shows how average condition score changes as time since
reconstruction increases. Bridges reconstructed within the last 10 years average
close to 7.5. Bridges that have not been touched in over 75 years average closer
to 5.5. The colour coding (green/orange/red) shows this cross the Good, Fair, and
Poor thresholds.

The right chart is the most informative. For bridges of the same age, it compares
those that have been reconstructed (green) against those that have never been
rebuilt (red). In every age group from 20 years old to over 100, reconstructed
bridges score higher. The gap is largest in the 41–80 year age bands — where
rebuilding a bridge appears to add roughly half a point to its average condition
score. On a 0–9 scale, half a point is the difference between a Fair and a Poor
rating for many bridges.

---

### 6. How Did the Models Compare?

![Model Comparison](visuals/model_comparison.png)

| Model | R² | MAE | RMSE |
|-------|----|-----|------|
| Simple Linear Regression | 0.30 | 0.77 | 1.01 |
| Multiple Linear Regression | 0.38 | 0.74 | 0.95 |
| **Polynomial Regression (deg 2)** | **0.42** | **0.72** | **0.91** |
| Ridge Regression | 0.38 | 0.74 | 0.95 |
| Lasso Regression | 0.37 | 0.74 | 0.95 |
| ElasticNet | 0.37 | 0.74 | 0.95 |

**Reading the metrics:**

- **R²** (R-squared): Measures how much of the variation in condition scores the
  model explains. 0 means the model is no better than guessing the average for
  every bridge. 1 would mean perfect predictions. Higher is better.
- **MAE** (Mean Absolute Error): The average gap between the model's prediction and
  the actual score, measured in condition score points. An MAE of 0.72 means
  predictions are off by less than three-quarters of a point on average. Lower is better.
- **RMSE** (Root Mean Squared Error): Similar to MAE but penalises larger errors
  more heavily. A bridge predicted at 6 but actually scoring 3 hurts RMSE far more
  than one predicted at 6 and actually scoring 5. Lower is better.

**Polynomial Regression was the best model across all three metrics.** It accounts
for the fact that bridge deterioration is not a perfectly straight-line process —
condition may hold steady for many years and then accelerate as a bridge gets older.
Squared terms (age², traffic²) let the model fit that kind of curve.

**An R² of 0.42 is the honest and expected result** for this feature set — not a
disappointing one. The remaining 58% of variation is driven by factors the model
was never given: the quality of original construction materials, local weather and
road salt exposure, specific maintenance decisions made at the state level, and the
judgement of the individual inspector. A much higher R² using only these features
would suggest data leakage rather than a genuine improvement.

**Why did Ridge, Lasso, and ElasticNet match Multiple Linear Regression so
closely?** Regularisation is most beneficial when a model is overfitting — learning
the quirks of the training data rather than the real pattern. With 380,000 training
rows, there is enough data that the models converge to similar solutions regardless
of penalty. These models would show more differentiation on a smaller dataset.

---

### 7. Which States Have the Most At-Risk Bridges?

![At-Risk by State](visuals/at_risk_by_state.png)

The at-risk report applies the Multiple Linear Regression model to all 474,880
highway bridges and flags those predicted to score 4 or below — the FHWA's
structural deficiency threshold.

**4,329 bridges were flagged as at-risk — 0.9% of the national highway bridge
inventory.**

The states with the highest concentrations are Illinois, Pennsylvania, Louisiana,
New York, and Indiana. This is consistent with the known geography of the US
bridge problem: the northeastern and midwestern states have the oldest bridge stock
in the country, combined with harsh winters where freeze-thaw cycles and road salt
accelerate structural wear. Rural networks in these states also tend to receive less
maintenance funding than bridges on major urban corridors.

Pennsylvania's appearance near the top of the individual bridge rankings is partly
explained by several bridges dating back to the 1800s still in active service.
Illinois bridges from 1968–2003 appear in the highest-risk group due to high
`LOAD_RATIO` values — a signal that their permitted routine load is a large
fraction of their structural maximum, which the model interprets as a condition risk.

---

## How to Run This Project

1. **Download the 2023 NBI dataset** from:
   [https://www.fhwa.dot.gov/bridge/nbi/ascii2023.cfm](https://www.fhwa.dot.gov/bridge/nbi/ascii2023.cfm)
   — select the national file (`nbi_2023.txt`). The file is approximately 200MB.

2. **Upload it to your Google Drive** at the path:
   `/MyDrive/nbi_2023.txt`
   *(or update the `FILE_PATH` variable at the top of Cell 2 in the notebook)*

3. **Open the notebook in Google Colab:**

   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

4. **Run all cells from top to bottom.** The full pipeline takes approximately
   3–5 minutes on a standard Colab CPU session. The most time-consuming step is
   the initial file load from Google Drive (~30–90 seconds depending on connection).

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Python 3.10 | Core programming language |
| Pandas | Data loading, cleaning and manipulation |
| NumPy | Numerical calculations and array operations |
| Matplotlib | Base charting library |
| Seaborn | Statistical chart styling (used for the correlation heatmap) |
| Scikit-Learn | All machine learning models, preprocessing, and evaluation metrics |
| Google Colab | Cloud notebook environment — no local installation required |
| Google Drive | Storage for the 200MB+ raw NBI file |

---

## About Me

My name is Joseph Terem Monjok, and I am a Graduate Civil Engineer with over a year of practical field experience in the construction and infrastructure sector. My academic foundation was built at the Federal University of Technology, Minna, where I earned my B.Eng with a CGPA of 4.15/5.0. Professionally, I am proficient in industry-standard engineering software, utilizing ProtaStructure for complex structural analysis and Autodesk Civil 3D for precise infrastructure design and land modeling.

Driven by the evolving landscape of the industry, I am expanding my expertise into the realms of Data Analytics, Machine Learning (ML), and ESG (Environmental, Social, and Governance). I am currently building a portfolio that integrates my engineering domain knowledge with technical skills in Python and SQL to solve real-world data problems. My goal is to leverage these multi-disciplinary tools to foster more resilient infrastructure and contribute to sustainable, data-driven engineering solutions.

- **LinkedIn:** https://www.linkedin.com/in/joseph-monjok-a8b813232

---

## References

Every technical decision in this project that was not common knowledge is traceable
to a source. The table below maps each decision to where it came from.

| Decision | Source |
|----------|--------|
| What each NBI field means, how the 0–9 condition scale works, and the full column reference | FHWA Recording and Coding Guide for the Structure Inventory and Appraisal of the Nation's Bridges (FHWA-PD-96-001): Page 38 [https://www.fhwa.dot.gov/bridge/mtguide.pdf](https://www.fhwa.dot.gov/bridge/mtguide.pdf) |
| Why condition columns contain the letter `N` instead of a number | FHWA Coding Guide, Items 58–62. When a structural component does not exist on a bridge — for example, a highway bridge has no culvert — the inspector records `N` for Not Applicable. Pandas reads any column containing a letter as text, which is why those columns required type conversion |
| Why `ADT_029` contains the value `999,999` | FHWA Coding Guide, Item 29. The value 999,999 is the FHWA's designated code for an unknown average daily traffic count. It is not a real figure and was replaced with a null value before any analysis |
| Mapping numeric state codes to state names | US Census Bureau FIPS State Codes: [https://www.census.gov/library/reference/code-lists/ansi/ansi-codes-for-states.html](https://www.census.gov/library/reference/code-lists/ansi/ansi-codes-for-states.html) |
| Why scores of 4 and below define the structurally deficient threshold | FHWA Bridge Condition by Highway System 2022: [https://www.fhwa.dot.gov/bridge/nbi/no10/yrbkge22.cfm](https://www.fhwa.dot.gov/bridge/nbi/no10/yrbkge22.cfm) |
| Why `LOWEST_RATING` is the minimum of the three component scores | FHWA Coding Guide, Item 67. The overall safety status of a bridge is determined by the weakest of its inspected components |
| Why culverts must be separated from highway bridges before modelling | FHWA Coding Guide, Items 58–62. Culverts are drainage pipes rated with a single `CULVERT_COND_062` score. They have no deck, superstructure, or substructure. Mixing them with highway bridges produces structurally meaningless missing value patterns in those columns |
| How Ridge, Lasso, and ElasticNet regularisation works and when to use each | Géron, A. (2022). *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* (3rd ed.). O'Reilly Media. Chapter 4: Training Models |
| Data leakage — definition and why it was the basis for excluding component scores from model training | Kaufman, S., Rosset, S., Perlich, C., & Stitelman, O. (2012). Leakage in Data Mining: Formulation, Detection, and Avoidance. *ACM Transactions on Knowledge Discovery from Data*, 6(4) |

---

> *This project is part of a structured machine learning portfolio applying data
> science to real engineering and industry problems.*
> *Civil engineering domain knowledge + data science methods.*
