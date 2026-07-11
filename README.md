# 🥃 Vendor Sales Performance Analysis

**End-to-end data analysis project** identifying underperforming vendors and brands, optimizing purchase strategy, and uncovering pricing/promotional opportunities for a beverage distribution business — using **Python (Pandas, SQL, Seaborn, SciPy)** and **Power BI**.

[![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas)](https://pandas.pydata.org/)
[![SQLite](https://img.shields.io/badge/SQL-SQLite3-07405E?logo=sqlite)](https://www.sqlite.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi)](https://powerbi.microsoft.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📌 Table of Contents
- [Overview](#-overview)
- [Business Problem](#-business-problem)
- [Dataset](#-dataset)
- [Tools & Technologies](#-tools--technologies)
- [Project Workflow](#-project-workflow)
- [Dashboard](#-dashboard)
- [Key Insights](#-key-insights)
- [Statistical Testing](#-statistical-testing)
- [Recommendations](#-recommendations)
- [Repository Structure](#-repository-structure)
- [How to Run](#-how-to-run)
- [Contact](#-contact)

---

## 📊 Overview

This project analyzes vendor and brand-level sales performance for a beverage (wine & spirits) distributor. It combines **SQL-based data extraction**, **Python EDA & statistical analysis**, and an interactive **Power BI dashboard** to answer core business questions around procurement efficiency, profitability, and inventory health.

The goal was to move beyond raw reporting and produce **actionable, data-backed recommendations** — the kind of analysis a business could actually act on to improve margins and reduce dead stock.

---

## ❓ Business Problem

A vendor's sales performance directly impacts profitability, inventory turnover, and purchasing strategy. This analysis was built to answer:

1. Which brands have **low sales but high profit margins**, and would benefit from promotional or pricing adjustments?
2. Which vendors and brands drive the **highest sales performance**?
3. Which vendors contribute most to **total purchase spend** (procurement concentration risk)?
4. Does **bulk purchasing** reduce unit cost, and what's the optimal order size?
5. Which vendors show **low inventory turnover**, indicating excess/slow-moving stock?
6. Is there a **statistically significant difference** in profit margins between top-performing and low-performing vendors?

---

## 🗂 Dataset

| Detail | Description |
|---|---|
| **Source** | Internal vendor/sales summary table (SQLite database) |
| **Records** | 10,692 rows (8,564 after data cleaning) |
| **Granularity** | Vendor → Brand level transactions |
| **Key Fields** | `VendorName`, `Brand`, `Description`, `PurchasePrice`, `ActualPrice`, `TotalPurchaseDollars`, `TotalSalesDollars`, `GrossProfit`, `ProfitMargin`, `StockTurnover`, `SalesToPurchaseRatio` |

**Data cleaning applied:** removed records with negative/zero gross profit, non-positive profit margin, and zero sales quantity to eliminate return/adjustment noise before analysis.

---

## 🛠 Tools & Technologies

- **Python** — Pandas, NumPy, Matplotlib, Seaborn, SciPy
- **SQL** — SQLite3 for querying and filtering raw vendor data
- **Statistics** — Hypothesis testing, confidence intervals (t-distribution)
- **Power BI** — Interactive executive dashboard
- **Jupyter Notebook** — Exploratory data analysis & reporting

---

## 🔄 Project Workflow

```
1. Data Extraction    → Queried vendor_sales_summary table from SQLite DB
2. Data Cleaning      → Removed inconsistent/negative-margin records
3. EDA                → Distribution plots, outlier detection, correlation heatmap
4. Business Analysis  → Grouped/aggregated metrics to answer 6 core questions
5. Statistical Test   → Confidence intervals comparing top vs. low vendor margins
6. Dashboard          → Built interactive Power BI dashboard for stakeholders
```

---

## 📈 Dashboard

An interactive **Power BI dashboard** was built to summarize vendor and brand performance for business stakeholders at a glance.

**Highlights captured on the dashboard:**
| Metric | Value |
|---|---|
| Total Sales | $441.41M |
| Total Purchase | $307.34M |
| Gross Profit | $134.07M |
| Profit Margin | 38.72% |
| Unsold Capital | $2.71M |

> 📁 See `Vendor_Sales_Performance_Dashboard.pdf` for the full dashboard export, including top vendors/brands by sales, purchase contribution %, and low-performing vendor/brand views.

---

## 🔍 Key Insights

**1. Promotional Opportunity Brands**
Identified **198 brands** with low total sales (bottom 15th percentile) but high profit margins (top 15th percentile) — strong candidates for promotional pushes or pricing repositioning rather than discontinuation.

**2. Top Performers**
- **Top vendor by sales:** Diageo North America Inc — $67.99M
- **Top brand by sales:** Jack Daniels No. 7 Black — $7.96M

**3. Procurement Concentration**
The **top 10 vendors account for 65.69%** of total purchase dollars, led by Diageo North America Inc alone at 16.3% — highlighting moderate supplier concentration risk.

**4. Bulk Purchase Economics**
Larger order sizes correlate with a **lower average unit purchase price** (~$16.38 for large orders vs. ~$18.96 for small orders), validating bulk-buying as a cost-saving lever — though the relationship isn't perfectly linear across all order sizes.

**5. Slow-Moving Inventory**
Vendors like **Alisa Carr Beverages, Highland Wine Merchants, and Park Street Imports** show stock turnover ratios below 1, indicating excess inventory and working-capital inefficiency tied up in slow-moving stock.

---

## 📐 Statistical Testing

To validate whether high-sales vendors are actually more profitable (or just bigger), a **95% confidence interval** comparison was run on profit margins:

| Segment | Mean Profit Margin | 95% CI |
|---|---|---|
| Top-performing vendors (sales ≥ 75th pct.) | 31.18% | (30.74%, 31.61%) |
| Low-performing vendors (sales ≤ 25th pct.) | 41.57% | (40.50%, 42.64%) |

**Finding:** Counter-intuitively, lower-sales-volume vendors operate at *higher* average margins — non-overlapping confidence intervals confirm this is statistically significant, not random noise. High-volume vendors likely compete on price/volume, while low-volume/niche brands sustain premium margins.

---

## ✅ Recommendations

- Launch **targeted promotions** for the 198 identified high-margin/low-visibility brands to unlock revenue upside without eroding margin.
- Diversify procurement away from top-3 vendors (32%+ of purchase spend) to reduce **supply chain concentration risk**.
- Set **minimum bulk-order thresholds** for high-volume SKUs to capture unit-cost savings.
- Run **liquidation or return-to-vendor programs** for the 10 lowest stock-turnover vendors to free up working capital.
- Treat high-margin/low-volume vendors as a **premium tier** — protect these relationships rather than optimizing them purely on volume.

---

## 📁 Repository Structure

```
vendor-sales-performance-analysis/
│
├── data/
│   └── vendor_sales_summary.csv          # Cleaned dataset used for analysis
│
├── notebooks/
│   └── vendor_performance_analysis.ipynb # Full EDA + statistical analysis
│
├── dashboard/
│   └── Vendor_Sales_Performance_Dashboard.pdf  # Power BI dashboard export
│
├── reports/
│   └── Vendor_Performance_Analysis.pdf   # Complete analysis write-up/notebook export
│
├── images/                               # Chart exports used in README (optional)
│
├── README.md
└── LICENSE
```

> 💡 Tip: Rename your uploaded files to match this structure before pushing — e.g. `vertopal_com_Vendor_Preformence_Analysis__2_.pdf` → `reports/Vendor_Performance_Analysis.pdf`. Clean, descriptive file names read as more professional to anyone browsing your repo.

---

## ▶️ How to Run

```bash
# Clone the repository
git clone https://github.com/<your-username>/vendor-sales-performance-analysis.git
cd vendor-sales-performance-analysis

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy

# Open the notebook
jupyter notebook notebooks/vendor_performance_analysis.ipynb
```

---

## 📬 Contact

**[Pravin Kumar Namdev]**
📧 pravin.bhu.stcomp@gmail.com | 🔗 [LinkedIn](https://linkedin.com/in/pravinnamdev) | 🌐 [Porfolio](github.com/25pravin)

⭐ If you found this project useful or interesting, consider giving it a star!
