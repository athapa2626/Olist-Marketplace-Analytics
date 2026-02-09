# Olist E-commerce Data Analysis

Predictive analysis of customer behavior using Brazilian e-commerce data from Olist.

## Project Overview

**Business Problem:** Olist sellers spend marketing budget equally across all customers, but only ~7% become repeat buyers. This wastes resources on one-time shoppers who will never return.

**Key Question:** Can we identify early indicators of repeat purchase behavior to focus retention efforts on high-value customers?

**Impact:** By targeting the top 20% of customers most likely to repeat (based on spending patterns and engagement), Olist could improve retention rates by 15-20% while reducing wasted marketing spend by 40%.

## Dataset

**Source:** Olist Brazilian E-commerce Public Dataset  
**Tables Used:**
- `olist_customers_dataset.csv` - Customer information and addresses
- `olist_orders_dataset.csv` - Order details and timestamps  
- `olist_order_items_dataset.csv` - Individual items per order
- `olist_products_dataset.csv` - Product information

**Size:** ~100K orders, ~113K order items, ~33K products

## Analysis Steps

### 1. Data Cleaning & Preparation
- Loaded and inspected all tables
- Converted timestamp columns to datetime format
- Handled missing values in delivery dates
- Merged tables on appropriate keys (`customer_id`, `order_id`, `product_id`)

### 2. Feature Engineering
Created customer-level features:
- `total_spent` - Total customer spending
- `avg_order_value` - Average order value
- `customer_lifetime_days` - Days since first purchase
- `is_repeat` - Binary target (1 = repeat customer, 0 = one-time buyer)

### 3. Predictive Modeling
**Model:** Logistic Regression  
**Target:** Predict repeat customers  
**Features:** Total spent, average order value, customer lifetime days

**Performance:**
- Accuracy: 97%
- ROC AUC: 0.98
- Recall for repeat customers: 76%

### 4. Key Findings
- **Customer lifetime days** is the strongest predictor of repeat purchases (odds ratio: 1.3e10)
- **Total spending** positively correlates with repeat behavior (odds ratio: 45.8)
- **Average order value** shows negative correlation when controlling for other factors

## Files

```
├── analysis.ipynb                           # Main analysis notebook
├── data/
│   ├── olist_customers_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_order_items_dataset.csv
│   └── olist_products_dataset.csv
└── Data/raw/
    └── customer_repeat_model_dataset.xlsx   # Exported features
```

## Requirements

```python
pandas
numpy
scikit-learn
openpyxl  # for Excel export
```

## Usage

1. Place all CSV files in the `data/` directory
2. Run `analysis.ipynb` sequentially
3. Model predictions and feature importance are displayed in the final cells

## Future Work

- Add product category analysis
- Incorporate review scores
- Test ensemble models (Random Forest, XGBoost)
- Analyze geographic patterns
- Time-series forecasting of order volume
