# python-and-ML-project
# QuickCart Stockout Risk Prediction

Machine learning project to predict inventory stockout risk for QuickCart dark stores.

## Business Problem

QuickCart needs to identify whether a product at a specific store is:

- **Safe**: sufficient stock is available
- **At-Risk**: stock may become insufficient soon
- **Imminent**: stock may run out before the next supplier delivery

The goal is to help inventory teams prioritize reorders and reduce lost sales caused by stockouts.

## Dataset

The project uses five CSV files:

| File | Description |
|---|---|
| `dim_stores.csv` | Store information |
| `dim_skus.csv` | Product/SKU information |
| `dim_suppliers.csv` | Supplier reliability and lead-time details |
| `dim_events.csv` | Festival and promotion event calendar |
| `fact_inventory_daily.csv` | Daily inventory records and target variable |

Dataset details:

- 21,600 inventory records
- 12 stores
- 60 SKUs
- 15 suppliers
- October 2026 daily data
- Target: `stockout_risk`

## Key Steps

- Loaded and validated five datasets.
- Fixed inconsistent city display casing.
- Treated supplier reliability value `N/A` as missing.
- Joined store, SKU, supplier, event, and inventory data.
- Created features such as:
  - Reorder gap
  - Days-of-cover ratio
  - Stock utilization
  - Demand gap
  - Recent reorder flag
  - Festival and promotion indicators
  - Supplier reliability risk
  - Calendar features
- Used a time-based split:
  - Train: October 1-23, 2026
  - Test: October 24-30, 2026

## Models Used

- Majority-class baseline
- Logistic Regression
- Random Forest Classifier

## Model Performance

| Model | Accuracy | Imminent Precision | Imminent Recall | Imminent F1 |
|---|---:|---:|---:|---:|
| Majority Baseline | 62.3% | 0.0% | 0.0% | 0.0% |
| Logistic Regression | 79.5% | 44.2% | 99.4% | 61.1% |
| Random Forest | 92.7% | 90.8% | 60.0% | 72.3% |

Random Forest was selected as the final model because it achieved the strongest overall accuracy, precision, and Imminent F1-score.

## Key Insights

- Imminent stockout risk was higher during festival periods.
- Perishable products had greater stockout risk than non-perishable products.
- Days of cover, days-of-cover ratio, reorder gap, stock utilization, and closing stock were important predictors.
- Supplier reliability and lead-time variation also influenced stockout risk.

## Business Recommendations

- Immediately replenish products predicted as **Imminent**.
- Monitor **At-Risk** items and plan reorders early.
- Give additional attention to perishable products during festival and promotional periods.
- Monitor low-reliability suppliers and suppliers with variable lead times.
- Use prediction output to prioritize inventory action by SKU, store, and supplier.

## Project Structure

```text
QuickCart-Stockout-Risk/
│
├── data/
│   ├── dim_stores.csv
│   ├── dim_skus.csv
│   ├── dim_suppliers.csv
│   ├── dim_events.csv
│   └── fact_inventory_daily.csv
│
├── QuickCart_Stockout_Risk.ipynb
├── quickcart_stockout_model.pkl
├── quickcart_features.pkl
├── quickcart_model_predictions.csv
├── requirements.txt
└── README.md

for data sets feel free to ask
