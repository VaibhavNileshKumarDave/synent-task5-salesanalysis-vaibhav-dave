# Task 5 — Sales Data Analysis Report

## Objective
Analyze 4 years of transactional sales data from a US-based Superstore
to identify monthly revenue trends, top-selling products, and
profitability patterns across categories, regions, and customer segments.
The goal is to surface actionable business insights that can help
management make better decisions around inventory, discounting, and
regional strategy.

## Dataset
Two datasets were used and merged for this analysis:

| File                  | Source  | Rows  | Key Columns                                      |
|-----------------------|---------|-------|--------------------------------------------------|
| train.csv             | Kaggle  | 9,800 | Order Date, Ship Date, Product Name, Customer ID, Sales |
| SampleSuperstore.csv  | Kaggle  | 9,994 | Profit, Discount, Quantity, Category, Region     |

Why two datasets?
train.csv contained time and product columns needed for trend analysis,
while SampleSuperstore.csv contained Profit, Discount, and Quantity
columns needed for profitability analysis. Neither dataset alone was
complete for this task, so both were merged on 10 common columns:
Ship Mode, Segment, Country, City, State, Postal Code, Region,
Category, Sub-Category, and Sales.

Final merged dataset: 9,801 rows × 24 columns
Date range: January 2015 to December 2018
Coverage: 48 US states, 4 regions, 3 categories, 1,848 unique products

## Steps Performed

### Phase 1 — Data Loading and Inspection
1. Loaded both CSV files using pandas with latin1 encoding
2. Performed initial inspection — df.head(), df.info(), df.describe()
3. Checked dataset shapes and column names before merging

### Phase 2 — Data Merging
4. Identified 10 common columns shared between both datasets
5. Merged using left join on common columns to retain all train.csv rows
6. Verified merge quality — only 11 rows had null Profit after merge
   (0.1% of total data — acceptable loss)

### Phase 3 — Data Cleaning
7. Dropped 11 rows with null Profit values (post-merge unmatched rows)
8. Converted Order Date and Ship Date from string to datetime format
9. Checked for and confirmed no duplicate rows
10. Verified all column data types after cleaning

### Phase 4 — Feature Engineering
11. Extracted Month column from Order Date (Period format for grouping)
12. Extracted Year column from Order Date (integer)
13. Computed Profit Margin % = (Profit / Sales) × 100 as a new column

### Phase 5 — Core Analysis

#### Monthly Revenue Trends
14. Grouped data by Month and summed Sales
15. Sorted chronologically and plotted as a line chart
16. Identified seasonal revenue peaks and flat periods

#### Top Products by Sales
17. Grouped by Product Name and summed total Sales revenue
18. Sorted descending and extracted top 10 products
19. Plotted as a horizontal bar chart ranked by revenue

#### Profit Analysis
20. Computed profit margin % by Region — sorted and plotted bar chart
21. Computed profit margin % by Category — sorted and plotted bar chart
22. Computed profit margin % by Segment — sorted and plotted bar chart
23. Built pivot table: Region × Category (profit values) → heatmap
24. Built pivot table: Region × Segment (profit values) → heatmap
25. Plotted Discount vs Profit scatter chart colored by Category
    to identify the discount tipping point

### Phase 6 — Insights and Reporting
26. Wrote business insight after every chart
27. Compiled Key Business Takeaways section summarizing 5 major findings

## Tools Used
Python, Pandas, Matplotlib, Seaborn, Jupyter Notebook

## Charts Produced

| Chart                              | File                        | Type         |
|------------------------------------|-----------------------------|--------------|
| Monthly Revenue Trends             | monthly_revenue.png         | Line chart   |
| Top 10 Products by Sales           | product_by_sale_count.png   | Bar chart    |
| Region by Profit Margin            | region_profit.png           | Bar chart    |
| Category by Profit Margin          | category_profit.png         | Bar chart    |
| Segment by Profit Margin           | segment_profit.png          | Bar chart    |
| Region × Category Heatmap          | Heatmap_pivot1.png          | Heatmap      |
| Region × Segment Heatmap           | Heatmap_pivot2.png          | Heatmap      |
| Discount vs Profit by Category     | discount_vs_profit.png      | Scatter plot |

## Key Results

### Overall Numbers
| Metric                  | Value        |
|-------------------------|--------------|
| Total Sales (4 years)   | $2,253,417   |
| Total Profit (4 years)  | $276,962     |
| Overall Profit Margin   | 12.29%       |
| Unique Products         | 1,848        |
| States Covered          | 48           |

### Monthly Revenue Trends
Revenue consistently peaks every year in September, then drops slightly
in October, and rises again sharply in November and December. Q4
(October to December) accounts for a disproportionately large share of
annual revenue every single year across the full 4-year period.
January to August remains relatively flat and low in comparison.

### Top Products by Sales
| Rank | Product                                | Total Sales |
|------|----------------------------------------|-------------|
| 1    | Canon imageCLASS 2200 Advanced Copier  | $61,600+    |
| 2–10 | Other products                         | $15K – $30K |

The Canon imageCLASS 2200 Advanced Copier generates more than double
the revenue of the second-highest product — a clear outlier and
flagship product for the business.

### Profit Analysis by Category
| Category        | Profit Margin |
|-----------------|---------------|
| Technology      | 17.28%        |
| Office Supplies | 16.83%        |
| Furniture       | 2.17%         |

Furniture is a near-breakeven category despite significant sales volume.

### Profit Analysis by Region
| Region  | Profit Margin |
|---------|---------------|
| West    | 14.83%        |
| East    | 13.22%        |
| South   | 11.90%        |
| Central | 7.69%         |

Central region significantly underperforms all other regions.

### Heatmap Finding
Furniture in the Central region generates a net negative profit
of -$3,211 — the only loss-making combination across all
Region × Category intersections in the dataset.

### Discount vs Profit
Transactions with discounts up to 20% are generally profitable.
Discounts at 30% or above almost universally result in net losses
across all three categories. Furniture is the most discount-sensitive
category — even moderate discounts push it into loss territory due
to its already thin base margin.

## Business Recommendations
1. Cap all standard discounts at 20% immediately — the data shows a
   hard tipping point beyond which profitability collapses

2. Audit Furniture in the Central region — this is the only
   combination generating a net loss and needs immediate management
   attention on pricing, shipping costs, or catalog reduction

3. Front-load Q4 inventory and marketing budgets — September,
   November, and December consistently drive the majority of
   annual revenue every year

4. Prioritize Technology and Office Supplies — both deliver
   16–17% profit margins consistently across all regions

5. Protect Canon imageCLASS 2200 stock levels — this single
   product generates over $61K in sales, more than double any
   other product. Stockouts would be disproportionately costly