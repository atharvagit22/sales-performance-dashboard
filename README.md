# Sales Insights Dashboard: MySQL + Power BI

An end-to-end sales analytics project that takes raw sales data from MySQL, cleans and models it in Power BI, and delivers an interactive 3-page dashboard for tracking revenue, profit margin, and market and customer performance.

**Tools:** MySQL · SQL · Power BI Desktop (Power Query, DAX, Data Modelling)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Business Questions](#business-questions)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Approach](#approach)
- [Dashboard Pages](#dashboard-pages)
- [Key Insights](#key-insights)
- [Recommendations](#recommendations)
- [How to Use This Project](#how-to-use-this-project)
- [Repository Structure](#repository-structure)
- [Skills Demonstrated](#skills-demonstrated)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Project Overview

Sales teams often have plenty of data but struggle to answer simple questions quickly: *How are we doing? Where is the money coming from? Are we actually profitable in the markets where we sell the most?*

This project solves that by building a complete analytics pipeline. Raw transactional data is stored in **MySQL**, explored and validated with **SQL**, cleaned and modelled in **Power BI**, and presented through a **3-page interactive dashboard** that decision-makers can filter by year, date, market, customer and product.

## Business Problem

A sales organisation operating across multiple markets and customers needs a single, reliable view of its performance. The data contains transactions in more than one currency (INR and USD), which makes revenue difficult to compare. Leadership also wants to know whether high-revenue markets are also high-profit markets, and which markets are meeting their profit-margin targets.

The goal of this project is to turn raw sales records into clear, actionable insight that supports faster and better business decisions.

## Business Questions

- What are our total revenue and sales quantity, and how are they trending?
- Which markets and customers drive the most revenue?
- Do the markets that bring in the most revenue also contribute the most profit?
- How does revenue compare with the previous year?
- Which markets are meeting or missing their profit-margin target?

## Dataset

The data is a relational sales database in MySQL made up of the following tables:

| Table | Description |
|---|---|
| `transactions` | Fact table with one row per sale: product, customer, market, date, quantity, amount, currency and cost |
| `customers` | Customer names and customer type |
| `products` | Product codes and product type |
| `markets` | Market names and the zone they belong to |
| `date` | Calendar table with year, month and date attributes |
| `profit_target` | Target profit-margin % set for each market |

## Project Workflow

```
MySQL (raw data)
      │
      ▼
SQL exploration & validation
      │
      ▼
Power BI: Power Query (cleaning, USD → INR conversion)
      │
      ▼
Star schema data model
      │
      ▼
DAX measures
      │
      ▼
3-page interactive dashboard
```

## Approach

### 1. SQL Exploration

Before building anything in Power BI, I explored and validated the data directly in MySQL to understand its structure and quality.

- Filtered records to inspect specific years, markets and customers
- Joined the transactions table with customer, product, market and date tables
- Aggregated revenue and quantity by **year, month and market**
- Checked for duplicates, null values and unusual amounts (such as zero or negative sales)
- Cross-checked SQL totals against Power BI totals to confirm the model was accurate

### 2. Data Cleaning in Power Query

- Imported the MySQL tables into Power BI Desktop
- Standardised data types (dates, numbers and text)
- Removed duplicate and invalid records
- **Converted USD transactions to INR** so that all revenue sits on one comparable currency
- Created a normalised revenue column used across all visuals
- Removed unused columns to keep the model light and fast

### 3. Data Modelling

Built a **star schema** to keep the model clean and performant:

- **Fact table:** Sales transactions
- **Dimension tables:** Customer, Product, Market, Date
- **Supporting table:** Profit Target (linked to Market)

One-to-many relationships flow from each dimension into the fact table, with filters passing in a single direction. A dedicated date table supports time-intelligence calculations.

### 4. DAX Measures

Reusable measures keep the report consistent and easy to maintain:

```DAX
Revenue = SUM(Sales[Normalised Amount])

Sales Quantity = SUM(Sales[Sales Qty])

Profit Margin = SUM(Sales[Profit])

Profit Margin % = DIVIDE([Profit Margin], [Revenue])

Revenue Contribution % =
DIVIDE([Revenue], CALCULATE([Revenue], ALL(Markets)))

Profit Margin Contribution % =
DIVIDE([Profit Margin], CALCULATE([Profit Margin], ALL(Markets)))

Revenue LY =
CALCULATE([Revenue], SAMEPERIODLASTYEAR('Date'[Date]))

Target Difference = [Profit Margin %] - [Target Profit Margin %]
```

## Dashboard Pages

### 1. Key Insights

<img width="1015" height="637" alt="Key Insights page" src="https://github.com/user-attachments/assets/b2acd376-61ea-459c-80a1-420ba9c5d254" />

A high-level snapshot of overall business health.

- **KPI cards:** Revenue, Sales Quantity, Total Customers, Total Markets
- **Revenue trend** over time
- **Revenue by market** and **revenue by customer**
- **Year and date slicers** to explore any period

### 2. Profit Analysis

<img width="1020" height="638" alt="Profit Analysis page" src="https://github.com/user-attachments/assets/c464e11d-76f7-4960-9837-6be6b11ae2d8" />

Compares where revenue comes from with where profit comes from.

- **Revenue contribution % vs profit margin contribution %** by market
- **Profit margin % by market**
- **Top 5 Customers** table

### 3. Performance Insights

<img width="1022" height="640" alt="Performance Insights page" src="https://github.com/user-attachments/assets/04f95b24-44b1-44f7-9d19-7ae55b730423" />

Tracks performance against the previous year and against targets.

- **Revenue vs last year** alongside profit margin %
- **Profit margin** by market, customer, product and zone
- **Adjustable profit-target slicer** to see which markets meet or miss the target

## Key Insights

- A small number of markets generate the majority of total revenue, showing a high concentration of sales.
- The top revenue-generating market is not always the top profit-generating market, so revenue alone does not show true performance.
- Some high-revenue markets fall below the profit-margin target, which points to cost or pricing issues.
- A handful of customers account for a large share of total revenue, which creates dependency risk.
- Year-over-year comparison highlights which periods grew and which declined, helping to spot seasonality.

## Recommendations

- Focus on improving margins in markets that bring in high revenue but low profit.
- Review pricing and cost structure in markets that miss the profit-margin target.
- Strengthen relationships with top customers while working to diversify the customer base.
- Use the target slicer regularly to monitor performance and set realistic goals per market.

## How to Use This Project

1. **Clone the repository**
```bash
   git clone https://github.com/atharvagit22/your-repo-name.git
```
2. **Set up the database:** import the provided SQL dump file into MySQL.
3. **Run the SQL queries** in the `sql/` folder to explore the data.
4. **Open the Power BI file** (`.pbix`) in Power BI Desktop.
5. **Update the data source** to point to your local MySQL server if needed, then click **Refresh**.

**Requirements:** MySQL Server and Workbench · Power BI Desktop (free)

## Repository Structure

```
├── sql/
│   ├── db_dump.sql
│   └── analysis_queries.sql
├── powerbi/
│   └── sales_insights_dashboard.pbix
├── images/
│   ├── key_insights.png
│   ├── profit_analysis.png
│   └── performance_insights.png
└── README.md
```

## Skills Demonstrated

- **SQL:** joins, filtering, aggregations, data validation
- **Power Query:** data cleaning, transformation, currency conversion
- **Data Modelling:** star schema, relationships, date table
- **DAX:** calculated measures, time intelligence, contribution %
- **Dashboard Design:** KPI cards, slicers, interactive visuals, clear layout
- **Business Analysis:** turning data into insights and recommendations

## Future Improvements

- Add forecasting to predict future revenue
- Add row-level security so each region sees only its own data
- Schedule automatic data refresh through Power BI Service
- Add drill-through pages for customer and product detail
- Extend the analysis with customer segmentation

## Author

**Atharva Lambde**

[LinkedIn](https://www.linkedin.com/in/atharva-lambde/) · [GitHub](https://github.com/atharvagit22) · atharvalambde@gmail.com

If you found this project useful, feel free to give it a ⭐
