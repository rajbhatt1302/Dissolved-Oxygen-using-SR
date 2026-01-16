# Dissolved Oxygen (DO) Prediction using Symbolic Regression

## Overview

This project uses **Symbolic Regression** to find a mathematical equation that estimates Dissolved Oxygen (DO) levels in water bodies. Instead of a "black box" model (like a neural network), this approach generates a readable formula (e.g., `y = 2*x0 + 0.5*x1`), allowing us to understand the physical relationship between the inputs and DO.

## Input Variables

The model uses two remote sensing indices as inputs:

- **x0**: NDVI (Normalized Difference Vegetation Index) 
- **x1**: n-wst (Normalized Water Surface Temperature) 

**Target Variable**:

- **y**: Dissolved Oxygen (DO) in ppm.

## Scaling Approach (Crucial Step)

Before finding the equation, we process the data using **Robust Scaling**.

### Why do we scale?

Raw data values can vary wildly (e.g., NDVI might be small, while temperature is large). If we don't scale, the algorithm(s) might bias itself.
## Output

- **Symbolic Regression**:
  - **Equations**: List of candidate equations.
  - **Best Model**: Best equation.
  - **Predictions**: `predicted_DO.csv.
- **RF & SVR**:
  - **Hyperparameters**: Saved to `best_rf_hyperparameters.csv` and `best_svr_hyperparameters.csv`.
  - **Predictions**: `rf_test_predictions.csv` and `svr_test_predictions.csv`.
