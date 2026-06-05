# Estimating Value-at-Risk with GARCH-Family Models

This project estimates **Value-at-Risk (VaR)** for an equally-weighted portfolio using GARCH-family volatility models.

## Portfolio

Five assets with daily log-returns from **May 2020 – May 2025**:

| Asset | Ticker |
|-------|--------|
| Apple Inc. | AAPL |
| S&P 500 Index | ^GSPC |
| CNY/USD Exchange Rate | CNYUSD=X |
| WTI Crude Oil Futures | CL=F |
| Ethereum / USD | ETH-USD |

## Methodology

### 1. Stylized Facts Analysis
Volatility clustering, leptokurtosis, and ARCH effects are documented via ACF plots, Ljung-Box tests, and LM-ARCH tests.

### 2. Model Estimation
Six volatility models are fit and compared using AIC/BIC and residual diagnostics:

- ARCH(1), ARCH(2), ARCH(5)
- GARCH(1,1), GARCH(2,1), GARCH(1,2)
- EGARCH(1,1)

Diagnostics include Ljung-Box tests on standardized and squared standardized residuals, and LM-ARCH tests.

### 3. Model Diagnostics
GARCH(1,1) is analyzed in depth:
- Nyblom parameter stability test
- Sign Bias test
- Adjusted Pearson Goodness-of-Fit test
- News Impact Curves

**Key result:** GARCH(1,1) with $\alpha_1 + \beta_1 = 0.98$ captures high volatility persistence (~34-day half-life) and is the preferred model by BIC.

### 4. VaR Forecasting & Backtesting
VaR is computed at **95%** and **99%** confidence levels for:
- **In-sample** period using fitted conditional volatility
- **Out-of-sample** period using a rolling 100-day window with 1-step-ahead forecasts

Model quality is evaluated by comparing violation rates against expected exceedance frequencies.

## Structure

```
var-garch.ipynb   # Main analysis notebook
var-garch.html    # HTML exported from Jupyter notebook
report.pdf        # Report
data/             # Input data
```

## Dependencies

- Python: `pandas`, `numpy`, `arch`, `scipy`, `statsmodels`, `yfinance`, `matplotlib`
- R: `rugarch` (via `rpy2`)
