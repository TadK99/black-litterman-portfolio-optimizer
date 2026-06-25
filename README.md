[README.md](https://github.com/user-attachments/files/29358842/README.md)
# Black-Litterman Portfolio Optimization Engine

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TadK99/black-litterman-portfolio-optimizer/blob/main/Black_Litterman_Portfolio_Optimizer.ipynb)

A from-scratch implementation of the **Black-Litterman model** — the Bayesian
framework institutional asset managers use to combine market-implied
equilibrium returns with subjective investor views, producing far more stable
portfolio weights than naive historical-mean mean-variance optimization.

## What it does

1. Pulls live price + market-cap data for a 10-stock equity universe via `yfinance`
2. Reverse-engineers market-implied equilibrium returns from market-cap weights (the BL "prior")
3. Blends in investor views (absolute + relative), each scaled by a confidence level
4. Produces posterior expected returns via the closed-form BL formula
5. Runs max-Sharpe mean-variance optimization on the blended estimates
6. Benchmarks against naive historical-mean optimization and raw market-cap weighting

## Why this matters

Plugging raw historical average returns into a Markowitz optimizer is
notoriously unstable — small estimation errors can swing a portfolio from
heavily long one stock to heavily short it. Black-Litterman (Goldman Sachs,
1990) fixes this by anchoring expected returns to what the market already
implies, and only nudging them based on views you actually hold conviction in.

## Sample output

| Market-Cap Weights | Efficient Frontier |
|---|---|
| ![weights](outputs/weights_comparison.png) | ![frontier](outputs/efficient_frontier.png) |

## Tech stack

`Python` · `yfinance` · `NumPy` · `SciPy` · `scikit-learn` (Ledoit-Wolf shrinkage) · `pandas` · `matplotlib` / `seaborn`

## Run it yourself

**Option 1 — Colab (recommended, zero setup):**
Click the badge above.

**Option 2 — Local:**
```bash
git clone https://github.com/YOUR_USERNAME/black-litterman-portfolio-optimizer.git
cd black-litterman-portfolio-optimizer
pip install -r requirements.txt
jupyter notebook Black_Litterman_Portfolio_Optimizer.ipynb
```

## Configuration

Everything tunable lives in one `CONFIG` dict at the top of the notebook —
swap the stock universe, lookback window, or investor views without touching
any engine code.

## Project structure

```
black-litterman-portfolio-optimizer/
├── Black_Litterman_Portfolio_Optimizer.ipynb
├── README.md
├── requirements.txt
└── outputs/
    ├── bl_weights.csv
    ├── efficient_frontier.png
    ├── weights_comparison.png
    ├── correlation_heatmap.png
    └── final_allocation_pie.png
```

## Possible extensions

- Idzorek's method for more intuitive view-confidence specification
- Rolling backtest of BL vs. buy-and-hold over historical periods
- Factor-model (Fama-French) covariance estimation
- Streamlit dashboard with live confidence-level sliders

## License

MIT
