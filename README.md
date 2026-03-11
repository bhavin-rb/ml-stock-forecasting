# ml-stock-forecasting
# Stock Price Forecasting with Machine Learning

>The first run of this notebook was executed on**December 21, 2025 (EAT)**

## Introduction
This project explores **stock price forecasting** using machine learning and time‑series models.  
We begin with Apple Inc. (AAPL) as a single‑equity case study, applying linear regression with lag features and technical indicators (SMA, RSI).  
The framework is then extended to a multi‑asset portfolio, showing how regression methods scale from individual stocks to portfolio‑level forecasting.

The project is structured into modular Colab notebooks to guide readers from simple regression baselines toward more advanced forecasting techniques (ARIMA, GARCH, ML/DL).  
This step‑by‑step approach provides both clarity for beginners and depth for practitioners interested in portfolio‑level analysis.
---
## Single Stock Regression Analysis

## Part 1: Static Forecast
In the static approach, technical indicators (SMA, RSI) are **frozen at their last observed values** during the forecast horizon.  
This produces volatile predictions but demonstrates the baseline regression workflow.

### Predicted Closing Prices (Static Forecast)
| Day | Price (USD) |
|-----|-------------|
| 1   | $261.06     |
| 2   | $303.90     |
| 3   | $260.13     |
| 4   | $234.54     |
| 5   | $220.56     |
| 6   | $278.05     |
| 7   | $310.56     |

---

## Part 2: Dynamic Forecast
In the dynamic approach, SMA and RSI are **recalculated at each forecast step** using predicted values.  
This produces smoother and more realistic trajectories, better reflecting how indicators evolve in practice.

### Predicted Closing Prices (Dynamic Forecast)
| Day | Price (USD) |
|-----|-------------|
| 1   | $262.39     |
| 2   | $259.59     |
| 3   | $258.70     |
| 4   | $259.34     |
| 5   | $261.59     |
| 6   | $261.29     |
| 7   | $259.44     |

---

## Forecast Comparison (Static vs Dynamic)
| Model   | RMSE | MAE  |    R²   |
|---------|------|------|---------|
| Static  | 2.05 | 1.45 | 0.9955  |
| Dynamic | 2.91 | 2.60 | -0.5921 |

**Interpretation:**  
- Static forecasts fit past data better (high R²) but exaggerate volatility.  
- Dynamic forecasts are more realistic out-of-sample, though harder to optimize.  
- Together, they illustrate the trade-off between accuracy and realism.
- The table captures the accuracy vs realism trade‑off very clearly — which is exactly the point of showing both approaches side by side.

---

## Final Plot
The chart below compares historical prices, static forecasts, and dynamic forecasts for Apple stock.  
*(See attached plot in repository)*

<img width="491" height="319" alt="image" src="https://github.com/user-attachments/assets/ec448b02-1bf0-4d3d-8dde-4615b1ae8ab6" />

<img width="490" height="317" alt="image" src="https://github.com/user-attachments/assets/e11e01ea-19d4-4b15-97f0-4551cdb2a123" />

---
## Portfolio Forecasting

This section extends the forecasting framework from a single stock (Apple) to a multi‑asset portfolio of major technology companies (AAPL, MSFT, GOOGL, AMZN, NVDA).  
By treating the portfolio as an equal‑weight average, we demonstrate how regression models scale beyond individual equities to capture collective behavior.  

Both static (frozen indicators) and dynamic (rolling SMA/RSI updates) forecasts are generated for each ticker and then consolidated at the portfolio level.  
The results are presented through:
- Individual plots and metrics per equity
- A consolidated portfolio plot showing average forecasts
- Portfolio‑level metrics (RMSE, MAE, R²) comparing static vs dynamic approaches

This portfolio analysis highlights the trade‑off between in‑sample accuracy and out‑of‑sample realism, while also showing how diversification smooths volatility and improves interpretability.

---
## Portfolio Forecast Results

### Consolidated Portfolio Forecasts (Next 7 Days, Static SMA/RSI)

| Day | AAPL   | MSFT   | GOOGL  | AMZN   | NVDA   |
|-----|--------|--------|--------|--------|--------|
| 1   | 261.06 | 405.47 | 307.65 | 216.03 | 184.07 |
| 2   | 303.90 | 356.19 | 332.33 | 198.34 | 220.37 |
| 3   | 260.13 | 422.76 | 294.14 | 204.36 | 161.79 |
| 4   | 234.54 | 455.39 | 277.55 | 243.70 | 164.99 |
| 5   | 220.56 | 444.10 | 276.15 | 225.96 | 148.75 |
| 6   | 278.05 | 382.57 | 340.69 | 206.74 | 215.10 |
| 7   | 310.56 | 346.66 | 354.58 | 192.20 | 226.86 |

### Consolidated Portfolio Forecasts (Next 7 Days, Dynamic SMA/RSI)

| Day | AAPL   | MSFT   | GOOGL  | AMZN   | NVDA   |
|-----|--------|--------|--------|--------|--------|
| 1   | 262.39 | 407.99 | 304.70 | 218.53 | 185.79 |
| 2   | 259.59 | 409.40 | 299.00 | 216.88 | 180.96 |
| 3   | 258.70 | 410.22 | 301.17 | 214.28 | 179.74 |
| 4   | 259.34 | 408.24 | 305.49 | 212.74 | 182.18 |
| 5   | 261.59 | 407.37 | 307.37 | 215.59 | 185.97 |
| 6   | 261.29 | 408.26 | 302.91 | 217.95 | 184.86 |
| 7   | 259.44 | 410.26 | 299.64 | 217.21 | 181.16 |

