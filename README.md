# volve-field-production-analytics
Interactive Power BI dashboard and analytical framework analyzing Equinor’s public Volve Oil Field dataset to evaluate hydrocarbon production trends, well performance, WOR, and GOR ratios.
# Volve Field Production Analytics & Well Performance Dashboard

## Project Overview
This project presents an end-to-end data analysis and visualization pipeline for Equinor’s public **Volve Oil Field** dataset (North Sea). Using daily production records spanning nearly a decade, I processed and structured the data in Excel and Power BI to analyze hydrocarbon recovery, trace production decline, and evaluate individual well behavior.

The main goal of this dashboard is to give petroleum engineers and stakeholders quick visibility into total field output, identifying top-performing wells and tracking key subsurface performance metrics like **Water-Oil Ratio (WOR)** and **Gas-Oil Ratio (GOR)**.

---

## Key Business Insights
* **Cumulative Field Output:** Generated **10.04M Sm³** of oil, **15.32M Sm³** of water, and **1.48BN Sm³** of gas across **13,000+ operational days** (Sept 2007 – Dec 2016).
* **Pareto Distribution in Production:** Two primary production wells—`15/9-F-12` (45.63%) and `15/9-F-14` (39.28%)—accounted for **over 84%** of the total oil extracted from the field.
* **Water Cut Escalation:** Production peaked in 2009 before natural reservoir depletion set in. Sharp increases in WOR starting around 2013 highlight water breakthrough in aging wells.

---

## Dashboard Architecture

### Page 1: Field Production Overview
Focuses on macro-level field performance and production contribution.
* **KPI Header Cards:** Executive summaries displaying total oil, water, gas, and active well counts.
* **Production Trends (Line Chart):** Historical monthly production profiles from 2008 to 2016.
* **Well Breakdown (Bar Chart & Donut Visual):** Oil volume contribution broken down by individual wellbore names.

### Page 2: Well Production Behavior
Allows granular, well-by-well dynamic filtering to analyze reservoir longevity and fluid ratios.
* **Well Slicer Controls:** Toggle across specific wellbores (`15/9-F-1 C`, `15/9-F-11`, `15/9-F-12`, `15/9-F-14`, `15/9-F-15 D`, `15/9-F-4`, `15/9-F-5`).
* **Operational Timelines:** Tracks active production start dates, completion dates, and total producing days.
* **Fluid Ratios:** Yearly trends for **Water-Oil Ratio (WOR)** and **Gas-Oil Ratio (GOR)** to monitor well efficiency and water breakthrough.

---

## Data Transformation & Engineering Logic

The raw daily logs required feature engineering in Excel and Power Query prior to visualization:

1. **Total Liquid Volume:**
   $$\text{Total Liquid} = \text{BORE\_OIL\_VOL} + \text{BORE\_WAT\_VOL}$$

2. **Water-Oil Ratio (WOR):**
   $$\text{WOR} = \frac{\text{BORE\_WAT\_VOL}}{\text{BORE\_OIL\_VOL}}$$

3. **Gas-Oil Ratio (GOR):**
   $$\text{GOR} = \frac{\text{BORE\_GAS\_VOL}}{\text{BORE\_OIL\_VOL}}$$

* **Data Cleaning:** Filtered out shut-in/non-producing operational days, standard calendar attributes (Year, Month Name, Month Number), and validated raw headers.
---

## Data Dictionary

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `DATEPRD` | Date | Record entry date |
| `NPD_WELL_BORE_NAME` | Text | Official well identifier |
| `BORE_OIL_VOL` | Decimal | Daily oil production volume ($\text{Sm}^3$) |
| `BORE_GAS_VOL` | Decimal | Daily gas production volume ($\text{Sm}^3$) |
| `BORE_WAT_VOL` | Decimal | Daily water production volume ($\text{Sm}^3$) |
| `ON_STREAM_HRS` | Numeric | Hours the well was actively producing |
| `AVG_DOWNHOLE_PRESSURE` | Decimal | Average bottom-hole pressure ($\text{psi}$ / $\text{bar}$) |

---

## Future Improvements (V2 Roadmap)
* **Star Schema Implementation:** Separate flat staging tables into dedicated `Dim_Well` and `Dim_Date` dimension tables linked to a clean fact table.
* **DAX Optimization:** Move calculated columns to dynamic DAX measures using `DIVIDE()` to safely handle zero-oil production days without math errors.
* **Automated Gateway Refresh:** Connect Power BI Service directly to a cloud data lake for scheduled updates.

---

## How to View
1. Download the `.pbix` file from this repository.
2. Open using **Power BI Desktop** (Latest version recommended).
3. Ensure the source path for `Copy of Volve production data.xlsx` is updated in Power Query if refreshing data locally.
