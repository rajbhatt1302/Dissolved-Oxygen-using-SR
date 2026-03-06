# Dissolved Oxygen (DO) Prediction using Symbolic Regression

## Overview

This project uses **Symbolic Regression** to find a mathematical equation that estimates Dissolved Oxygen (DO) levels in water bodies. Instead of a "black box" model (like a neural network), this approach generates a readable formula (e.g., `y = 2*x0 + 0.5*x1`), allowing us to understand the physical relationship between the inputs and DO.

## Step 1: Finding Stable Pixels

Before calculating DO, we need to find stable land pixels to ensure data consistency. Use `find_stable_pixels.ipynb` as the first step.
The script analyzes a time series of Landsat images (Red, NIR, and LST bands along with a water mask) and calculates the Coefficient of Variation (CV) for all land pixels over time.
It pinpoints the most stable pixels with the lowest CV, providing their geographic coordinates, which can be useful for minimising residual noise.

## Input Variables

The model uses two remote sensing indices as inputs:

- **x0**: NDVI (Normalized Difference Vegetation Index)
- **x1**: n-wst (Normalized Water Surface Temperature)

**Target Variable**:

- **y**: Dissolved Oxygen (DO) in ppm.

## Scaling Approach (Crucial step)

### Symbolic Regression

For Symbolic Regression and Machine Learning in general, variable scaling is a critical pre-processing step. Scaling ensures that all features contribute proportionately to the model, preventing variables with larger magnitudes from dominating the learning process. It also helps gradient-based optimizations converge faster. Specifically for Symbolic Regression, we implement **Dynamic Scaling** to scale the data range while preserving natural data variability.

#### Scaling for $x_0$ (NDVI) & $x_1$ (n-WST)

- **Rationale**: Dynamically centers the variable's mean to mitigate systemic bias and expands its effective range (variance). This ensures the feature carries sufficient statistical weight in the search space.

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
