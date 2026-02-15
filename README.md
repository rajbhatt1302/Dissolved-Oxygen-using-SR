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

For Symbolic Regression, we implement **Bound-Safe Dynamic Centering** to ensure strict target ranges while preserving natural data variability:

#### 1. Dynamic Centering for $x_0$ (NDVI)

- **Target Range**: **$[-0.5, 1.0]$**
- **Method**: $x_{scaled} = \text{clip}((x - \text{mean}(x)) + 0.1, -0.5, 1.0)$
- **Rationale**: Centers NDVI around **0.1**. This lower center ensures that negative values appear more frequently in the scaled output, reflecting the natural behavior of water-based NDVI indices.

#### 2. Bound-Safe Centering for $x_1$ (n-WST)

- **Target Range**: **$[0.5, 1.0]$**
- **Method**: $x_{scaled} = \text{clip}((x - \text{mean}(x)) \times 2.0 + 0.75, 0.5, 1.0)$
- **Rationale**: Centers temperature data at 0.75. The tight scaling factor of 2.0 ensures that the variance is expanded to fill the positive range without being forced to hit the boundaries at all times.

#### Stability Justification:

The model requires $x_0 + x_1 + 0.99 > 0$. By ensuring $x_0 \ge -0.5$ and $x_1 \ge 0.5$, the minimum possible sum is $-0.5 + 0.5 + 0.99 = 0.99$. This guarantees strict mathematical stability across all input conditions.

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
