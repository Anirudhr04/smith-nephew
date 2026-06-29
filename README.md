# Supply Chain SIOP Reporting Dashboard

## Overview
This repository contains a Power BI dashboard designed for Sales, Inventory, and Operations Planning (SIOP). The dashboard provides executive-level visibility into supply chain performance by comparing forecast data against actuals to measure **Forecast Accuracy** and **Forecast Bias** across different regions and items.

## Key Features
* **Dynamic Forecast Lag Selection:** An interactive control panel allows users to dynamically switch the dashboard context between different forecast lag periods (Resultant, Lag 0, Lag 1).
* **Automated KPI Tracking:** Custom DAX measures instantly calculate aggregate Actuals, Forecasts, Forecast Bias %, and Forecast Accuracy %.
* **Geographical & Item-Level Drill-Downs:** A visual hierarchy that allows supply chain managers to view macro-level regional performance and drill down to root-cause item-level discrepancies.

## Data Architecture & Transformations
The backend data model was built using Power Query to handle complex matrix data structures:
* **Unpivoting Forecasts:** Transformed wide-format forecast matrix data into a structured tabular schema (Attribute/Value pairs) to enable dynamic DAX filtering.
* **Table Merging:** Consolidated granular Actuals data with the Forecast table matching on `Period`, `Item`, and `Country`.

## Core DAX Measures
The dashboard relies on robust DAX logic to handle unpivoted structures and prevent division-by-zero errors:
* **Total Actuals:** `SUM('Forecast'[Actuals__Revenue_Qty])`
* **Total Forecast:** `SUM('Forecast'[resultant revenue forecast])` *(dynamically adjusts based on lag selection)*
* **Forecast Bias %:** `DIVIDE([Total Forecast] - [Total Actuals], [Total Actuals], 0)`
* **Forecast Accuracy %:** `1 - ABS([Forecast Bias %])`

## Dashboard Layout
1. **Control Panel:** Interactive slicers for Period, Region/Country, and Lag Type.
2. **KPI Ribbon:** High-level summary cards displaying Total Actuals, Total Forecast, Bias %, and Accuracy %.
3. **Regional Comparison:** A clustered column chart displaying Forecast vs. Actual volume side-by-side per country.
4. **Diagnostic Matrix:** A detailed table layout itemizing Forecast Accuracy at the individual SKU/Item level to highlight supply chain variances.

## How to Use
1. Download the `.pbix` file from this repository.
2. Open using **Power BI Desktop**.
3. Use the slicers on the left-hand panel to interact with the data and filter by specific periods or forecast lags.
