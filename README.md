# Access-to-drinking-water-analysis
Data analysis of global access to basic drinking-water services (2000–2020), exploring annual rates of change, rural vs. urban disparities, regional trends, and progress toward SDG 6.

## ExploreAI 2023 Integrated Project — SDG 6: Clean Water and Sanitation

This project investigates global access to **basic drinking-water services** between **2000 and 2020**, with a focus on changes in access at the **national, rural, and urban levels**.

The analysis uses data from the WHO/UNICEF Joint Monitoring Programme (JMP) and explores how access to drinking water has changed over time, how rural and urban populations compare, and how progress differs across global regions.

A key part of the project is the calculation of the **Annual Rate of Change (ARC)**, which measures the average yearly change in access to basic drinking-water services.

---

## Overview

Access to safe and reliable drinking water is an essential component of public health, economic development, and human well-being.

The project investigates the following question:

> **How has access to basic drinking-water services changed between 2000 and 2020, and how does progress differ between national, rural, urban, and regional populations?**

The analysis focuses on:

* Changes in drinking-water access over time
* Annual rates of change
* Rural versus urban differences
* Countries reaching full access
* Countries experiencing declining access
* Regional differences in progress
* The relationship between progress and the Sustainable Development Goal 6

---

## Project Objectives

The main objectives of this project are to:

1. Understand the structure and contents of the drinking-water dataset.
2. Investigate how observations are distributed across the years.
3. Calculate and analyse the **Annual Rate of Change (ARC)**.
4. Compare drinking-water access between rural and urban populations.
5. Identify countries with full access and countries experiencing declining access.
6. Investigate differences in progress across global regions.
7. Interpret the findings in relation to **UN Sustainable Development Goal 6**.

---

# Dataset

The main dataset used in this project is:

**`Estimates on the use of water (2000-2020).csv`**

A second dataset was used to assign countries to geographical regions:

**`Regions.csv`**

### Main variables

The original dataset contains information including:

* Country name
* Year
* National drinking-water access
* Rural drinking-water access
* Urban drinking-water access
* Population information

Additional calculated variables were created during the analysis.

---

# Project Workflow

The project was completed through five main stages.

### Stage 1 — Becoming familiar with the dataset

The first stage involved exploring the dataset to understand:

* The number of observations
* The countries represented
* The years covered
* The available drinking-water indicators
* The structure and meaning of the variables

### Stage 2 — Investigating year representation

The distribution of observations across years was examined to understand whether the dataset contained consistent yearly information.

This was important because the calculation of ARC depends on comparing observations from different years.

### Stage 3 — Investigating Annual Rates of Change

The Annual Rate of Change was calculated for:

* National access
* Rural access
* Urban access

ARC provides a way of measuring how quickly drinking-water access changes from one observation to the next.

### Stage 4 — Investigating access by area

The analysis compared:

* National access
* Rural access
* Urban access

Additional indicators were created to identify observations where access was effectively **100% of the population**.

### Stage 5 — Investigating access by region

Countries were linked to geographical regions using `Regions.csv`.

The ARC indicators were then aggregated to investigate differences in progress across:

* East Asia & Pacific
* Europe & Central Asia
* Latin America & Caribbean
* Middle East & North Africa
* North America
* South Asia
* Sub-Saharan Africa

---

# Annual Rate of Change (ARC)

The Annual Rate of Change measures the average change in drinking-water access between two observations.

The general formula is:

```text
ARC = (P2 - P1) / (Y2 - Y1)
```

Where:

* `P1` = drinking-water access at the first observation
* `P2` = drinking-water access at the second observation
* `Y1` = first year
* `Y2` = second year

The result represents the approximate **percentage-point change per year**.

### Interpretation

* **ARC > 0** → access is increasing
* **ARC = 0** → no change in access
* **ARC < 0** → access is decreasing

For example, an ARC of `0.5` means that access increased by approximately **0.5 percentage points per year** over the period being compared.

---

# ARC Calculations

The following calculated variables were created:

```text
ARC_n
ARC_r
ARC_u
```

Where:

* `ARC_n` = National ARC
* `ARC_r` = Rural ARC
* `ARC_u` = Urban ARC

The calculations were based on consecutive observations for the same country.

For example:

```text
ARC_n = (wat_bas_n(n+1) - wat_bas_n(n))
        / (year(n+1) - year(n))
```

