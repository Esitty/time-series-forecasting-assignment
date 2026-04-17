# Time Series Forecasting: Solar Energy Production

## Overview
This project applies time series analysis and machine learning to forecast solar energy production using meteorological and environmental data. The goal was to identify what drives energy output and build a model capable of producing reliable forward-looking estimates to support operational planning.

## Dataset
196,777 15-minute interval readings recorded from 2017 to 2022, capturing six variables: energy captured (Wh), sunlight intensity (W/m²), temperature, hourly rainfall, cloud coverage, and daylight length. All variables were initially stored as object types and required type conversion and cleaning before analysis.

## What I Did & What I Found

### Data Cleaning
All numeric columns were cast to appropriate types and a small number of missing values (fewer than 15 rows per column across ~197K records) were dropped rather than imputed, preserving data integrity without meaningful loss.

### Exploratory Analysis
The data showed strong right-skew in energy output more than half of all 15-minute readings recorded zero production, reflecting nighttime hours. Peak output reached 5,020 Wh. Cloud coverage averaged 66% and sunlight intensity averaged just 32.6 W/m², consistent with a northern European climate. These patterns confirmed that the relationship between environmental conditions and energy output is non-linear.

### Modelling
Two models were trained and compared on an 80/20 chronological train-test split:

| Model | R² | MAE |
|---|---|---|
| Linear Regression | 0.846 | 239.8 Wh |
| Random Forest | **0.914** | **131.9 Wh** |

The Random Forest model substantially outperformed the linear baseline its R² of 0.91 indicates it explains 91% of the variance in energy output, and its MAE of ~132 Wh is nearly half that of the linear model. This confirms that the relationship between weather conditions and solar production is non-linear, and that tree-based models are better suited to capturing it.

### Forecasting
The Random Forest model was used to forecast average solar energy production for January 2026, producing an estimate of **129.4 Wh**. This sits comfortably within the range of historical January averages (83–180 Wh across 2017–2022), confirming the forecast is both credible and seasonally consistent.

## Why It Matters
Accurate solar energy forecasting has direct operational value it supports grid balancing, procurement decisions, and maintenance scheduling. Knowing in advance that a January is likely to produce around 129 Wh per interval allows energy managers to plan backup capacity or adjust storage accordingly. The model's strong performance (R² = 0.91) suggests it could be deployed with confidence in a real planning context.

## Tools & Libraries
- Python, Jupyter Notebook
- pandas, numpy, matplotlib, seaborn
- scikit-learn (LinearRegression, RandomForestRegressor, StandardScaler, train_test_split)

