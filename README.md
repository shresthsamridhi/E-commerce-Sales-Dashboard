📊 Sales & Employee Performance Dashboard — Power BI
An end-to-end interactive Business Intelligence project built using Power BI Desktop, analyzing sales performance, product trends, employee efficiency, and customer distribution for a classic models retail business across 2003–2005.
This project focuses heavily on:
transforming raw relational data into meaningful business insights,
building clean, interactive dashboards with professional design,
writing reliable DAX measures with proper blank handling,
and designing a dashboard experience that is both analytical and visually intuitive.
---
📌 Project Workflow
```
Raw Relational Dataset (MySQL-style tables)
        ↓
Data Modeling & Relationships in Power BI
        ↓
Data Transformation via Power Query
        ↓
DAX Measures & Calculated Columns
        ↓
Dashboard Design & Visualization
        ↓
Interactivity, Slicers & Cross-Filtering
        ↓
Business Insights & KPI Reporting
```
---
📌 About the Dataset
The dataset is based on a company sales and order management system for a classic models retail business — covering vehicles like cars, motorcycles, planes, ships, trains, and trucks.
Table	Description
`employees`	Sales rep names, job titles, and reporting hierarchy
`customers`	Customer details including country and assigned sales rep
`orders`	Order dates, status, quantities ordered
`products`	Product names, product lines, buy price, MSRP
`productlines`	Product category descriptions
Time Period Covered: 2003 · 2004 · 2005
The data required careful modeling — tables were connected through relationships (customer ↔ orders ↔ products ↔ employees) before any analysis could begin.
---
📂 Project Structure
```
sales-dashboard-powerbi/
│
├── dashboard.pbix               # Main Power BI project file
│
├── screenshots/
│   ├── sales_dashboard.png
│   ├── employee_dashboard.png
│   └── orders_dashboard.png
│
└── README.md
```
---
🖥️ Dashboard Preview
Page 1 — Sales & Product Performance
![Sales Dashboard](screenshots/sales_dashboard.png)
Page 2 — Employee Performance Analysis
![Employee Dashboard](screenshots/employee_dashboard.png)
Page 3 — Orders & Product Analysis
![Orders Dashboard](screenshots/orders_dashboard.png)
---
🏗️ Phase 1 — Data Modeling & Power Query
Before building any visuals, the raw tables were connected and cleaned inside Power BI.
Relationships Built
Tables were linked using primary and foreign keys:
`orders` connected to `customers` via `customerNumber`
`customers` connected to `employees` via `salesRepEmployeeNumber`
`orders` connected to `products` via `productCode`
`products` connected to `productlines` via `productLine`
Power Query Transformations
Correct data types assigned to all columns (dates, numbers, text)
Extracted `Year`, `Month`, and `Month Name` from order date for time-based analysis
Removed any irrelevant or null-heavy columns
---
🏗️ Phase 2 — DAX Measures
All KPIs and calculations were built using DAX (Data Analysis Expressions).
Key Measures Written
Total Sales
```
Total Sales = SUMX(orders, orders[quantityOrdered] * orders[priceEach])
```
Total Profit
```
Total Profit = SUMX(orders, (orders[priceEach] - products[buyPrice]) * orders[quantityOrdered])
```
Profit %
```
Profit % = DIVIDE([Total Profit], [Total Sales], 0)
```
YoY Sales Growth
```
YoY Growth % = 
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date])),
    CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date])),
    0
)
```
Safe measures were used throughout to handle blank values and avoid division errors, ensuring visuals never broke on filtered or sparse data.
---
📄 Dashboard Pages
Page 1 — Sales & Product Performance Dashboard
This page gives a high-level overview of overall business performance.
KPI Cards:
Total Sales → $1.77M
Total Profit → $695.88K
Profit % → 39.29
Top Selling Product → 1992 Ferrari 360 Spider red
2004 Sales Goal Tracker → $0.43M achieved vs $0.28M goal (+54.97%)
Visuals:
Order Quantity Trend (2003–2005) — Bar Chart
Sales Distribution by Product Line — Pie Chart with tooltips
Product Line Performance Analysis — Treemap
Top 5 Selling Products — Horizontal Bar Chart
Lowest Performing Products — Horizontal Bar Chart
Customer Distribution Across Countries — Map Visual
Slicers: Year · Employee Name · Country · Product Line
---
Page 2 — Employee Performance Analysis Dashboard
This page focuses on individual sales rep performance over time.
Important Design Decision:
During development, it was observed that several employees had very limited order data — not enough to render meaningful trends or charts. Rather than showing misleading or near-empty visuals, the Employee Name slicer was configured to display only employees with sufficient sales records. This ensured that every visual on this page remained accurate and trustworthy.
KPI Cards:
Total Sales per Employee
Total Profit per Employee
Total Orders Handled
Total Quantity Sold
Visuals:
Monthly Sales Trend — Line Chart
Yearly Sales Performance — Area Chart
Employee Efficiency Analysis (Sales vs Orders) — Scatter Chart
Sales Growth Analysis (YoY %) — Line Chart
Top 5 Performing Employees — Treemap
Employee Performance Summary — Matrix Table
Slicers: Employee Name · Year (2003–2005)
---
Page 3 — Orders & Product Analysis Dashboard
This page provides a deeper product and category-level breakdown.
Visuals:
Sum of Sales by Product Line — Horizontal Bar Chart
Sum of Quantity Ordered by Product Line — Horizontal Bar Chart
Sum of Quantity Ordered by Product Name — Horizontal Bar Chart
Sum of Sales by Product Name — Horizontal Bar Chart
Sum of Sales by Year — Line Chart (2003 → 2004 → 2005)
---
✨ Key Business Insights
Classic Cars dominated revenue with 40.43% share of total product line sales ($3.8M overall)
1992 Ferrari 360 Spider red was the single best-selling product — $0.27M in sales, $53K in profit
Sales peaked in 2004 at $4.34M before declining significantly in 2005 to $1.77M
2004 exceeded its sales goal by +54.97% ($0.43M achieved vs $0.28M goal)
Gerard Hernandez ranked as the top-performing employee by total sales
Trains was the lowest performing product line at only $0.2M in sales
Faster-selling products tended to cluster in Classic Cars and Vintage Cars categories
---
✨ Features & Techniques Used
Feature	Detail
DAX Measures	Safe blank handling, DIVIDE(), SUMX(), SAMEPERIODLASTYEAR()
YoY Growth	Year-over-year percentage change calculated via DAX
Conditional Formatting	Applied to KPI cards and matrix tables
Tooltip Integration	Custom tooltip on pie chart showing product-level sales breakdown
Cross-Filtering	All visuals interact with each other dynamically
Slicers	Employee Name, Year, Product Line, Country
Data Modeling	Multi-table star schema with proper relationships
Power Query	Type casting, column extraction, data cleanup
Map Visual	Geographic customer distribution via Bing Maps
Dark Corporate Theme	Consistent professional dark UI across all pages
---
📊 Visuals Used
`KPI Cards` · `Line Charts` · `Area Charts` · `Scatter Charts` · `Pie Charts` · `Treemaps` · `Horizontal Bar Charts` · `Map Visual` · `Slicers` · `Matrix Table` · `KPI Trend Visuals`
---
🚀 How to Use
Download the `dashboard.pbix` file from this repository
Open it in Power BI Desktop (free to download)
Use the slicers to filter by Employee, Year, Country, or Product Line
Hover over visuals for tooltips and additional drill-through details
Click on any visual segment to cross-filter the entire dashboard
---
🛠️ Tools Used
Power BI Desktop
DAX (Data Analysis Expressions)
Power Query (M Language)
Bing Maps (for geographic visual)
---
🧠 Key Learning Outcomes
This project helped build understanding of:
how to model relational data inside Power BI before analysis,
why safe DAX measures matter when working with filtered or sparse data,
how slicer design decisions directly affect dashboard reliability,
and how business-oriented thinking improves the quality of insights beyond just building charts.
One of the most important decisions made during this project:
> Employees with insufficient data were excluded from the performance slicer — because showing incomplete data as if it were complete would have been misleading, not insightful.
---
Built as a hands-on learning project to understand real-world BI dashboard development using Power BI.