The same approach was used for rural and urban access.

---

# Data Transformation

Several new variables were created during the analysis.

### `y_diff`

Measures the difference between two observation years.

### `ARC_n`

Annual Rate of Change for national drinking-water access.

### `ARC_r`

Annual Rate of Change for rural drinking-water access.

### `ARC_u`

Annual Rate of Change for urban drinking-water access.

### Rounded access variables

The following variables were created for the full-access analysis:

```text
wat_bas_n (rounded)
wat_bas_r (rounded)
wat_bas_u (rounded)
```

### Full-access ARC variables

The following variables were also created:

```text
ARC_n_full
ARC_r_full
ARC_u_full
```

These were used to distinguish full-access observations from observations where further improvement was still possible.

### `ARC_diff`

The rural–urban ARC difference was calculated as:

```text
ARC_diff = ARC_r - ARC_u
```

A positive value means rural access was improving faster than urban access.

---

# Handling Missing Values

Missing ARC values do not necessarily represent zero change.

They can occur because:

* There is no previous observation for comparison.
* The required consecutive observation is missing.
* There is insufficient information to calculate an ARC.
* The year difference is unavailable.

Therefore:

> **Missing ARC values should be interpreted as unavailable calculations rather than evidence of no progress.**

---

# Full Access Analysis

The project also investigated observations where drinking-water access was effectively **100% of the population**.

The full-access analysis used rounded values and considered both observations involved in the comparison.

This distinction is important because countries already at full access have little or no room for further improvement.

Consequently, an ARC of zero can mean something very different depending on the starting level of access.

For example:

* A country with 100% access and ARC = 0 is already at full coverage.
* A country with 70% access and ARC = 0 has experienced stagnation and still has a substantial coverage gap.

---

# Rural vs Urban Analysis

One of the major objectives of the project was to investigate whether drinking-water access was changing at different rates in rural and urban areas.

The comparison was based on:

```text
ARC_diff = ARC_r - ARC_u
```

### Interpretation

* `ARC_diff > 0` → rural access is improving faster
* `ARC_diff < 0` → urban access is improving faster
* `ARC_diff = 0` → rural and urban progress is occurring at the same rate

Importantly, a higher rural ARC does **not** necessarily mean that rural areas have better access.

Rural areas may begin from a lower baseline and therefore have more room for improvement.

---

# Key Findings

## Overall ARC Summary

| Statistic | Year Difference | National ARC | Rural ARC | Urban ARC |
| --------- | --------------: | -----------: | --------: | --------: |
| Average   |             4.8 |       0.2767 |    0.4845 |    0.1548 |
| Minimum   |              5* |      -1.0218 |   -1.2274 |   -1.6201 |
| Maximum   |              1* |       2.7503 |    2.6679 |    2.6682 |

*The supplied Year Difference minimum/maximum values should be verified against the spreadsheet before publication, as their ordering appears unusual.

### Main observation

The average ARC was highest for **rural areas**:

* Rural: **0.4845 percentage points/year**
* National: **0.2767 percentage points/year**
* Urban: **0.1548 percentage points/year**

This suggests that, on average, rural drinking-water access was improving more rapidly than urban access.

However, this does not mean that rural access was necessarily higher. A higher ARC can occur because rural areas started from lower access levels and therefore had more room for improvement.

---

# ARC Classification

After excluding observations representing full access, the ARC results were classified as positive, zero, or negative.

| Category | National | Rural | Urban |
| -------- | -------: | ----: | ----: |
| ARC > 0  |      135 |   116 |    93 |
| ARC = 0  |       16 |     5 |     7 |
| ARC < 0  |       16 |    17 |    26 |

### Positive ARC

Most observations showed improvement:

* National: **135**
* Rural: **116**
* Urban: **93**

This indicates that increasing access was substantially more common than declining access.

### Zero ARC

The number of observations with no change was:

* National: **16**
* Rural: **5**
* Urban: **7**

These values exclude observations identified as already having full access.

### Negative ARC

Declining access occurred in:

* National: **16**
* Rural: **17**
* Urban: **26**

Urban areas therefore had the highest number of observations showing declining access.

---

# Full Access Findings

The analysis identified the following number of full-access observations:

| Area     | Full Access |
| -------- | ----------: |
| National |          62 |
| Rural    |          29 |
| Urban    |          55 |

Urban full access was considerably more common than rural full access.

