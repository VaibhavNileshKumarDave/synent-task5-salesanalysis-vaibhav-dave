# Task 5 — Sales Data Analysis
### Synent Technologies Data Analyst Internship

---

## Problem Statement

Retail businesses generate large volumes of transactional data but often struggle to extract actionable insights from it. This project analyzes 4 years of sales data from a fictional US-based Superstore to identify revenue patterns, top-performing products, and profitability drivers — with the goal of surfacing business decisions that can improve margins and reduce losses.

---

## Dataset Details

Two datasets were used and merged for this analysis:

| File | Source | Rows | Key Columns |
|---|---|---|---|
| `train.csv` | Kaggle — Superstore Sales | 9,800 | Order Date, Ship Date, Product Name, Customer info, Sales |
| `SampleSuperstore.csv` | Kaggle — Sample Superstore | 9,994 | Profit, Discount, Quantity, Category, Region |

**Why two datasets?** `train.csv` contains time and product columns needed for trend analysis, while `SampleSuperstore.csv` contains Profit and Discount columns needed for profitability analysis. Neither dataset alone was sufficient, so both were merged on 10 common columns (`Ship Mode`, `Segment`, `Country`, `City`, `State`, `Postal Code`, `Region`, `Category`, `Sub-Category`, `Sales`).

**Final merged dataset:** 9846 rows x 21 columns, covering orders from **January 2015 to December 2018** across **48 US states**, **4 regions**, **3 categories**, and **1,848 unique products**.

---

## Approach

```
1. Setup          →  Import libraries, load both CSVs
2. Data Cleaning  →  Fix date types, drop 11 null-profit rows, remove duplicates
3. Engineering    →  Extract Month, Year columns; compute Profit Margin %
4. Analysis       →  Monthly revenue trends, top products, profit by region/category/segment
5. Visualization  →  Line chart, bar charts, heatmaps, scatter plot
6. Insights       →  Business interpretation written after each chart
```

**Libraries used:** `pandas`, `matplotlib`, `seaborn`

---

## Key Results

### Overall Numbers
| Metric | Value |
|---|---|
| Total Sales (4 years) | $2,253,417 |
| Total Profit (4 years) | $276,962 |
| Overall Profit Margin | 12.29% |
| Unique Products | 1,848 |

### Monthly Revenue Trends
- Revenue consistently peaks in **September, November, and December** every year
- Mid-year months (Jan–Aug) show flat, lower revenue
- Q4 alone accounts for a disproportionate share of annual revenue, driven by holiday and year-end corporate buying

### Top Products by Sales
| Rank | Product | Total Sales |
|---|---|---|
| 1 | Canon imageCLASS 2200 Advanced Copier | $61,600 |
| 2–10 | Other products | $15,000 – $30,000 |

Canon imageCLASS 2200 generates more than **double** the sales of the next closest product — a clear flagship item.

### Profit Analysis — Category
| Category | Profit Margin |
|---|---|
| Technology | 17.28% |
| Office Supplies | 16.83% |
| Furniture | **2.17%** |

Furniture is a near-breakeven category despite significant sales volume.

### Profit Analysis — Region
| Region | Profit Margin |
|---|---|
| West | 14.83% |
| East | 13.22% |
| South | 11.90% |
| Central | **7.69%** |

Central region significantly underperforms, especially in Furniture (net loss of -$3,211).

### Discount vs Profit
- Discounts up to **20%** are generally profitable
- Discounts at **30% or above** almost universally result in net losses
- Furniture is the most discount-sensitive category — even moderate discounts push it into loss territory

---

## Business Recommendations

1. **Cap discounts at 20%** — the data shows a hard tipping point; anything above 30% is consistently unprofitable
2. **Audit Furniture in the Central region** — this combination is generating a net loss and needs immediate intervention
3. **Front-load Q4 inventory and marketing** — September, November, and December drive the majority of annual revenue
4. **Prioritize Technology and Office Supplies** — both categories deliver 16–17% margins consistently across all regions
5. **Protect the Canon imageCLASS 2200 stock** — this single product generates over $61K in sales; stockouts would be disproportionately costly

---

## Repository Structure

```
synent-task5-salesanalysis-vibhu/
│
├── data/
│   ├── train.csv
│   └── SampleSuperstore.csv
│
├── notebooks/
│   └── superstore_sales_analysis.ipynb
│
├── outputs/
│   ├── monthly_revenue.png
│   ├── product_by_sale_count.png
│   ├── region_profit.png
│   ├── category_profit.png
│   ├── segment_profit.png
│   ├── Heatmap_pivot1.png
│   ├── Heatmap_pivot2.png
│   └── discount_vs_profit.png
│
└── README.md
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/VaibhavNileshKumarDave/synent-task5-salesanalysis-vaibhav-dave

# 2. Install dependencies
pip install pandas matplotlib seaborn jupyter

# 3. Place datasets in the data/ folder
SampleSuperstore.csv: https://www.kaggle.com/datasets/bravehart101/sample-supermarket-dataset
train.csv: https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting

# 4. Open the notebook
jupyter notebook notebooks/superstore_sales_analysis.ipynb
```

---

## Author

**Vibhu** — Data Analyst Intern, Synent Technologies  
B.Tech Computer Engineering, LDRP-ITR, Gandhinagar (2027)  
Internship Submission — June 2026
