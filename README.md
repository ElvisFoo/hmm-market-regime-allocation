# HMM Market Regime Allocation

This project explores whether Hidden Markov Models (HMMs) can be used to identify market regimes and support a systematic, risk-aware ETF allocation strategy.

The goal is not simply to maximize returns, but to investigate whether regime-aware allocation can improve risk-adjusted performance, reduce drawdowns, and provide a more structured way to think about changing market conditions.

## View Rendered Report

The research notebook is also exported as an HTML report for easier reading:

[Open the rendered project report](https://elvisfoo.github.io/hmm-market-regime-allocation/)

## Project Motivation

Markets behave differently across time. A portfolio that performs well in a calm growth environment may behave very differently during a crisis, inflation shock, or high-volatility regime.

This project aims to answer:

> Can market and macroeconomic signals be used to identify probabilistic market regimes, and can those regimes guide portfolio allocation decisions?

## Planned Asset Universe

The initial ETF universe is:

| ETF | Role |
|---|---|
| SPY | U.S. equities / growth exposure |
| TLT | Long-term U.S. Treasuries / duration hedge |
| GLD | Gold / inflation and uncertainty hedge |
| SHY | Short-term U.S. Treasuries / defensive cash-like exposure |

## Planned Methodology

The project will follow a research workflow:

1. Collect ETF price data and macroeconomic data.
2. Engineer market and macro risk features.
3. Train Hidden Markov Models to identify latent market regimes.
4. Interpret the regimes using asset returns, volatility, drawdowns, and macro conditions.
5. Define transparent allocation rules for each regime.
6. Backtest the regime-aware strategy using walk-forward validation.
7. Compare results against static benchmarks such as SPY, 60/40, and equal-weight allocation.

## Key Evaluation Metrics

The strategy will be evaluated using:

- CAGR
- annualized volatility
- Sharpe ratio
- Sortino ratio
- maximum drawdown
- Calmar ratio
- turnover
- performance during stress periods

## Current Status

The project currently covers project motivation, asset universe design, data sourcing, feature engineering, HMM intuition, candidate regime model training, and regime interpretation.

## Disclaimer

This project is for educational and research purposes only. It is not financial advice or a live trading strategy.
