# ml-stock-forecasting
# Stock Price Forecasting with Machine Learning

>The first run of this notebook was executed on**December 21, 2025 (EAT)**

## Introduction
This project explores stock price forecasting using machine learning and time-series models.  
We begin with **Apple Inc. (AAPL)** as a single equity case study, applying regression with lag features and technical indicators.  
The project is structured into modular notebooks to guide readers from simple models to more advanced forecasting techniques.

---

## Part 1: Static Forecast
In the static approach, technical indicators (SMA, RSI) are **frozen at their last observed values** during the forecast horizon.  
This produces volatile predictions but demonstrates the baseline regression workflow.

### Predicted Closing Prices (Static Forecast)
| Day | Price (USD) |
|-----|-------------|
| 1   | $271.67     |
| 2   | $296.04     |
| 3   | $287.10     |
| 4   | $263.12     |
| 5   | $244.74     |
| 6   | $268.27     |
| 7   | $296.73     |

---

## Part 2: Dynamic Forecast
In the dynamic approach, SMA and RSI are **recalculated at each forecast step** using predicted values.  
This produces smoother and more realistic trajectories, better reflecting how indicators evolve in practice.

### Predicted Closing Prices (Dynamic Forecast)
| Day | Price (USD) |
|-----|-------------|
| 1   | $274.70     |
| 2   | $273.36     |
| 3   | $271.82     |
| 4   | $272.10     |
| 5   | $273.84     |
| 6   | $274.36     |
| 7   | $273.06     |

---

## Forecast Comparison (Static vs Dynamic)
| Model   | RMSE | MAE  |    R²   |
|---------|------|------|---------|
| Static  | 1.98 | 1.38 | 0.9954  |
| Dynamic | 2.82 | 2.55 | -0.4032 |

📊 **Interpretation:**  
- Static forecasts fit past data better (high R²) but exaggerate volatility.  
- Dynamic forecasts are more realistic out-of-sample, though harder to optimize.  
- Together, they illustrate the trade-off between accuracy and realism.

---

## Final Plot
The chart below compares historical prices, static forecasts, and dynamic forecasts for Apple stock.  
*(See attached plot in repository)*

<img width="2970" height="1924" alt="apple_forecast_static" src="https://github.com/user-attachments/assets/203991b6-29f5-4372-9ee1-eafcdfab0d86" />

<img width="2970" height="1924" alt="apple_forecast_static_vs_dynamic" src="https://github.com/user-attachments/assets/a5cbf5ba-7a92-4ccb-a409-104e0abd30f8" />

---

## Roadmap
This repository will expand into a **series of forecasting methods**:
- ✅ Linear Regression (Static vs Dynamic)  
- 🔜 ARIMA (AutoRegressive Integrated Moving Average)  
- 🔜 GARCH (Generalized AutoRegressive Conditional Heteroskedasticity)  
- 🔜 Portfolio Forecasting (multi-equity models)  
- 🔜 Advanced ML/DL models (Random Forests, LSTMs)

---

## Project Structure
/Stock-Forecasting-Project
│
├── notebooks/
│   ├── apple_static_dynamic.ipynb   # Single equity demo
│   ├── portfolio_forecasting.ipynb  # Multi-equity extension
│
├── results/                         # Saved plots and tables
├── README.md                         # Documentation and analysis
└── requirements.txt                  # Dependencies


---

## Conclusion
This project demonstrates how simple regression models can be applied to financial time-series forecasting.  
By comparing static and dynamic approaches, we highlight the importance of indicator recalculation and the **trade-offs between in-sample accuracy and out-of-sample realism**.  
Future work will extend these methods to ARIMA, GARCH, and portfolio-level forecasting.

