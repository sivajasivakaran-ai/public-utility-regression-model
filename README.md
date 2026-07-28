# public-utility-regression-model
# Hotazel Steam Forecasting

A time series forecasting tutorial/project that uses linear regression (OLS) to model and predict quarterly revenue, using Apple's quarterly sales data as a worked example.

## Overview

This notebook walks through building a time-trend regression model for forecasting, progressing from a simple trend model to a seasonally-adjusted model with dummy variables, and finally to forecasting future (out-of-sample) values using synthetic data.

## What the notebook does

1. **Data loading & prep** — Loads quarterly sales data (`qSales_2024.csv`), filters to a single ticker (AAPL), and converts the date column to a proper datetime type.
2. **Visualization** — Plots revenue over time to inspect the trend before modeling.
3. **Time index construction** — Creates a sequential `time` variable (1, 2, 3, …) to use as the independent variable in the regression, following standard time-series regression conventions.
4. **Train/test split** — Splits the data chronologically into 75% training / 25% testing.
5. **Baseline trend model** — Fits an OLS model of revenue on time (`revenue = β0 + β1 * time`) and generates point forecasts and prediction intervals (80% confidence level) on the test set.
6. **Seasonal dummy variable model** — Adds a dummy variable flagging a specific fiscal quarter (`fqtr == 1`) plus an interaction term (`time * dummy`) to capture seasonal effects on both the trend level and slope. Refits the model and re-evaluates on the test set.
7. **Forecasting future values** — Loads a synthetic dataset (`synthetic_data.csv`) representing future time periods, dummy variables, and interaction terms, and applies the fitted model to generate forecasts and prediction intervals beyond the observed data.

## Key concepts covered

- Time series regression using a simple integer time index as the predictor
- Train/test splitting for time series (chronological, not random)
- Point forecasts vs. prediction intervals (`get_prediction().summary_frame()`)
- Using dummy variables and interaction terms to model seasonality (level shift + slope shift)
- Forecasting beyond the dataset using synthetically constructed future inputs

## Requirements

- Python 3
- `pandas`
- `numpy`
- `statsmodels`
- `matplotlib`

## Data files needed

- `qSales_2024.csv` — historical quarterly sales data (must include `tic`, `datadate`, `saleq`, `fqtr` columns)
- `synthetic_data.csv` — synthetic future data with `time`, `release_dummy_variable`, and `release_dummy_interaction` columns

## Usage

Run the notebook cells in order. Each modeling stage (baseline trend → seasonal model → future forecast) builds on the previous one, so cells should not be run out of sequence.
