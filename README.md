# Bike Order Value Prediction

## Project Overview
This project predicts total bike order value using product, order and
geographic characteristics.

The goal was to build an accurate regression model while maintaining a clear
separation between model selection and final evaluation on unseen data.

## Business Question
Can total order value be predicted from order quantity, bike characteristics
and location, and which variables contribute most strongly to those
predictions?

## Dataset
Target:
- total_price

Predictors:
- quantity
- model
- category_1
- category_2
- frame_material
- city
- state

Unit price was intentionally excluded because it would create near-direct
target leakage.

## Methodology

1. Exploratory data analysis
2. Linear Regression benchmark
3. Regression assumption diagnostics
4. Multicollinearity assessment
5. Outlier sensitivity analysis
6. Automated model comparison with PyCaret
7. XGBoost tuning and ensemble experiments
8. Cross-validation model selection
9. Final evaluation on an untouched 30% test set
10. Prediction-error and permutation-importance analysis

Cross-validation was used only for model selection.

The untouched test set was used only once to estimate generalisation
performance on unseen observations.

## Final Results

The original XGBoost regressor was selected as the final model configuration.

Performance on the untouched test set:

| Metric | Result |
|---|---:|
| R² | 0.911 |
| RMSE | 1,549 |
| MAE | 139 |
| RMSLE | 0.047 |

## Key Findings

- XGBoost substantially outperformed the Linear Regression benchmark.
- Hyperparameter tuning, stacking and voting did not improve performance.
- High-value orders were retained because they appear to represent legitimate
  premium or high-quantity transactions.
- Frame material, bike model and quantity were the strongest predictive
  drivers.
- Geographic variables contributed comparatively little predictive
  information.
- Prediction error was concentrated disproportionately among very high-value
  orders.

## Model Selection

Candidate models were compared using 5-fold cross-validation.

The original XGBoost model achieved the lowest cross-validated RMSE and was
selected before the untouched test set was evaluated.

## Limitations

- Product attributes contain overlapping information.
- The random split evaluates new orders from the same historical population.
- Performance on completely new bike models has not been directly tested.
- High-value orders remain substantially harder to predict.
- Geographic effects should not be interpreted causally.

## Tools

Python  
pandas  
scikit-learn  
XGBoost  
PyCaret  
statsmodels  
Matplotlib

## Repository

* `bike_order_value_prediction.ipynb` — complete analysis and modelling workflow
* `data/bike_orderlines_df.csv` — dataset used in the project
* `README.md` — project overview and results
* `requirements.txt` — Python dependencies
