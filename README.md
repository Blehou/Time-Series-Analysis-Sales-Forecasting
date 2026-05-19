# Time-Series-Analysis-Sales-Forecasting

## Overview

This project focuses on time series forecasting using simulated sales data covering the period from 2010 to 2019.
The objective is to predict the daily number of products sold in 2019 using both:

* a statistical forecasting approach based on the Box-Jenkins methodology,
* and a machine learning approach using Gradient Boosting.

The project explores trend analysis, seasonality, stationarity, feature engineering and forecasting evaluation.

---

# Dataset

The dataset contains simulated daily sales data with:

* `Date`
* `store`
* `product`
* `number_sold`

### Characteristics

* Period covered:

  * Train set: 2010 → 2018
  * Test set: 2019
* 7 unique stores
* 10 unique products
* No missing values
* Simulated components:

  * long-term trends
  * yearly seasonality
  * weekday/weekend effects
  * random noise

The objective is to forecast the `number_sold` variable for 2019.

---

# Project Structure

```bash
├── train.csv
├── test.csv
├── Sale-Forecasting.ipynb
├── README.md
└── LICENCE
```

---

# 1. Statistical Approach – Box-Jenkins / SARIMA

The first part of the project uses a classical statistical time series approach.

## Main steps

* Time series visualization
* Buys-Ballot analysis
* Additive vs multiplicative structure analysis
* Seasonal decomposition
* Stationarity testing (ADF test)
* Differencing
* ACF / PACF analysis
* SARIMA modeling
* Forecasting on 2019

## Final Model

SARIMA(0,1,1)(0,1,1,7)

## SARIMA Results

* MAE ≈ 258.7
* MAPE ≈ 0.47%

The SARIMA model successfully captures:

* the global trend,
* the weekly seasonality,
* and the overall structure of the series.

However, predictions remain smoother than the real data and struggle to reproduce local irregular fluctuations.

---

# 2. Machine Learning Approach – Gradient Boosting

The second approach transforms the forecasting problem into a supervised learning task.

## Feature Engineering

Several temporal features were created:

### Calendar Features

* day of week
* month
* year
* week of year
* weekend indicator

### Lag Features

* lag_1
* lag_7
* lag_30

### Rolling Statistics

* rolling mean
* rolling standard deviation

The model also uses:

* `store`
* `product`

to capture local sales behaviors.

---

# Model

The forecasting model used is:

* Gradient Boosting Regressor

## Results

* MAE ≈ 8.54
* MAPE ≈ 1.21%

The Gradient Boosting model reproduces:

* the trend,
* the seasonality,
* and a large part of the local fluctuations.

Compared to SARIMA, the ML approach captures short-term variations more accurately thanks to feature engineering.

---

# Evaluation Metric

The main evaluation metric used in this project is:

$$
MAPE = \frac{1}{n}\sum_{t=1}^{n}\left|\frac{y_t-\hat{y}_t}{y_t}\right| \times 100
$$

(MAPE – Mean Absolute Percentage Error)

---

# Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Statsmodels
* Scikit-learn

---

# Key Takeaways

* SARIMA performs very well for capturing global temporal structures.
* Gradient Boosting provides more flexible predictions and better captures local variations.
* Feature engineering plays a crucial role in machine learning forecasting tasks.
