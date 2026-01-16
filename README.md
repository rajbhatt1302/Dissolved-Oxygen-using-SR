# Dissolved Oxygen (DO) Prediction using Symbolic Regression

## Overview

This project uses **Symbolic Regression** to find a mathematical equation that estimates Dissolved Oxygen (DO) levels in water bodies. Instead of a "black box" model (like a neural network), this approach generates a readable formula (e.g., `y = 2*x0 + 0.5*x1`), allowing us to understand the physical relationship between the inputs and DO.

## Input Variables

The model uses two remote sensing indices as inputs:

- **x0**: NDVI (Normalized Difference Vegetation Index) - Indicates vegetation health.
- **x1**: n-wst (Normalized Water Surface Temperature) - Indicates thermal properties.

**Target Variable**:

- **y**: Dissolved Oxygen (DO) in ppm.

## Scaling Approach (Crucial Step)

Before finding the equation, we process the data using **Robust Scaling**.

### Why do we scale?

Raw data values can vary wildly (e.g., NDVI might be small, while temperature is large). If we don't scale, the algorithm might bias itself toward the larger numbers, ignoring the smaller but important ones.


## Output

- **Equations**: The script will print a list of candidate equations.
- **Best Model**: It identifies the "Best Model" based on accuracy ($R^2$) and error (MAE).
- **Predictions**: A file `predicted_DO.csv` is generated, comparing observed vs. predicted values.