### Forecast Comparison (Static vs Dynamic, Portfolio Average)

| Model    | RMSE  | MAE  | R²       |
|----------|-------|------|----------|
| Static   | 28.17 | 24.69| -111.371 |
| Dynamic  | 4.62  | 3.99 | -1.4903  |

### Interpretation

The portfolio results highlight the trade‑off between **static** and **dynamic** forecasting:

- **Static forecasts** fit past data tightly but produce unstable and exaggerated forward predictions, leading to very high errors and strongly negative R² values at the portfolio level.  
- **Dynamic forecasts** recalculate SMA/RSI at each step, resulting in more realistic trajectories. Although the statistical fit (R²) remains negative due to short‑horizon volatility, RMSE and MAE are significantly lower compared to static forecasts.  
- **Portfolio averaging** further smooths volatility, showing how diversification stabilizes forecasts and makes dynamic modeling more practical.

Together, these results demonstrate why regression baselines must be extended with dynamic updates — they capture market behavior more faithfully and provide a stronger foundation for advanced models (ARIMA, GARCH, ML/DL).

---

## Portfolio Forecast Plot

The consolidated portfolio plot provides a visual comparison of **static** and **dynamic** forecasts for the equal‑weight portfolio (AAPL, MSFT, GOOGL, AMZN, NVDA).  

- The black line shows the historical portfolio average over the last 60 days.  
- The red marker highlights the current portfolio average price.  
- The blue dashed line represents the 7‑day static forecast (SMA/RSI frozen).  
- The green solid line represents the 7‑day dynamic forecast (SMA/RSI recalculated each step).  

This visualization illustrates how diversification smooths volatility and how dynamic updates produce more realistic trajectories compared to static forecasts.

<img width="491" height="317" alt="image" src="https://github.com/user-attachments/assets/9f9c406b-6f07-41d2-8490-ef50e9f71b36" />

---

## Consolidated Portfolio Forecasts (Next 7 Days)

| Date       | Static Forecast | Dynamic Forecast |
|------------|-----------------|------------------|
| 2026-03-12 | 275.06          | 275.88           |
| 2026-03-13 | 282.23          | 273.17           |
| 2026-03-14 | 268.64          | 272.82           |
| 2026-03-15 | 275.23          | 273.60           |
| 2026-03-16 | 263.10          | 275.58           |
| 2026-03-17 | 284.63          | 275.05           |
| 2026-03-18 | 286.17          | 273.54           |

### Interpretation

This table summarizes the consolidated portfolio forecasts over the next 7 days.  
- **Static forecasts** (SMA/RSI frozen) show larger swings and exaggerated volatility.  
- **Dynamic forecasts** (SMA/RSI recalculated each step) produce smoother, more realistic trajectories.  

Together with the plots and metrics, this table provides a clear numerical view of how static vs dynamic approaches diverge in short‑term portfolio forecasting.

---

## Portfolio Forecast Metrics

| Model   | RMSE | MAE | R²       |
|---------|------|-----|----------|
| Static  | 8.01 | 7.01| -32.6196 |
| Dynamic | 2.39 | 1.94| -1.9849  |

### Interpretation

- **Static forecasts** show much higher error values (RMSE, MAE) and strongly negative R², confirming that frozen indicators are unstable for portfolio forecasting.  
- **Dynamic forecasts** reduce RMSE and MAE substantially, producing more realistic short‑term projections even though R² remains slightly negative due to volatility.  
- This comparison reinforces the lesson from the single‑equity case: regression baselines only become useful when indicators are updated dynamically.  

Together with the plots and forecast tables, these metrics complete the portfolio analysis and set the stage for more advanced models (ARIMA, GARCH, ML/DL).

---

### Data Context

The forecasts in this project were generated using market data collected during a period of global uncertainty.  
This context is important to keep in mind, as heightened volatility and crisis conditions can amplify short‑term fluctuations and affect the performance of forecasting models.  
The results therefore illustrate not only the technical trade‑offs between static and dynamic approaches, but also how models behave under stressed market environments.

---

## Roadmap
This repository will expand into a **series of forecasting methods**:
- ✅ Linear Regression (Static vs Dynamic)  
- 🔜 ARIMA (AutoRegressive Integrated Moving Average)  
- 🔜 GARCH (Generalized AutoRegressive Conditional Heteroskedasticity)  
- 🔜 Portfolio Forecasting (multi-equity models)  
- 🔜 Advanced ML/DL models (Random Forests, LSTMs)

---

## Conclusion

This project demonstrates how simple regression models can be applied to financial time‑series forecasting.  
By comparing static and dynamic approaches, we highlight the importance of indicator recalculation and the **trade‑offs between in‑sample accuracy and out‑of‑sample realism**.  

The portfolio analysis further shows how diversification smooths volatility while still reflecting the challenges of forecasting under uncertain market conditions.  
Future work will extend these methods to ARIMA, GARCH, and advanced ML/DL models, building on this regression baseline to achieve more robust and realistic forecasts.

---
---

Thank you for exploring this project!  
Stay tuned for updates as new forecasting methods are added, and feel free to contribute or share feedback to help refine the journey from regression baselines to advanced ML/DL models.

