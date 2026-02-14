# Dissolved Oxygen (DO) Prediction using Symbolic Regression

## Overview

This project uses **Symbolic Regression** to find a mathematical equation that estimates Dissolved Oxygen (DO) levels in water bodies. Instead of a "black box" model (like a neural network), this approach generates a readable formula (e.g., `y = 2*x0 + 0.5*x1`), allowing us to understand the physical relationship between the inputs and DO.

## Input Variables

The model uses two remote sensing indices as inputs:

- **x0**: NDVI (Normalized Difference Vegetation Index)
- **x1**: n-wst (Normalized Water Surface Temperature)

**Target Variable**:

- **y**: Dissolved Oxygen (DO) in ppm.

## Scaling Approach (Crucial step)

### Symbolic Regression

For Symbolic Regression, we use the **Rescaled Gaussian RBF** formula to scale input variables:
$$x_{scaled} = 2 \cdot \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) - 1$$
This transformation helps in identifying non-linear relationships while keeping the inputs within a normalized range.

### RF & SVR

Random Forest and Support Vector Regression models use **Standard Scaling** (`StandardScaler`) for input features. This is essential for SVR performance and ensures consistent feature magnitudes across models.

## Output

- **Symbolic Regression**:
  - **Equations**: List of candidate equations.
  - **Best Model**: Best equation.
  - **Predictions**: predicted_DO.csv.
- **RF & SVR**:
  - **Hyperparameters**: Saved to `best_rf_hyperparameters.csv` and `best_svr_hyperparameters.csv`.
  - **Predictions**: `rf_test_predictions.csv` and `svr_test_predictions.csv`.
