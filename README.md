# Daily Stat-Arb Pipeline: 2800.HK vs Hang Seng Index Basket

**Status**: Personal / interview project (not live trading)

## Motivation
Demonstrate classic statistical arbitrage pipeline under real-world Hong Kong market data constraints (poor intraday reliability via Yahoo Finance in 2025–2026).  
Focus: hedge ratio stability, cost-aware backtesting, signal realism on efficient ETF.

## What it does
- Dynamic market-cap weighted synthetic index from ~90 HSI constituents
- Blended hedge ratio (log-prices + price-ratio normalization)
- Z-score based mean-reversion signals
- Parameter sweep + explicit transaction cost modeling (8/12/16 bps round-trip)
- Realistic metrics: Sharpe, drawdown, turnover, hold period

## Key Results

| Param set       | Cost (bps) | Trades | Ann. Return | Sharpe | Max DD | Win % | Avg Hold (days) | Turnover (×/yr) |
|-----------------|------------|--------|-------------|--------|--------|-------|-----------------|-----------------|
| Aggressive      | 8          | 5      | 26%         | 0.79   | -14%   | 80%   | 11              | 2.6             |
| Very Conservative | 8        | 3      | 4%          | 0.11   | -15%   | 67%   | 14              | 1.5             |

**Takeaway**: Modest edge possible in simulation, but collapses under realistic HK costs/slippage → aligns with tight premium/discount of TraHK.

## Limitations & Lessons
- Very low trade frequency (sampling noise dominant)
- No volatility targeting / position sizing yet
- Efficient ETF → daily arb edge is minimal (better intraday or stress periods)
- Learned: cost modeling & hedge ratio debugging are critical

## Tech stack
Python • yfinance • pandas • statsmodels • matplotlib • backtrader (exploratory)

## How to run
```bash
pip install -r requirements.txt
jupyter notebook main_notebook.ipynb
