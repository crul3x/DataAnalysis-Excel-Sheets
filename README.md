# Sales Performance Analysis - 2023

## AI Transparency Statement

This project was built with AI assistance as an intentional part of the workflow.

This reflects a real and growing skill in modern data work - knowing how to use AI tooling effectively, direct it toward the right outputs, and understand the decisions behind the data. Every analytical decision (null handling strategy, date standardization, derived column logic, chart selection) was deliberately chosen and is documented in the Data Cleaning Log sheet.

---

A end-to-end data analytics project covering data cleaning, exploratory analysis, pivot-style summary tables and charts, and an interactive web dashboard built using AI assistance.

---

## Project Overview

This project analyzes 1,200 fictional sales transactions recorded across Jan-Dec 2023, spanning 4 regions, 6 products (15 SKUs), 6 sales representatives, and 3 customer segments.

The goal was to simulate a realistic analyst workflow - from receiving a raw, messy dataset all the way through to a polished, interactive dashboard while documenting every decision made along the way.

### Business Questions

1. Which region generates the most revenue, and how evenly distributed is performance across regions?
2. Which products and SKUs are driving the majority of revenue?
3. How does revenue trend across months and quarters throughout the year?
4. Which sales representatives are the top and bottom performers, and by how much do they differ?
5. Which customer segments contribute most to overall revenue?

---

## Dataset

| Property | Detail |
|---|---|
| Source | Synthetically generated (Python) |
| Rows | 1,200 transactions |
| Columns | 10 (original) -> 14 (after cleaning) |
| Period | January - December 2023 |
| Products | Laptop, Tablet, Monitor, Printer, Keyboard, Mouse |
| SKUs | 15 (2-3 per product, each with a fixed price tier) |
| Regions | North, South, East, West |
| Sales Reps | Amit, Sara, John, Priya, Rahul, Neha |
| Segments | Consumer, Corporate, Home Office |

### Quality Issues
- Mixed date formats (4 formats: `DD/MM/YYYY`, `DD Mon YYYY`, `YYYY-MM-DD`, `MM-DD-YYYY`)
- Inconsistent casing across Region, Category, and Customer Segment columns
- 145 missing Quantity values (~12.1% of rows)

---

## Process Walkthrough

### 1. Data Cleaning
All cleaning decisions were documented in the **Data Cleaning Log** sheet before being applied. Key decisions:

- **Casing** - standardized Region, Category, and Customer Segment using `PROPER(TRIM())`
- **Dates** - unified 4 formats into `DD/MM/YYYY` using `DATEVALUE()` with a helper column
- **Missing Quantity** - filled with median per product group. Dropping 145 rows (12.1%) was too significant; filling with 1 would understate revenue. Median per product is statistically defensible.
- **Derived columns** - added `Revenue` (Quantity × Unit_Price), `Month`, `Month_Num`, `Quarter`
- **Product Reference Table** - built a 15-SKU lookup table used as an XLOOKUP source throughout the analysis

### 2. Exploratory Analysis
Summary statistics calculated across 5 dimensions: overall KPIs, revenue by region, revenue by product, revenue by month, and revenue by sales rep.

### 3. Analysis & Charts
5 paired sections - each with a summary table on the left and a corresponding chart on the right:
- Sales Rep Performance (horizontal bar)
- Regional Trends by Month (cross-tab + line chart)
- Product & SKU Breakdown (hierarchical table + stacked column)
- Customer Segment by Region (cross-tab + donut)
- Quarterly Performance (grouped table + column chart)

### 4. Interactive Dashboard
A standalone interactive dashboard built with AI assistance. Filterable by Region and Quarter, with live-updating KPI cards and 6 charts.

---

## Key Findings

- **Total Revenue: $1,063,326** across 1,200 orders with an average order value of **$886**
- **Laptops dominate** - contributing **52.1% of total revenue** ($554,490) despite being one of six products
- **East region leads** with $281,279 in revenue, but the four regions are remarkably balanced - the spread between highest and lowest is only ~$25,000, suggesting no region is being neglected
- **Q2 was the strongest quarter** at $302,709, with August being the single highest revenue month at $107,629
- **Rahul is the top sales rep** at $202,100 - 38.6% more than the lowest performer, Amit, at $145,851. This gap is worth investigating for coaching or territory review
- **Consumer segment leads** with 34.7% of revenue ($368,747), narrowly ahead of Corporate and Home Office which are closely matched

---

## How to View the Dashboard

**Option 1 - Live link (GitHub Pages)**
[https://crul3x.github.io/DataAnalysis-Excel-Sheets/](https://crul3x.github.io/DataAnalysis-Excel-Sheets/)

---

*Dataset is synthetic and does not represent any real company or individuals.*
