# SPY Stock Price Forecasting: ARIMA vs. LSTM

## Overview

This project forecasts SPY stock prices using two different approaches:
- **ARIMA:** A classical time series model that serves as a baseline.
- **LSTM:** A deep learning model capable of capturing non-linear dependencies in stock prices.

The project demonstrates the complete modeling pipeline—from data collection and preprocessing to model training, evaluation, and interactive visualization. It also discusses challenges, trade-offs, and potential avenues for further improvements.

## Repository Structure


## Methodology

### Data Collection
- **Data Source:** Historical SPY stock price data (from 2010 to 2022) is collected using the [yfinance API](https://pypi.org/project/yfinance/).
- **Target Variable:** We use the daily `Close` price for forecasting.

### Data Preprocessing
- **Cleaning:** Missing values and anomalies are identified and addressed.
- **Scaling:** The `Close` prices are normalized using Min-Max scaling for input into the LSTM model.
- **Windowing:** A sliding window of 60 days is used to create sequences for LSTM training.
- **Stationarity:** For the ARIMA model, stationarity is a key consideration. Differencing is applied within ARIMA (order (1,1,1) is used as an example).

### Forecast Models

#### ARIMA
- **Approach:** A classical statistical model that uses autoregression and moving averages.
- **Benefits:** Transparent model parameters and simplicity in capturing short-term dependencies.
- **Limitations:** Requires time series to be stationary and may struggle with non-linear patterns.

#### LSTM
- **Approach:** A deep learning model that employs Long Short-Term Memory (LSTM) units to capture long-term dependencies.
- **Benefits:** Better at modeling non-linearities and complex patterns.
- **Limitations:** More computationally intensive and inherently less interpretable.

### Evaluation
- **Metrics:** Both models are evaluated using:
  - Mean Squared Error (MSE)
  - Mean Absolute Error (MAE)
- **Visualization:** Forecasts are compared interactively using Plotly, featuring range sliders, hover tooltips, and downloadable plots.

## Challenges and Trade-offs

### Non-Stationarity
- **Issue:** Stock prices are non-stationary, which poses a challenge for classical models like ARIMA.
- **Solution:** Differencing and seasonality detection techniques are applied for ARIMA. LSTM models, due to their non-linear nature, can inherently manage non-stationarity but require careful regularization.

### Interpretability vs. Predictive Power
- **ARIMA:** Offers clear interpretation through its statistical parameters (p, d, q values).
- **LSTM:** Provides improved predictive power on complex datasets but suffers from a lack of interpretability.
- **Enhancement:** Techniques like [SHAP](https://github.com/slundberg/shap) can be integrated to better understand LSTM predictions.

### Complexity and Computational Cost
- **ARIMA:** Lightweight and faster to train, yet limited in capturing complex patterns.
- **LSTM:** More flexible and capable but requires significant computational resources and hyperparameter tuning to avoid overfitting.

## Further Improvements

1. **Experimentation with Additional Models:**
   - **TCNs (Temporal Convolutional Networks):** Could better capture long-term dependencies.
   - **Transformer-based Models:** For capturing sequential dependencies with attention mechanisms.

2. **Hyperparameter Tuning:**
   - Utilize GridSearch or Bayesian optimization (e.g., with [Optuna](https://optuna.org/)) to systematically fine-tune parameters like:
     - Number of LSTM units
     - Learning rate
     - Batch size
     - Window length

3. **Enhance Interpretability:**
   - Apply **SHAP** (SHapley Additive exPlanations) to understand the impact of different input features on LSTM predictions.
   - Visualize feature contributions to provide insights into model decisions.

4. **Deployment and Interactivity:**
   - Integrate the interactive Plotly dashboard into a **Streamlit** web application.
   - Provide user controls for selecting forecast horizons, model parameters, and viewing detailed performance metrics.

## Usage

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/spy-stock-forecasting.git
   cd spy-stock-forecasting

Model	MSE	MAE	Pros	Cons
ARIMA	52.3	5.6	Interpretable, Lightweight	Struggles with non-linearity
LSTM	43.9	4.2	Handles complex patterns	Black-box, needs tuning
