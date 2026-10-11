# Time Series Analysis Project

Course project for Time Series Analysis. The goal is to model a real-world time series with two forecasting approaches, **interpret every step** (technically and in a business context), and compare the forecasts methodologically. It is not only about producing forecasts.

## Dataset

**US retail sales: clothing and clothing accessories stores (not seasonally adjusted)**, monthly, in millions of dollars, January 1992 to July 2026 (415 observations).

- Source: [FRED, series `MRTSSM448USN`](https://fred.stlouisfed.org/series/MRTSSM448USN) (US Census Bureau, Monthly Retail Trade Survey).
- File: [MRTSSM448USN.csv](MRTSSM448USN.csv) (columns `observation_date`, `MRTSSM448USN`).

The series can be decomposed as:

**Yₜ = Tₜ + Sₜ + Rₜ** (trend + seasonality + residual)

It shows a visible upward trend and a strong yearly seasonality (peak in December, dip in January and February) over more than 30 years. Its seasonal amplitude grows with the level, which makes the additive vs multiplicative choice a real question. The COVID-19 shock (spring 2020) is a clear outlier that Prophet can model as a special event.

## Approaches

### 1. ETS decomposition + ARIMA (understand and explore)

- Decompose Yₜ into trend (Tₜ), seasonality (Sₜ) and residual (Rₜ).
- Model the residual Rₜ with ARIMA:
  - stationarity checks (ADF / KPSS),
  - ACF / PACF analysis to choose the (p, d, q) orders,
  - residual diagnostics.
- Forecast by recombining the trend, the seasonality and the ARIMA forecast of Rₜ.
- Interpret each component, technically and in business terms.

### 2. Facebook Prophet (discover and compare)

- Understand how the method works: additive trend, seasonality, holidays, changepoints.
- Try different parameters (changepoint prior scale, seasonality mode, holidays, etc.) and interpret their effect.

## Forecast comparison

- Use the same train / test split for both approaches: train from January 1992 to December 2024, test from January 2025 to July 2026.
- Compare them with loss functions: MSE, RMSE, MAE, MAPE.
- Discuss when and why one approach performs better than the other.

## Report structure

The report is written in the Jupyter notebook `tsa-project.ipynb`:

1. Introduction
2. Data exploration
3. Approach 1: ETS decomposition + ARIMA
4. Approach 2: Prophet
5. Forecast comparison
6. Conclusion
7. AI-usage policy: the main prompts and how AI was used in the project

## Setup

Dependencies are managed with [uv](https://docs.astral.sh/uv/):

```bash
uv sync
```

Then open the notebook and select the `.venv` kernel.

## Workflow

The work is tracked with GitHub issues, one per step of the report. See the [issues](https://github.com/Adrien-EPF/TSA_Project/issues).
