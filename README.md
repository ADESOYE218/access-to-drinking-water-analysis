# access-to-drinking-water-analysis
Data analysis of global access to basic drinking-water services (2000–2020), exploring annual rates of change, rural vs. urban disparities, regional trends, and progress toward SDG 6.
# Access to Drinking Water: Data Analysis

## Overview

This project investigates global access to **basic drinking-water services** using data covering the period **2000–2020**.

The analysis focuses on the United Nations **Sustainable Development Goal 6 (SDG 6): Clean Water and Sanitation**, with particular attention to how access to basic water services has changed over time across:

* National populations
* Rural populations
* Urban populations
* Geographic regions

The project uses data transformation, statistical analysis, conditional calculations, and visualisation to understand patterns in access to drinking water and differences between rural and urban populations.


## Project Objectives

The main objectives of this project are to:

1. Understand the structure and representation of the water-access dataset.
2. Investigate the years represented for each country.
3. Calculate the **Annual Rate of Change (ARC)** in access to basic water services.
4. Compare changes in access across national, rural, and urban populations.
5. Identify countries with full access to basic water services.
6. Investigate differences between rural and urban progress.
7. Analyse water-access trends by geographic region.
8. Explore the relationship between population size, region, and Annual Rate of Change.
9. Communicate findings related to global progress toward SDG 6.


## Dataset

The primary dataset is based on the **WHO/UNICEF Joint Monitoring Programme (JMP) Estimates on the Use of Water**.

The analysis uses data covering approximately:

**2000–2020**

Key variables include:

| Variable       | Description                                                |
| -------------- | ---------------------------------------------------------- |
| `name`         | Country name                                               |
| `year`         | Year of observation                                        |
| `wat_bas_n`    | Access to basic water services for the national population |
| `wat_bas_r`    | Access to basic water services for the rural population    |
| `wat_bas_u`    | Access to basic water services for the urban population    |
| `population_n` | National population information                            |
| `region`       | Geographic region                                          |
| `y_diff`       | Difference between observation years                       |
| `ARC_n`        | Annual Rate of Change for national access                  |
| `ARC_r`        | Annual Rate of Change for rural access                     |
| `ARC_u`        | Annual Rate of Change for urban access                     |
| `ARC_n_full`   | Identifies countries with full national access             |
| `ARC_r_full`   | Identifies countries with full rural access                |
| `ARC_u_full`   | Identifies countries with full urban access                |
| `ARC_diff`     | Difference between rural and urban ARC                     |

---

## Annual Rate of Change

The project uses **Annual Rate of Change (ARC)** to measure the average yearly change in access to basic drinking-water services.

The general formula is:

```text
ARC = (P₂ - P₁) / (Y₂ - Y₁)
```

Where:

* `P₁` = access percentage in the first year
* `P₂` = access percentage in the second year
* `Y₁` = first year
* `Y₂` = second year

For example, the national ARC is calculated as:

```text
ARC_n = (wat_bas_n₂ - wat_bas_n₁) / (year₂ - year₁)
```

The ARC is expressed in **percentage points per year**.

A positive ARC indicates increasing access, while a negative ARC indicates declining access.


## Data Transformation

Several features were created during the analysis.

### 1. Year Difference

The `y_diff` feature measures the number of years between observations for the same country.

Conceptually:

```text
y_diff = year(n+1) - year(n)
```

The calculation is only performed when consecutive rows belong to the same country.

### 2. Annual Rates of Change

Three ARC variables were created:

```text
ARC_n
ARC_r
ARC_u
```

These represent annual changes for national, rural, and urban populations respectively.

### 3. Rounded Water Access

Additional rounded variables were created:

```text
wat_bas_n_rounded
wat_bas_r_rounded
wat_bas_u_rounded
```

Rounding allows values such as `99.6%` to be interpreted as `100%` when identifying countries that effectively have full access.

### 4. Full Access Indicators

The following variables identify countries with full access across the available observation period:

```text
ARC_n_full
ARC_r_full
ARC_u_full
```

### 5. Rural vs Urban Difference

The `ARC_diff` feature measures the difference between rural and urban Annual Rates of Change:

```text
ARC_diff = ARC_r - ARC_u
```

This helps identify whether access is improving faster in rural or urban populations.

---

## Analysis Workflow

### 01. Becoming Familiar with the Dataset

The first stage examines the structure of the dataset and compares the 2000–2020 dataset with the previously used dataset.

The analysis identifies:

* Available features
* Country observations
* Year representation
* Missing values
* Duplicate observations

---

### 02. Investigating Year Representation

The dataset does not necessarily contain observations for every year for every country.

The data is sorted by:

1. Country name
2. Year

The `y_diff` variable is then used to investigate the time gap between observations.

The analysis includes:

* Average year difference
* Minimum year difference
* Maximum year difference
* Distribution of observation years
* Identification of duplicate records

---

### 03. Investigating Annual Rates of Change

ARC is calculated separately for:

* National populations
* Rural populations
* Urban populations

The analysis calculates:

* Average ARC
* Minimum ARC
* Maximum ARC
* Missing ARC values
* Countries with increasing access
* Countries with decreasing access
* Countries with no change

