# Mean Reversion Quant Strategy

## Overview

This project builds and evaluates a simple mean-reversion trading strategy using historical market data. The main idea is that when an asset price moves far below its recent average, it may be temporarily undervalued and could revert back toward its average.

The strategy uses a rolling moving average and rolling standard deviation to calculate a z-score signal. It then enters a long position when the price is significantly below its recent average and exits when the price returns closer to normal.

This project is intended as a beginner-friendly quantitative finance research project focused on data analysis, signal generation, backtesting, and performance evaluation.

## Research Question

Can short-term deviations from a moving average be used to create a profitable mean-reversion strategy on liquid ETFs such as SPY or QQQ?

## Hypothesis

If the price of an ETF falls far below its recent moving average, the price may have a higher probability of reverting upward in the near future.

## Strategy Logic

The strategy calculates:

- Daily returns
- Rolling moving average
- Rolling standard deviation
- Z-score of price relative to the moving average

The z-score is defined as:

```text
z = (current price - rolling mean) / rolling standard deviation
```

Trading rule:

```text
If z-score < -2: enter long position
If z-score > 0: exit position
Otherwise: keep current position
```

A one-day shift is applied to the trading signal to avoid lookahead bias. This means that a signal generated today can only affect the position starting tomorrow.

## Data

The project uses historical daily price data downloaded with `yfinance`.

Example assets:

- SPY
- QQQ
- IWM
- XLK
- XLF

The initial test uses SPY from 2015 to 2025.

## Tools and Libraries

```bash
Python
Jupyter Notebook
pandas
NumPy
matplotlib
SciPy
statsmodels
scikit-learn
yfinance
```

Install dependencies:

```bash
pip install numpy pandas matplotlib scipy statsmodels scikit-learn yfinance
```

## Project Structure

```text
mean-reversion-quant-project/
│
├── data/
├── notebooks/
│   └── 01_exploration.ipynb
│
├── src/
│   ├── data_loader.py
│   ├── signals.py
│   ├── backtest.py
│   └── metrics.py
│
├── results/
│   └── plots/
│
├── README.md
└── requirements.txt
```

## Backtesting Method

The backtest compares the mean-reversion strategy against a simple buy-and-hold benchmark.

The strategy return is ca