This is consistent with the broader observation that rural areas generally have greater remaining room for improvement.

---

# Missing ARC Values

The analysis identified:

| Area     | Missing ARC Values |
| -------- | -----------------: |
| National |                  2 |
| Rural    |                 64 |
| Urban    |                 50 |

The larger number of missing rural and urban ARC values highlights the importance of considering data availability when comparing progress.

---

# Rural vs Urban Progress

The results reveal an important pattern:

> **Rural areas had a higher average ARC than urban areas.**

Average ARC:

| Area     | Average ARC |
| -------- | ----------: |
| Rural    |  **0.4845** |
| National |  **0.2767** |
| Urban    |  **0.1548** |

This suggests that rural areas were, on average, experiencing faster improvements in drinking-water access.

However, this should not be interpreted as rural populations having greater overall access.

The ARC measures **rate of change**, not the absolute level of access.

---

# Declining Access

Urban observations had the highest number of negative ARC values:

```text
National: 16
Rural:    17
Urban:    26
```

The most negative ARC values were:

* National: **-1.0218**
* Rural: **-1.2274**
* Urban: **-1.6201**

These results show that although overall progress was generally positive, declines in drinking-water access did occur.

---

# Regional Analysis

Countries were grouped into seven regions using `Regions.csv`.

The following table shows the average ARC for national, rural, and urban access.

| Region                     | Average National ARC | Average Rural ARC | Average Urban ARC | Countries |
| -------------------------- | -------------------: | ----------------: | ----------------: | --------: |
| East Asia & Pacific        |               0.2784 |            0.5078 |            0.2330 |        40 |
| Europe & Central Asia      |               0.1117 |            0.2244 |            0.0470 |        64 |
| Latin America & Caribbean  |               0.1444 |            0.6803 |            0.0715 |        48 |
| Middle East & North Africa |               0.3456 |            0.7370 |            0.1240 |        10 |
| North America              |               0.0172 |            0.1423 |            0.0020 |         5 |
| South Asia                 |               0.4802 |            0.5591 |            0.2655 |        11 |
| Sub-Saharan Africa         |               0.5583 |            0.6042 |            0.2704 |        53 |

---

# Regional Findings

## Sub-Saharan Africa

Sub-Saharan Africa had the **highest average national ARC**:

```text
National: 0.5583
Rural:    0.6042
Urban:    0.2704
```

With **53 countries**, the region represents one of the largest groups in the analysis.

The results suggest strong overall progress, particularly in rural areas.

---

## Middle East & North Africa

The Middle East & North Africa had the **highest average rural ARC**:

```text
National: 0.3456
Rural:    0.7370
Urban:    0.1240
```

The rural ARC of **0.7370 percentage points per year** was the highest among all regions.

However, the region contains only **10 countries**, so the result should be interpreted with some caution.

---

## Latin America & Caribbean

The region recorded:

```text
National: 0.1444
Rural:    0.6803
Urban:    0.0715
```

The rural rate was substantially higher than the urban rate.

The region contains **48 countries** in the analysis.

---

## South Asia

South Asia recorded:

```text
National: 0.4802
Rural:    0.5591
Urban:    0.2655
```

The region therefore showed strong national and rural progress.

There were **11 countries** represented.

---

## East Asia & Pacific

East Asia & Pacific recorded:

```text
National: 0.2784
Rural:    0.5078
Urban:    0.2330
```

The results again show faster rural improvement compared with urban improvement.

The analysis contains **40 countries** from this region.

---

## Europe & Central Asia

Europe & Central Asia recorded:

```text
National: 0.1117
Rural:    0.2244
Urban:    0.0470
```

The relatively low ARC values may partly reflect the fact that many countries in the region already had relatively high levels of drinking-water access.

The region contains **64 countries**, the largest regional count in this analysis.

---

## North America

North America had the lowest average ARC across all three categories:

```text
National: 0.0172
Rural:    0.1423
Urban:    0.0020
```

The analysis contains **5 countries** from this region.

The low ARC should not automatically be interpreted as poor performance.

Countries with already-high levels of access have less room for further improvement, which can result in a lower rate of change.

---

# Regional National ARC Ranking

Based on average national ARC:

