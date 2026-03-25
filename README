# Saskatchewan Regional Inventory Risk Report — Q1 2026

**Live Dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/joshua.manoj/viz/SaskatchewanRegionalInventoryRiskReport-Q12026/SaskatchewanBranchHealthMap)

---

## Project Overview

A regional supply chain monitoring system built to track inventory health across multiple Saskatchewan branch locations. The goal was to move from reactive restocking to **proactive supply management** — identifying branches at risk of stockouts before they happen, with enough lead time to act.

The project combines **BigQuery SQL analysis** with a **Tableau Public dashboard** to give operations managers a real-time view of which branches and parts need immediate attention.

---

## Business Problem

Saskatchewan branch managers were identifying inventory issues reactively — only after stockouts had already occurred or were imminent. There was no centralized, visual way to monitor stock health across all locations simultaneously.

**Key questions this project answers:**
- Which branches are critically understocked right now?
- Which specific parts are at the highest risk of running out?
- Where should restocking efforts be prioritized across the province?

---

## Data Source

- **Dataset:** Branch-level sales and inventory data across Saskatchewan locations
- **Fields:** Branch Location, Part Name, Monthly Sales Quantity, Current Inventory, Revenue, Profit
- **Tool:** Google BigQuery (`ins-optimizer.salesinventory.SI analysis`)
- **Branches covered:** Estevan, and additional Saskatchewan locations

---

## SQL Query — Core Analysis Logic

The central analysis was a Stock-to-Sales Ratio calculation, with business status classification for dashboard filtering:

```sql
SELECT 
    Branch_Location,
    Part_Name,
    Quantity AS Monthly_Sales,
    Current_Inventory,
    -- Step 1: Calculate the critical ratio
    ROUND(SAFE_DIVIDE(Current_Inventory, Quantity), 2) AS Stock_to_Sales_Ratio,
    -- Step 2: Assign a business status for the dashboard
    CASE 
        WHEN SAFE_DIVIDE(Current_Inventory, Quantity) < 1.0 THEN 'CRITICAL: STOCK OUT'
        WHEN SAFE_DIVIDE(Current_Inventory, Quantity) BETWEEN 1.0 AND 1.3 THEN 'WARNING: LOW STOCK'
        ELSE 'HEALTHY'
    END AS Inventory_Status
FROM 
    `ins-optimizer.salesinventory.SI analysis`
ORDER BY 
    Stock_to_Sales_Ratio ASC;
```

**How the ratio works:**
- **< 1.0** → Current inventory cannot cover one month of sales → `CRITICAL: STOCK OUT`
- **1.0 – 1.3** → Less than 1.3 months of cover → `WARNING: LOW STOCK`
- **> 1.3** → Sufficient stock on hand → `HEALTHY`

Ordering by `Stock_to_Sales_Ratio ASC` surfaces the most at-risk parts first.

---

## Tableau Dashboard

**[Saskatchewan Branch Health Map](https://public.tableau.com/app/profile/joshua.manoj/viz/SaskatchewanRegionalInventoryRiskReport-Q12026/SaskatchewanBranchHealthMap)**

The dashboard provides:
- **Branch Health Map** — geographic view of inventory status across Saskatchewan locations
- **Risk Status Breakdown** — CRITICAL / WARNING / HEALTHY classification by branch and part
- **Stock-to-Sales Ratio Rankings** — sortable table showing highest-risk parts first
- **Revenue and Profit Context** — financial impact of at-risk inventory items

---

## Key Findings

- Multiple Saskatchewan branches showed WARNING or CRITICAL status across high-revenue parts
- Stock-to-Sales ratios below 1.0 identified specific parts requiring immediate restocking
- The 2-week lead time built into the WARNING threshold gives operations managers actionable advance notice before stockouts occur

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Google BigQuery (SQL) | Data querying, ratio calculation, status classification |
| Tableau Public | Interactive dashboard and geographic visualization |
| Excel / CSV | Data preparation and validation |

---

## Files in This Repository

| File | Description |
|------|-------------|
| `Sales_Inventory_Analysis.csv` | Processed dataset with Stock-to-Sales ratios and inventory status |
| `sales_dataset.csv` | Raw sales transaction data used for analysis |
| `README.md` | Project documentation |

---

## Author

**Joshua Manoj**  
Data Analyst | Google Data Analytics Certified  
[LinkedIn](https://linkedin.com/in/joshua-manoj) · [Tableau Public](https://public.tableau.com/app/profile/joshua.manoj)
