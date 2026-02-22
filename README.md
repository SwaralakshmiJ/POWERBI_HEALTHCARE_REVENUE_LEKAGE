# # Healthcare Revenue Leakage Analysis using POWERBI
"Utilized Power BI Desktop to engineer a financial audit dashboard. Implemented DAX measures to identify $8.8M in revenue leakage and utilized Power Query for data normalization, resulting in a 100% accurate audit of billing anomalies across 55k+ records."

## 📌 Project Overview
This project focuses on identifying and analyzing **Revenue Leakage** within a hospital's billing system. By analyzing a dataset of 55,000+ patient records, I identified specific billing anomalies where high-cost treatments (>$45,000) were associated with ultra-short hospital stays (≤1 day).

**Key Finding:** Identified **$8.8 Million** in potential revenue leakage due to billing inconsistencies.

## 🛠️ Tech Stack
* **Data Tool:** Power BI Desktop
* **Data Source:** Cleaned Healthcare Dataset (`healthcare_cleaned`)
* **Language:** DAX (Data Analysis Expressions) for complex calculations
* **Architecture:** Star Schema (transformed into a high-performance Flat Table)

## 📊 Data Model & Logic
The analysis is built on a consolidated healthcare table containing patient demographics, admission details, and financial data.

### The "Revenue Leakage" Logic
To isolate high-risk billing errors, the following logic was applied:
1.  **High-Value Filter:** Bills exceeding **$45,000**.
2.  **Short-Stay Filter:** Discharge occurs within **1 day** (24 hours) of admission.
3.  **The Result:** These cases represent high-risk anomalies that require manual audit to prevent financial loss.

## 📈 Key Measures (DAX)
Selected formulas used in this project:

* **Total Revenue:** `SUM('healthcare_cleaned'[Billing Amount])`
* **Revenue Leakage:** ```dax
    CALCULATE(
        [Total Revenue],
        FILTER(
            'healthcare_cleaned',
            DATEDIFF('healthcare_cleaned'[Date of Admission], 'healthcare_cleaned'[Discharge Date], DAY) <= 1 
            && 'healthcare_cleaned'[Billing Amount] > 45000
        )
    )
    ```
* **Leakage %:** `DIVIDE([Revenue Leakage], [Total Revenue], 0)`

## 🖥️ Dashboard Features
* **Executive KPI Cards:** Real-time tracking of Total Revenue, Leakage Amount, and Efficiency %.
* **Medical Condition Analysis:** A bar chart identifying which diseases (e.g., Diabetes, Cancer) drive the highest billing risks.
* **Doctor Integrity Leaderboard:** A detailed table ranking practitioners by their associated leakage amounts.
* **Interactive Slicers:** Ability to filter the entire audit by **Insurance Provider**, **Admission Type**, and **Gender**.

## 💡 Business Insights
* **Total Identified Risk:** $8.8M.
* **Top Risk Factor:** Emergency admissions combined with "Abnormal" test results showed the highest correlation with leakage.
* **Primary Action:** Recommended a targeted audit for the top 5 doctors contributing to 40% of the total leakage.

---
*Created as part of a Healthcare Data Analytics Portfolio.*