| Rank | Region                     | National ARC |
| ---: | -------------------------- | -----------: |
|    1 | Sub-Saharan Africa         |       0.5583 |
|    2 | South Asia                 |       0.4802 |
|    3 | Middle East & North Africa |       0.3456 |
|    4 | East Asia & Pacific        |       0.2784 |
|    5 | Latin America & Caribbean  |       0.1444 |
|    6 | Europe & Central Asia      |       0.1117 |
|    7 | North America              |       0.0172 |

This ranking indicates that the fastest average national progress occurred in **Sub-Saharan Africa**, while North America had the lowest average rate of change.

Again, the ranking measures **rate of improvement**, not absolute access levels.

---

# Regional Rural vs Urban Comparison

The rural–urban ARC difference was calculated using:

```text
ARC_diff = ARC_r - ARC_u
```

| Region                     | Rural–Urban ARC Difference |
| -------------------------- | -------------------------: |
| East Asia & Pacific        |                     0.2748 |
| Europe & Central Asia      |                     0.1774 |
| Latin America & Caribbean  |                     0.6088 |
| Middle East & North Africa |                     0.6130 |
| North America              |                     0.1403 |
| South Asia                 |                     0.2937 |
| Sub-Saharan Africa         |                     0.3338 |

### Largest rural–urban differences

The largest differences were observed in:

1. **Middle East & North Africa — 0.6130**
2. **Latin America & Caribbean — 0.6088**
3. **Sub-Saharan Africa — 0.3338**
4. **South Asia — 0.2937**

The important overall pattern is that:

> **Rural ARC was higher than urban ARC in every region.**

This suggests that rural areas were generally experiencing faster improvements in drinking-water access than urban areas during the period analysed.

---

# Important Interpretation

ARC should not be used by itself to determine which region or country has the best drinking-water situation.

For example, a country with:

```text
99% access → 100% access
```

may have a small ARC because it is already close to universal coverage.

Meanwhile:

```text
50% access → 60% access
```

can produce a much larger ARC despite the country still having considerably lower overall access.

Therefore, ARC should be interpreted alongside:

* Current access levels
* Starting access levels
* Full-access indicators
* Rural/urban differences
* Data availability
* Regional context

---

# Visualisations

Recommended visualisations for the project include:

### 1. Year Distribution

Shows how observations are distributed across the 2000–2020 period.

Suggested file:

```text
visualizations/year_distribution.png
```

### 2. Rural vs Urban ARC

A comparison of average rural and urban ARC.

Suggested file:

```text
visualizations/arc_rural_vs_urban.png
```

### 3. Regional ARC Analysis

Compares national, rural, and urban ARC across the seven regions.

Suggested file:

```text
visualizations/regional_arc_analysis.png
```

---

# Google Sheets Formulas

The analysis was also performed using Google Sheets.

## Year Difference

```excel
=IF(A3=A2,B3-B2,"")
```

This calculates the difference between years when the observations belong to the same country.

---

## National ARC

```excel
=IF($A3=$A2,(E3-E2)/($B3-$B2),"")
```

---

## ARC with Error Handling

```excel
=IFERROR(IF($A3=$A2,(E3-E2)/($B3-$B2),""),"null")
```

This prevents errors caused by missing or invalid comparisons.

---

# Key Insights

Several major insights emerged from the analysis.

### 1. Drinking-water access generally improved

Most observations had a positive ARC.

This indicates that access to basic drinking-water services generally increased between observations.

### 2. Rural access improved faster on average

The average rural ARC was:

```text
0.4845 percentage points/year
```

compared with:

```text
National: 0.2767
Urban:    0.1548
```

### 3. Urban areas experienced more declines

There were:

```text
26 urban negative ARC observations
```

compared with:

```text
17 rural
16 national
```

### 4. Full access was more common in urban areas

Full-access observations were:

```text
National: 62
Rural:    29
Urban:    55
```

### 5. Rural progress was faster across every region

Every regional group had a higher average rural ARC than urban ARC.

### 6. Sub-Saharan Africa had the highest average national ARC

Its average national ARC was:

```text
0.5583
```

### 7. Middle East & North Africa had the highest rural ARC

Its average rural ARC was:

```text
0.7370
```

### 8. North America had the lowest ARC

North America's average ARC was lowest across national, rural, and urban categories.

This may partly reflect already-high levels of access and therefore limited room for improvement.

---

# SDG 6 — Clean Water and Sanitation

This project directly relates to **Sustainable Development Goal 6 (SDG 6)**:

