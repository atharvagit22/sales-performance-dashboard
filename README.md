# Sales Insights Dashboard: MySQL + Power BI

An end-to-end sales analytics project that takes raw sales data from MySQL, cleans and models it in Power BI, and delivers an interactive 3-page dashboard for tracking revenue, profit margin and market and customer performance.

**Tools:** MySQL · SQL · Power BI Desktop (Power Query, DAX, Data Modelling)

---

## Business Questions

- What are our total revenue and sales quantity, and how are they trending?
- Which markets and customers drive the most revenue?
- Do the markets that bring in the most revenue also contribute the most profit?
- How does revenue compare with the previous year?
- Which markets are meeting or missing their profit-margin target?

## Approach

- **SQL:** explored and validated the sales data in MySQL using filters, joins and aggregations (revenue by year, month and market).
- **Data cleaning:** cleaned the data in Power Query, including converting USD transactions to INR so all revenue is comparable.
- **Data model:** built a star schema with a sales fact table and customer, product, market and date dimensions, plus a profit-target table.
- **DAX:** created reusable measures for revenue, profit margin, contribution %, last-year revenue and target difference.

## Dashboard Pages

**1. Key Insights**
<img width="1015" height="637" alt="image" src="https://github.com/user-attachments/assets/b2acd376-61ea-459c-80a1-420ba9c5d254" />

KPI cards (Revenue, Sales Quantity, Total Customers, Total Markets), revenue trend, and revenue by market and customer, with year and date slicers.

**2. Profit Analysis**
<img width="1020" height="638" alt="image" src="https://github.com/user-attachments/assets/c464e11d-76f7-4960-9837-6be6b11ae2d8" />

Revenue contribution % vs profit margin contribution % by market, profit margin % by market, and a Top 5 Customers table.

**3. Performance Insights**
<img width="1022" height="640" alt="image" src="https://github.com/user-attachments/assets/04f95b24-44b1-44f7-9d19-7ae55b730423" />

Revenue vs last year with profit margin %, profit margin by market, customer, product and zone, and an adjustable profit-target slicer.


<!-- Add screenshots: ![Key Insights](images/key_insights.png) -->

## Skills Demonstrated

SQL · Power Query · Data Modelling · DAX · Dashboard Design · Business Analysis

## Author

**Atharva Lambde**
[LinkedIn](https://www.linkedin.com/in/atharva-lambde/) · [GitHub](https://github.com/atharvagit22) · atharvalambde@gmail.com
