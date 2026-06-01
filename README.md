# HMM Market Regime Allocation

This project studies whether Hidden Markov Models (HMMs) can identify probabilistic market regimes and support a systematic, risk-aware ETF allocation strategy.

The goal is not to build a black-box strategy that simply maximizes return. The goal is to build an interpretable research workflow that connects market data, macroeconomic indicators, regime modelling, portfolio allocation, and walk-forward backtesting.

## Rendered Report

The full notebook is exported as an HTML report for easier reading:

[Open the rendered project report](https://elvisfoo.github.io/hmm-market-regime-allocation/)

The source notebook is available at:

[`notebooks/market_regime_allocation_research.ipynb`](notebooks/market_regime_allocation_research.ipynb)

## Research Question

> Can market and macroeconomic signals be used to identify probabilistic market regimes, and can those regimes support a systematic ETF allocation strategy that improves risk-adjusted performance and drawdown control compared with static benchmarks?

## Asset Universe

The allocation universe uses four liquid ETFs:

| ETF | Role |
|---|---|
| SPY | U.S. equities / growth exposure |
| TLT | Long-term U.S. Treasuries / duration exposure |
| GLD | Gold / inflation and uncertainty hedge |
| SHY | Short-term U.S. Treasuries / defensive cash-like exposure |

These assets were chosen because they are interpretable, liquid, and represent distinct building blocks commonly used in cross-asset allocation.

## Data Sources

- **Tiingo**: daily ETF price data
- **FRED**: macroeconomic and market-risk indicators

Raw API outputs and processed datasets are cached locally under `data/`, which is ignored by git.

## Methodology

The project follows a full research workflow:

1. Collect ETF price data and macroeconomic indicators.
2. Engineer monthly market and macro features.
3. Train and compare 2-state, 3-state, and 4-state Gaussian HMMs.
4. Select a 3-state HMM based on validation evidence and interpretability.
5. Interpret inferred regimes using returns, volatility, drawdowns, macro conditions, frequency, persistence, and historical timing.
6. Define a transparent regime-to-allocation policy.
7. Run a walk-forward backtest using only information available up to each rebalance date.
8. Compare the regime-aware strategy against SPY buy-and-hold and a static 60/40 SPY/TLT benchmark.
9. Discuss results, stress episodes, limitations, and practical interpretation.

## Main Findings

The selected 3-state HMM produced interpretable regimes:

- **Resilient risk-on**
- **Policy-supported recovery**
- **Stress**

The baseline regime strategy did not maximize raw return versus SPY, but it improved the risk-adjusted profile.

Over the full walk-forward simulation from 2019 onward:

| Strategy | Annualized Return | Annualized Volatility | Sharpe Ratio | Max Drawdown |
|---|---:|---:|---:|---:|
| HMM regime strategy | 12.7% | 12.9% | 1.00 | -23.5% |
| SPY buy-and-hold | 17.9% | 19.5% | 0.94 | -33.7% |
| 60/40 SPY/TLT | 10.1% | 12.5% | 0.83 | -27.7% |

In the held-out test period from 2022 onward, the HMM strategy was especially useful compared with static 60/40 allocation, which struggled during the stock-bond selloff.

## Interpretation

The project supports the idea that regime-aware allocation can be useful as a risk analytics framework. The HMM does not forecast exact market returns. Instead, it estimates changing market conditions and uses those estimates to guide portfolio risk exposure.

The strategy is best understood as a disciplined allocation overlay rather than a production trading system.

## Limitations

Key limitations include:

- results are historical evidence, not proof of future performance;
- major stress regimes are rare, so stress-period conclusions are uncertain;
- monthly regime signals can react slowly to sudden crashes;
- regime labels and allocation weights require human judgment;
- the asset universe and implementation assumptions are intentionally simplified.

## Repository Structure

```text
.
+-- docs/
|   +-- index.html                         # Rendered HTML report for GitHub Pages
+-- notebooks/
|   +-- market_regime_allocation_research.ipynb
+-- .env.example                           # Example environment variables
+-- .gitignore
+-- README.md
+-- requirements.txt
```

Local files ignored by git include:

- `.env`
- `data/raw/`
- `data/processed/`
- `docs/*_executed.ipynb`
- `PROJECT_STRUCTURE.md`

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

Create a local `.env` file using `.env.example` as a template:

```text
TIINGO_API_KEY=your_tiingo_api_key
FRED_API_KEY=your_fred_api_key
```

Then run the notebook from the repository root.

## Disclaimer

This project is for educational and research purposes only. It is not financial advice, investment advice, or a live trading strategy.