> **Ensure availability and sustainable management of water and sanitation for all.**

Access to safe drinking water is a fundamental component of SDG 6.

The analysis helps demonstrate how access has changed over time and where progress may still be needed.

The rural–urban comparison is particularly relevant because differences in access can highlight inequalities in infrastructure and service provision.

---

# Broader Context

The findings demonstrate that measuring progress requires more than simply looking at whether access increased.

A complete assessment should consider:

* How much access increased
* The starting level of access
* The remaining population without access
* Rural versus urban differences
* Regional inequalities
* Whether progress is accelerating or declining
* Data availability and quality

The ARC approach provides a useful measure of progress, but it should be combined with absolute access indicators for a more complete picture.

---

# Tools Used

The project used:

* **Google Sheets** — data cleaning and calculations
* **CSV datasets** — source data
* **GitHub** — project documentation and version control
* **Data analysis techniques** — comparison, aggregation, and interpretation
* **WHO/UNICEF JMP data** — drinking-water access estimates

---

# Project Structure

A suggested repository structure is:

```text
access-to-drinking-water-analysis/
│
├── data/
│   ├── Estimates on the use of water (2000-2020).csv
│   └── Regions.csv
│
├── analysis/
│   └── Access_to_Drinking_Water_Analysis.xlsx
│
├── visualizations/
│   ├── year_distribution.png
│   ├── arc_rural_vs_urban.png
│   └── regional_arc_analysis.png
│
├── README.md
├── .gitignore
└── LICENSE
```

---

# Learning Outcomes

Through this project, I developed practical experience in:

* Exploring real-world datasets
* Understanding data structures
* Cleaning and transforming data
* Creating calculated variables
* Working with missing values
* Applying mathematical formulas to data
* Calculating Annual Rates of Change
* Comparing rural and urban populations
* Grouping data by geographical region
* Creating summary statistics
* Interpreting data-driven findings
* Connecting data analysis to the Sustainable Development Goals
* Documenting a data-analysis project using GitHub

---

# Limitations

There are several limitations to consider when interpreting the findings.

### Data availability

Some countries and years have missing observations, which affects ARC calculations.

### Unequal regional sample sizes

The number of countries differs considerably between regions.

For example:

* North America: **5 countries**
* Middle East & North Africa: **10 countries**
* Europe & Central Asia: **64 countries**

Regional averages based on small numbers of countries should therefore be interpreted cautiously.

### ARC does not represent absolute access

A high ARC does not necessarily mean high drinking-water access.

Likewise, a low ARC does not necessarily mean poor performance.

### Country-level variation

Regional averages can hide substantial differences between individual countries.

### Full-access effect

Countries already close to 100% access have less room for improvement, which can naturally result in lower ARC values.

---

# Conclusion

This project analysed global access to basic drinking-water services from **2000 to 2020**, with particular attention to national, rural, urban, and regional trends.

The analysis found that drinking-water access generally improved over the period, with **rural areas showing a higher average Annual Rate of Change than urban areas**.

At the regional level, **Sub-Saharan Africa recorded the highest average national ARC**, while **Middle East & North Africa recorded the highest average rural ARC**.

A consistent finding across all regions was that **rural ARC was higher than urban ARC**, indicating faster rates of improvement in rural areas. However, this should not be interpreted as rural areas having higher overall access, since ARC measures the rate of change rather than the absolute level of access.

The analysis also identified observations with declining access, full access, zero change, and missing ARC values. These results demonstrate the importance of considering both data quality and starting levels of access when interpreting progress.

Overall, the project demonstrates how data analysis can be used to investigate progress toward **SDG 6: Clean Water and Sanitation**, while also highlighting the importance of understanding inequalities between rural and urban populations and across different regions of the world.

---

# Data Source

The project uses drinking-water access estimates from the **WHO/UNICEF Joint Monitoring Programme (JMP)** and the accompanying regional classification dataset used in the project.


# Disclaimer

This project was completed for educational and analytical purposes as part of the ExploreAI 2023 integrated project.

The findings presented in this repository are based on the supplied datasets and the methodology described above. Regional and country-level results should be interpreted in the context of data availability, differences in baseline access, and the limitations of using Annual Rate of Change as a standalone measure of progress.


## Author

**ExploreAI 2023 — Integrated Project**

*Access to Drinking Water | SDG 6: Clean Water and Sanitation*



