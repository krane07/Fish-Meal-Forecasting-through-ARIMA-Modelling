# Fish-Meal-Forecasting-through-ARIMA-Modelling
## Introduction

This project focuses on forecasting fish meal prices, a critical commodity in the animal feed industry, particularly for aquaculture. Reliable price forecasts are essential for risk management and strategic decision-making in financial markets. Using historical data from Peru, this research aims to develop an optimal forecasting model to identify potential risks and opportunities in the fish meal market. The primary methodology employed is the Autoregressive Integrated Moving Average (ARIMA) model, a widely recognized and effective tool for time series forecasting.

## Project Overview

This project focuses on forecasting fish meal prices using the Autoregressive Integrated Moving Average (ARIMA) model. The analysis utilizes historical price data from Peru, obtained from the International Monetary Fund (IMF) website, spanning from 1990 to 2024. The goal is to develop a robust forecasting model to aid in risk management and strategic decision-making within the fish meal market.

## Data

The dataset used in this project contains monthly fish meal prices (PFSHMEAL) in dollars per metric ton for Peru. The data was sourced from the IMF commodity prices website: <https://www.imf.org/en/Research/commodity-prices>. The original dataset contains 94 different commodities, from which only the "Fish meal" commodity is extracted for this analysis.

## Methodology

The forecasting process involves several key steps:

1.  **Data Loading and Preparation:**

    * The `external_data_mar.xls` file is imported using `readxl`.

    * Relevant columns are selected, and header rows are removed.

    * The fish meal price series is transformed using a natural logarithm to stabilize variance.

    * A time series object (`xts`) is created with monthly dates from 1990 to 2024.

2.  **Exploratory Data Analysis (EDA):**

    * Descriptive statistics are calculated and printed.

    * Visualizations (plot of time series, histogram, frequency) are generated to understand the data distribution and trends.

3.  **Stationarity Testing and Differencing:**

    * The Augmented Dickey-Fuller (ADF) test is conducted to check for unit roots (non-stationarity) in the time series.

    * Since the initial series is non-stationary, it is differenced once to achieve stationarity.

    * The ADF test is re-conducted on the differenced series to confirm stationarity.

4.  **ARIMA Model Identification:**

    * Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots are used to identify potential orders for the AutoRegressive (AR) and Moving Average (MA) components of the ARIMA model.

5.  **ARIMA Model Estimation and Selection:**

    * Several ARIMA models (AR(1), AR(2), MA(1), ARMA(1,1), ARMA(2,1)) are fitted to the differenced data.

    * Model diagnostics include:

        * **Ljung-Box Test:** To check for autocorrelation in residuals.

        * **Shapiro-Wilk Test:** To check for normality of residuals.

        * Visual inspection of residual plots.

        * Calculation of standard errors, AIC (Akaike Information Criterion), and BIC (Bayesian Information Criterion) for model comparison. Lower AIC/BIC values generally indicate a better fit.

6.  **Model Training and Evaluation:**

    * The dataset is split into training (90%) and testing (10%) sets.

    * The best-performing ARIMA models (MA(1) and ARMA(1,1) based on initial analysis) are re-trained on the training data.

    * Residual diagnostics (Ljung-Box, Shapiro-Wilk) and AIC/BIC are re-checked for the trained models.

    * **Dynamic Forecasting (Type A):** Forecasts are generated for the test period using the `forecast()` function. Accuracy metrics (e.g., RMSE, MAE, MAPE) are calculated.

    * **Static Forecasting (Type B):** One-step-ahead forecasts are generated for the test period using the `fitted()` function on a model applied to the test data, based on coefficients estimated from the training data. Accuracy metrics are calculated.

7.  **STL Model Forecasting (Seasonal-Trend Decomposition using Loess):**

    * The original (non-logged, non-differenced) fish meal price series is converted to a `ts` object.

    * The series is decomposed into seasonal, trend, and remainder components using `decompose(type = "multiplicative")`.

    * An STL model with ARIMA (`stlm`) is fitted to the training data.

    * Forecasts are generated for the test period.

    * Accuracy metrics (MSE, RMSE, MAE, MAPE) are calculated for the STL model's forecasts.

    * Visualizations of the STL decomposition and forecasts are provided.

## Results

The project evaluates various ARIMA model specifications and an STL-ARIMA approach to identify the most optimal model for forecasting fish meal prices. The accuracy metrics (RMSE, MAE, MAPE) from both dynamic and static forecasting methods, as well as the STL model, provide insights into the models' predictive performance. The analysis aims to determine a reliable forecast that can assist in identifying market risks and opportunities.

## How to Run the Code

To run this analysis, you will need R and RStudio (recommended).

1.  **Clone the Repository:**

    ```bash
    git clone [https://github.com/krane07/Fish-Meal-Forecasting-through-ARIMA-Modelling.git](https://github.com/your-username/Fish-Meal-Forecasting-through-ARIMA-Modelling.git)
    cd Fish-Meal-Forecasting-through-ARIMA-Modelling
    ```

2.  **Download the Data:**

    * Download the `external_data_mar.xls` file from the IMF commodity prices website: <https://www.imf.org/en/Research/commodity-prices>.

    * Place the downloaded `external_data_mar.xls` file in the same directory as the R script, or update the file path in the R script:

        ```R
        data_set <- read_excel("path/to/your/external_data_mar.xls")
        ```

3.  **Install Dependencies:**
    Open RStudio, open the R script, and install the required packages using the following commands:

    ```R
    install.packages("readxl")
    install.packages("zoo")
    install.packages("xts")
    install.packages("lmtest")
    install.packages("summarytools")
    install.packages("tseries")
    install.packages("forecast")
    install.packages("stats")
    install.packages("ggplot2")
    install.packages("MLmetrics")
    ```

4.  **Run the R Script:**
    Execute the R script (e.g., `fish_meal_forecasting.R`) in RStudio. The script will perform all data loading, analysis, modeling, and forecasting steps, printing results and generating plots.

## Dependencies

The following R packages are required to run the script:

* `readxl`

* `zoo`

* `xts`

* `lmtest`

* `summarytools`

* `tseries`

* `forecast`

* `stats`

* `ggplot2`

* `MLmetrics`
