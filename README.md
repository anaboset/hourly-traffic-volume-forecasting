# Hourly Traffic Volume Forecasting

## Overview

This project develops a multi-step hourly traffic volume forecasting system using historical traffic data from the Metro Interstate Traffic Volume dataset.

The goal is to predict future traffic volume at multiple forecasting horizons and compare different forecasting approaches ranging from simple statistical baselines to machine learning and deep learning models.

## Project Objectives

- Analyze historical hourly traffic patterns.
- Perform time-series data preprocessing and exploratory data analysis.
- Engineer lag, rolling-window, and calendar-based features.
- Develop multi-step traffic forecasting models.
- Compare Seasonal Naive, Prophet, XGBoost, and LSTM models.
- Evaluate forecasting performance at multiple horizons.
- Identify the most effective approach for hourly traffic prediction.

## Dataset

The project uses the **Metro Interstate Traffic Volume** dataset.

The dataset contains approximately 48,000 hourly observations of traffic volume on Interstate 94, together with weather and calendar-related information.

### Main variables

- Traffic volume
- Temperature
- Rain
- Snow
- Clouds
- Weather description
- Holiday information
- Date and time

Raw datasets are not included in this repository.

## Forecasting Horizons

The models are evaluated for:

| Horizon | Prediction |
|---|---|
| 1 hour | Traffic volume one hour ahead |
| 3 hours | Traffic volume three hours ahead |
| 6 hours | Traffic volume six hours ahead |
| 12 hours | Traffic volume twelve hours ahead |
| 24 hours | Traffic volume one day ahead |

## Data Preprocessing

The preprocessing pipeline includes:

1. Loading the traffic dataset.
2. Parsing timestamps.
3. Sorting observations chronologically.
4. Removing duplicate timestamps.
5. Reindexing the data to a continuous hourly timeline.
6. Handling missing weather values.
7. Preserving missing traffic observations rather than artificially filling target values.

## Exploratory Data Analysis

Exploratory analysis was performed to understand:

- Long-term traffic trends.
- Daily traffic patterns.
- Weekly seasonality.
- Monthly and yearly patterns.
- Relationship between traffic volume and weather variables.
- Missing observations and timestamp irregularities.

Visualizations generated during the analysis are stored in the `figures/` directory.

## Feature Engineering

Time-series features include:

### Lag features

- 1-hour lag
- 24-hour lag
- 168-hour lag

### Rolling features

- 3-hour rolling mean and standard deviation
- 24-hour rolling mean and standard deviation

Rolling statistics are shifted before calculation to prevent future information from leaking into the training data.

### Calendar features

- Hour
- Day of week
- Month
- Weekend indicator
- Cyclical hour representation
- Cyclical day-of-week representation

## Models

Four forecasting approaches are evaluated.

### 1. Seasonal Naive

A simple baseline model that uses historical seasonal traffic values as predictions.

This provides a reference point for determining whether more advanced models provide meaningful improvement.

### 2. Prophet

Prophet is used as a time-series forecasting model capable of modeling trend and seasonal patterns.

### 3. XGBoost

XGBoost is used as a gradient boosting model with engineered time-series features.

It learns relationships between historical traffic values, lag features, rolling statistics, calendar features, and available external variables.

### 4. LSTM

Long Short-Term Memory (LSTM) neural networks are used to model sequential dependencies in historical traffic patterns.

LSTM is included as the deep learning approach in the project.

## Validation Strategy

Because this is a time-series forecasting problem, random train-test splitting is avoided.

The project uses time-based validation / expanding-window evaluation to ensure that future observations are never used to train models predicting the past.

The evaluation is performed across multiple forecasting horizons.

## Evaluation Metrics

The models are evaluated using:

### MAE

Mean Absolute Error measures the average absolute difference between predicted and actual traffic volume.

Lower values indicate better performance.

### sMAPE

Symmetric Mean Absolute Percentage Error measures relative forecasting error while reducing some of the limitations of traditional MAPE.

Lower values indicate better performance.

### MASE

Mean Absolute Scaled Error compares model performance against a naive forecasting baseline.

A MASE value below 1 indicates improvement over the baseline.

## Project Structure

```text
traffic-volume-forecasting/
│
├── data/
│   └── Dataset information
│
├── notebooks/
│   └── Trafic_Hourly_Forcasting(2).ipynb
│
├── docs/
│   └── Project documentation
│
├── figures/
│   └── EDA and model visualizations
│
├── models/
│   └── Saved model files if required
│
├── results/
│   └── Model evaluation results
│
├── .gitignore
├── requirements.txt
└── README.md
