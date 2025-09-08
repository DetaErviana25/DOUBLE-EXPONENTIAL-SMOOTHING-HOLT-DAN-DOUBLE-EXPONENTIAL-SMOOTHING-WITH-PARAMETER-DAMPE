# IPM Forecasting with Damped Holt Method

## 📊 Overview
This repository contains R code for forecasting the Human Development Index (IPM - Indeks Pembangunan Manusia) of East Lampung Regency using Double Exponential Smoothing methods, specifically comparing standard Holt's method with the Damped Holt method for time series forecasting.

## 🎯 Research Objectives
- Apply Double Exponential Smoothing (Holt's method) to IPM time series data
- Compare standard Holt's method with Damped Holt's method
- Evaluate forecasting accuracy using multiple error metrics
- Generate 5-period ahead forecasts for East Lampung Regency's IPM

## 📈 Data Description

### Dataset
- **Variable**: IPM (Human Development Index)
- **Location**: East Lampung Regency (Kabupaten Lampung Timur)
- **Time Period**: 2010-2022 (13 years)
- **Frequency**: Annual data
- **Source File**: `Indeks Pembangunan Manusia.xlsx`

### Data Structure
```
Year: 2010, 2011, 2012, ..., 2022
IPM:  [Time series values]
```

## 📋 Prerequisites

### Required R Packages
```r
library(readxl)    # For reading Excel files
library(forecast)  # For advanced forecasting methods
```

### Required Files
- `Indeks Pembangunan Manusia.xlsx` (Sheet2) - Contains IPM data

## 🔧 Methods Implemented

### 1. Standard Holt's Method (Double Exponential Smoothing)
- **Function**: `HoltWinters()` with `gamma = FALSE`
- **Parameters**: 
  - α (alpha): Level smoothing parameter
  - β (beta): Trend smoothing parameter
- **Characteristics**: Assumes linear trend continues indefinitely

### 2. Damped Holt's Method
- **Function**: `holt()` with `damped = TRUE`
- **Parameters**:
  - α (alpha): Level smoothing parameter
  - β (beta): Trend smoothing parameter
  - φ (phi): Damping parameter (0 < φ < 1)
- **Characteristics**: Trend dampens over time, more conservative forecasts

## 📊 Analysis Workflow

### 1. Data Preparation
```r
# Import data
IPM <- read_excel("DATA PKL/Indeks Pembangunan Manusia.xlsx", sheet = "Sheet2")

# Convert to time series
IPM <- ts(IPM$Ipm, start = 2010, frequency = 1)
```

### 2. Standard Holt's Method
```r
# Fit model
holtb.IPM = HoltWinters(IPM.ts, alpha = NULL, beta = NULL, gamma = FALSE)

# Generate forecasts
pred.holtb = predict(holtb.IPM, 5)
```

### 3. Damped Holt's Method
```r
# Fit model
holt.IPM2 = holt(IPM, h = 5, damped = TRUE, alpha = NULL, beta = NULL, phi = NULL)
```

## 📏 Accuracy Metrics

### Error Measures Calculated
1. **SSE** - Sum of Squared Errors
2. **MSE** - Mean Squared Error
3. **RMSE** - Root Mean Squared Error
4. **MAPE** - Mean Absolute Percentage Error

### Formulas
```
MSE = SSE / n
RMSE = √MSE
MAPE = (1/n) × Σ|Actual - Forecast|/|Actual| × 100%
```

## 🚀 Usage

### 1. Setup Environment
```r
# Set working directory
setwd("your/path/to/data")

# Load required libraries
library(readxl)
library(forecast)
```

### 2. Run Analysis
```r
# Execute the complete script
source("IPM DAMPED.R")
```

### 3. View Results
The script will output:
- Model parameters (α, β, φ)
- Accuracy metrics
- Forecasted values for next 5 periods
- Visualization plots

## 📈 Output Visualizations

### 1. Time Series Plot
- Original IPM data from 2010-2022
- Trend visualization

### 2. Standard Holt's Method Plot
- **Blue line**: Actual data
- **Red line**: Fitted values
- **Red points**: 5-period forecasts
- Vertical line separating historical and forecast periods

### 3. Damped Holt's Method Plot
- **Purple line**: Actual data
- **Red line**: Fitted values
- **Green line**: Forecasted values with confidence intervals

## 🔍 Key Features

### Model Comparison
| Method | Trend Behavior | Best For |
|--------|---------------|----------|
| Standard Holt | Linear trend continues | Data with consistent trend |
| Damped Holt | Trend dampens over time | Data where trend may flatten |

### Automatic Parameter Optimization
- All smoothing parameters (α, β, φ) are optimized automatically
- Uses maximum likelihood estimation or sum of squared errors minimization

### Comprehensive Error Analysis
- Multiple accuracy metrics for model evaluation
- Residual analysis capabilities

## 📊 Expected Results

### Model Output
```r
# Standard Holt's parameters
Alpha: [optimized value]
Beta:  [optimized value]

# Damped Holt's parameters  
Alpha: [optimized value]
Beta:  [optimized value]
Phi:   [damping parameter]
```

### Forecast Output
```r
# 5-period ahead forecasts
2023: [forecast value]
2024: [forecast value]
2025: [forecast value]
2026: [forecast value]
2027: [forecast value]
```

## 🎯 Applications

### Policy Planning
- **Regional Development**: Long-term IPM planning for East Lampung
- **Resource Allocation**: Budget planning based on projected development needs
- **Performance Monitoring**: Tracking progress against forecasted targets

### Research Applications
- Comparative study of forecasting methods
- Trend analysis in human development
- Regional development pattern analysis

## 🔧 Customization Options

### Forecast Horizon
```r
# Change forecast periods (currently set to 5)
h = 10  # For 10-period ahead forecasts
```

### Parameter Control
```r
# Manual parameter setting (if desired)
alpha = 0.3
beta = 0.1
phi = 0.8
```

## 📝 Mathematical Foundation

### Standard Holt's Method
```
Level:    l_t = α×y_t + (1-α)×(l_{t-1} + b_{t-1})
Trend:    b_t = β×(l_t - l_{t-1}) + (1-β)×b_{t-1}
Forecast: ŷ_{t+h} = l_t + h×b_t
```

### Damped Holt's Method
```
Level:    l_t = α×y_t + (1-α)×(l_{t-1} + φ×b_{t-1})
Trend:    b_t = β×(l_t - l_{t-1}) + (1-β)×φ×b_{t-1}
Forecast: ŷ_{t+h} = l_t + (φ + φ² + ... + φ^h)×b_t
```

## ⚠️ Important Notes

### Data Requirements
- Minimum 2-3 years of data for reliable trend estimation
- Regular time intervals (annual data in this case)
- No missing values in the time series

### Method Selection
- **Use Standard Holt** when trend is expected to continue linearly
- **Use Damped Holt** when trend may flatten or reverse over time
- Compare accuracy metrics to choose the best method

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Additional forecasting methods (ARIMA, ETS)
- Seasonal decomposition analysis
- Cross-validation procedures
- Interactive visualizations

## 📄 License

This project is available for educational and research purposes. Please cite appropriately when using this code for academic work.

---

**Note**: Ensure the Excel file is properly formatted with IPM data in Sheet2 before running the analysis.
