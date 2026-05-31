# 🐍 Superstore Python EDA

![Python](https://img.shields.io/badge/Tool-Python_3.x-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/Library-pandas-150458?style=flat&logo=pandas)
![matplotlib](https://img.shields.io/badge/Library-matplotlib-11557c?style=flat)
![seaborn](https://img.shields.io/badge/Library-seaborn-4EACD0?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## 📌 Project Overview

Full Exploratory Data Analysis (EDA) of the Superstore Sales dataset using Python. This notebook covers data loading, cleaning, statistical profiling, outlier detection, correlation analysis, and 10+ visualisations built with matplotlib and seaborn.

**Dataset:** 9,994 orders | US Retail Superstore | Jan 2014 – Dec 2017

---

## 📊 Dataset

- **Source:** [Kaggle — Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
- **File:** Sample - Superstore.csv (2.29 MB)
- **Shape:** 9,994 rows × 21 columns

---

## 📓 Notebook Structure

```
1. Data Loading & Initial Inspection
   - pd.read_csv(), df.shape, df.info(), df.head()
   - Check dtypes, missing values, duplicates

2. Data Cleaning
   - Convert Order Date / Ship Date to datetime
   - Create derived columns: Profit Margin %, Ship Days, Year, Month

3. Descriptive Statistics
   - df.describe() for all numeric columns
   - Mean vs median comparison (skewness detection)

4. Outlier Detection
   - IQR method: Q1, Q3, IQR bounds
   - Flag outliers in Sales and Profit columns
   - Visualise with boxplots

5. Distribution Analysis
   - Histograms for Sales, Profit, Discount, Quantity
   - KDE plots to show distribution shape

6. Correlation Analysis
   - df.corr() heatmap
   - Key finding: Discount vs Profit = -0.22

7. Category & Sub-Category Analysis
   - groupby aggregations
   - Bar charts: Sales and Profit by Category
   - Worst and best performing sub-categories

8. Regional Analysis
   - Sales and Profit by Region
   - Grouped bar charts

9. Time Series Analysis
   - Monthly revenue trend (2014-2017)
   - Year-over-Year growth comparison

10. Discount Impact Analysis
    - Scatter plot: Discount vs Profit
    - Box plots: Profit distribution by discount band
    - Key finding: >40% discount = consistent losses

11. Business Insights Summary
    - Written conclusions from each analysis section
```

---

## 📈 Visualisations

| Chart | Type | Key Insight |
|-------|------|-------------|
| Sales distribution | Histogram + KDE | Right-skewed, median far below mean |
| Profit boxplot | Boxplot | Many negative outliers |
| Discount vs Profit | Scatter + trendline | Clear negative correlation |
| Sales by Category | Horizontal Bar | Technology leads |
| Profit by Sub-Category | Diverging Bar | Tables biggest loss-maker |
| Monthly trend | Line Chart | Q4 peak each year |
| Correlation heatmap | Heatmap | Discount-Profit relationship visible |
| Profit by Region | Bar Chart | West most profitable |
| Ship Days distribution | Histogram | Most orders ship in 3-5 days |
| Discount bands vs Profit | Box Plot | >40% discount always loses money |

---

## 🔑 Key Python Code Snippets

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
df = pd.read_csv('Sample - Superstore.csv', encoding='latin-1')

# Derived columns
df['Order Date'] = pd.to_datetime(df['Order Date'])
df['Profit Margin %'] = (df['Profit'] / df['Sales']) * 100
df['Ship Days'] = (df['Ship Date'] - df['Order Date']).dt.days
df['Year'] = df['Order Date'].dt.year
df['Month'] = df['Order Date'].dt.month

# Category profitability
category_summary = df.groupby('Category').agg(
    Total_Sales=('Sales', 'sum'),
    Total_Profit=('Profit', 'sum'),
    Order_Count=('Order ID', 'count')
).reset_index()
category_summary['Profit_Margin_%'] = (
    category_summary['Total_Profit'] / category_summary['Total_Sales'] * 100
)

# Discount impact analysis
df['Discount Band'] = pd.cut(df['Discount'],
    bins=[-0.1, 0.1, 0.2, 0.3, 0.4, 0.5, 1.0],
    labels=['0-10%','10-20%','20-30%','30-40%','40-50%','50%+'])

discount_profit = df.groupby('Discount Band')['Profit'].mean()
```

---

## 💡 Key Findings

1. Sales are right-skewed — median ($54) far below mean ($230)
2. 18.7% of orders are loss-making, concentrated in Furniture
3. Discount-Profit correlation = -0.22 (moderate negative)
4. Orders with >40% discount have average negative profit
5. Technology category: 17.4% profit margin (best)
6. Tables sub-category: consistent losses in all regions
7. Q4 drives 32-35% of annual revenue — strong seasonality
8. West region: highest sales and most profitable

---

## 🛠️ Skills Demonstrated

- Python data manipulation with pandas
- Datetime parsing and feature engineering
- Statistical analysis: describe(), IQR outlier detection
- Correlation analysis with heatmaps
- Data visualisation: matplotlib, seaborn (10+ chart types)
- Business insight derivation from EDA
- Clean, documented Jupyter notebook structure

---
*Part of the 90-Day Data Analyst Career System | By Ravi Bathula*
