# Demand Forecasting & Inventory Optimization

A machine learning and time series analytics project that predicts sales demand and forecasts future inventory needs, helping businesses reduce overstocking and stockouts.

## Problem Statement

Many companies struggle with inventory forecasting — inaccurate stock levels caused by legacy practices, obsolete approaches, and unpredictable demand patterns and surges. This project identifies sales demand patterns and builds models to optimize inventory levels and minimize overstocking.

## Key Results

**Regression Models — "What drives sales quantity?"**

| Model | Features | Train R² | Test R² |
|-------|----------|----------|---------|
| Linear Regression | Stock Level | 0.348 | 0.348 |
| Random Forest | Stock Level | 0.354 | 0.343 |
| Linear Regression | Stock Level + Category + Order Qty | 0.348 | 0.348 |
| XGBoost | All 16 features | 0.507 | 0.308 |
| XGBoost (tuned) | All 16 features | 0.356 | 0.346 |

**Time Series Models — "What will demand be next month?"**

| Model | MAE | RMSE | MAPE |
|-------|-----|------|------|
| **ARIMA(1,0,0)** | 4,978 units | 5,494 units | **1.2%** | ✅ Best model |
| SARIMA(1,0,0)(0,0,1,12) | 13,941 units | 14,071 units | 3.3% |

**Top finding:** Stock Level is the dominant driver of sales — validated three ways (correlation 0.59, flat EDA averages for all other features, and 79.6% XGBoost feature importance). All regression models plateaued at ~35% Test R², while the ARIMA time series model delivered most accurate 3-month-ahead demand forecasts.

## Dataset

Sourced from https://www.kaggle.com/code/jijagallery/retail-store-inventory-forecasting 

## Methodology

1. **Data Cleaning & EDA** - Handled partial-month data, explored demand patterns (weather, seasonality, and category)
2. **Regression Models** - Linear Regression → Random Forest → XGBoost to predict daily Sales Qty
3. **Time Series Forecasting** - ARIMA and SARIMA to forecast monthly demand, validated with a 21-month train / 3-month test split
4. **Business Recommendations** - Add in Safety stock, supplier lead time features and accumulate more data to re-train models 


## Repository Contents

| File | Description |
|---|---|
| [`Demand_forecasting.ipynb`](Demand_forecasting.ipynb) | Full analysis — EDA, regression models, time series forecasting models |
| [`Retail Inventory & Sales Performance Dashboard.pbix`](<Retail Inventory & Sales Performance Dashboard.pbix>) | Interactive Power BI dashboard (sales value, inventory value, stock coverage) |
| [`Inventory and Sales performance Dashboard.jpg`](<Inventory and Sales performance Dashboard.jpg>) | Dashboard preview screenshot |
| [`Demand forecasting case study.pdf`](<Demand forecasting case study.pdf>) | Presentation deck summarizing the project |
| [`retail_store_inventory.csv`](retail_store_inventory.csv) | Source dataset |


## Limitations

This dataset is synthetic, which inflates forecast accuracy (near-zero decomposition residuals) compared to real-world data, where MAPE typically runs 10–30%. With only 24 months of history, SARIMA's seasonal component had insufficient data to learn reliable patterns. 

[Connect with me on LinkedIn](https://www.linkedin.com/in/jelin-foo-yq/)