---

### 04. Investigating Access by Area

The analysis investigates differences between national, rural, and urban populations.

Countries are classified according to whether their ARC is:

```text
Missing
Full access
ARC = 0
ARC < 0
ARC > 0
```

This provides a more meaningful interpretation of changes in access because countries that already have approximately 100% access may have an ARC of zero simply because there is little room for improvement.

---

### 05. Investigating Access by Region

Regional information is added to the dataset using the `Regions.csv` file.

The analysis calculates:

* Number of countries per region
* Average national ARC
* Average rural ARC
* Average urban ARC

The results are then visualised to investigate relationships between:

* Region
* National ARC
* Rural ARC
* Population size

---

## Key Questions

The project attempts to answer questions such as:

* How frequently were water-access observations recorded?
* What is the average time between observations?
* Is access to basic water services improving?
* Is access improving faster in rural or urban areas?
* Which countries experienced declining access?
* How many countries already have full access?
* Which regions have experienced the greatest improvement?
* What is the relationship between national and rural progress?
* Does population size appear to influence Annual Rate of Change?
* Which countries show the largest rural–urban differences?



## Visualisations

The project includes visualisations such as:

### Year Distribution

A histogram showing the distribution of years represented in the dataset.

### Rural vs Urban ARC

A histogram showing the difference between rural and urban Annual Rates of Change.

### Regional Analysis

A visualisation comparing:

* National ARC
* Rural ARC
* Region
* National population size

These visualisations help identify geographical and population-related patterns that may not be immediately apparent from summary statistics.

---

## Example Google Sheets Formulas

### Year Difference

```excel
=IF(A3=A2,B3-B2,"")
```

### National ARC

```excel
=IF($A3=$A2,(E3-E2)/($B3-$B2),"")
```

### ARC with Error Handling

```excel
=IFERROR(IF($A3=$A2,(E3-E2)/($B3-$B2),""),"null")
```

The same approach can be adapted for rural and urban access.

### Full Access

A conditional statement can be used to identify countries whose rounded access values reach 100% across both observations.

---

## Important Interpretation

A higher ARC does not automatically mean that a population has better access to water.

For example, a country already reporting approximately **100% access** may have an ARC close to zero because there is little opportunity for further improvement.

Therefore, ARC should be interpreted alongside:

* Existing access levels
* Full-access indicators
* Population type
* Region
* Population size

This distinction is particularly important when comparing rural and urban populations.

---

## Findings and Discussion

The analysis highlights the continuing disparity in access to basic drinking-water services.

Rural populations generally face greater challenges in accessing basic water services than urban populations. However, changes in ARC need to be interpreted carefully because countries starting from very different access levels can have very different rates of progress.

Regional analysis also provides insight into where improvements are occurring and where significant gaps remain.

The project particularly highlights **Sub-Saharan Africa** as an important region in discussions around global water access and SDG 6.

---

## SDG 6: Clean Water and Sanitation

This project contributes to the broader discussion surrounding:

**United Nations Sustainable Development Goal 6 — Clean Water and Sanitation.**

SDG 6 aims to ensure availability and sustainable management of water and sanitation for all.

Understanding changes in access to basic drinking-water services can help identify:

* Areas requiring additional investment
* Rural–urban disparities
* Regions experiencing slower progress
* Countries where access is declining
* Opportunities for targeted intervention

---

## Project Structure

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

## Tools Used

* **Google Sheets** — Data cleaning, transformation, calculations, and visualisation
* **Spreadsheet formulas** — `IF`, `IFERROR`, `COUNTIFS`, lookup functions, and statistical functions
* **Data analysis** — Descriptive statistics and Annual Rate of Change
* **Data visualisation** — Histograms and regional comparison plots
* **GitHub** — Project documentation and version control


## Learning Outcomes

Through this project, I developed practical experience in:

* Data cleaning
* Data transformation
* Spreadsheet analysis
* Conditional logic
* Handling missing values
* Duplicate detection
* Statistical summaries
* Annual Rate of Change calculations
* Data visualisation
* Geographic analysis
* Rural vs urban comparison
* Communicating data-driven insights

---

## Limitations

The analysis has several limitations:

1. The dataset does not contain observations for every year for every country.
2. Missing values can affect ARC calculations.
3. ARC measures change but does not describe the full context behind that change.
4. Countries may begin the analysis period with very different levels of water access.
5. Rounded values are used when identifying approximately 100% access.
6. Regional averages can hide substantial differences between individual countries.
7. Population size and access trends should not automatically be interpreted as causal relationships.

---

## Conclusion

Access to safe and basic drinking water remains an important global development issue.

By transforming the WHO/UNICEF JMP water-access data and calculating Annual Rates of Change, this project provides a structured way to examine progress across national, rural, and urban populations.

The analysis demonstrates why data transformation and appropriate statistical interpretation are important when evaluating progress toward **SDG 6: Clean Water and Sanitation**.

The results can help highlight where progress is occurring, where disparities remain, and where additional attention may be required.


## Data Source

The project is based on the **WHO/UNICEF Joint Monitoring Programme (JMP) for Water Supply, Sanitation and Hygiene** data.

