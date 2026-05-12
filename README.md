# Settlement_Query_Manager
A dynamic Excel-based risk management tool designed to centralise trade exceptions and prioritise Aged Risk across global markets. 

## Executive Summary
This project involves the creation of an interactive dashboard and Aged Risk Tracker for a Markets Operations environment. The tool is engineered to provide real-time visibility into trade settlement queries, prioritising "High Risk" to ensure regulatory compliance. By transitioning from static data lists to a dynamic, risk-first visualization, the dashboard reduces management blind spots and accelerates decision-making.

## Visual Preview
![Settlement Query Management Dashboard Preview](images/Dashboard_Overview.png)

## Problem Statement
In high-volume financial operations, client queries can be spread across multiple desks. Manual tracking leads to "Aged Risks" - trades that remain unsettled past their value date, increasing financial exposure.

## Objectives
* **Centralisation** - Consolidate trade queries into a single resource.
* **Mitigate Risk** - Implement logic to categorise trades into Low, Medium and High Risk buckets and flag High Risk buckets.
* **Dynamic Interactivity** - Enable desk-specific drill downs using synchronised slicers.

## Technical Highlights

### Aging Logic (NETWORKDAYS)
Calculates trade latency based on business days rather than calander days. Through integrating a MAX(0,) wrapper, the logic eliminates negative aging values for trades settled on the same day and accurately reflects trade settlement cycles by excluding weekends and holidays.

### Dynamic Tables
Utalises structured tables to make the dashboard scalable, This means formulas, Pivot Table ranges and conditional formatting automatically expand as new trade queries are added. Minimising manual maintenance and broken range references.

### Logic Bridge (GETPIVOTDATA) (IFERROR)
Contains a connection layer between the raw data and the UI. By using the GETPIVOTDATA and IFERROR functions, the dashboard maintains data integrity during zero volume.

```excel
=IFERROR(GETPIVOTDATA("Query ID",Calculation_Sheet!$B$4,"Status","Open"),0)
```
