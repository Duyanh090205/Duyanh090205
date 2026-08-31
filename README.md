# Duy Anh Nguyen

Undergraduate at the University of South Florida. Applying for 2027 quantitative researcher
and trader roles.

### **→ [Full case studies with the numbers behind them](https://github.com/Duyanh090205/portfolio)**

---

## [WC2026 Monte Carlo](https://github.com/Duyanh090205/wc2026-monte-carlo) — the locked pre-tournament top four were the exact four semifinalists

A tournament simulator that prices outright (champion) markets, then tracked itself against
Polymarket and Kalshi for all 41 days of the World Cup.

The model was **locked on 10 June 2026, before the first match**, and never re-fitted — the
daily rerun re-conditions on locked results only. Every number below is out-of-sample.

|  | Model | Polymarket | Outcome |
|---|---|---|---|
| Spain to win | **19.11%** | 16.45% | Spain won |
| Top 4 by semifinal probability | Spain · France · England · Argentina | — | **all four reached the semifinals** |

- **25 of 31 knockout ties called correctly (80.6%)** — two-way Brier score, the mean squared
  error of probability forecasts, of **0.156** against a 0.25 coin-flip baseline
- More confident than the de-vigged market on *all four* correct semifinalists
  (43.9 vs 40.0, 39.6 vs 37.3, 34.5 vs 31.0, 32.0 vs 27.4) — the edge was directional across
  the top of the book, not one lucky team
- Five of the six knockout misses sat in the 50–64% band. No high-confidence blow-ups.
- 1,000,000 simulations per day, 41 consecutive days, unattended in CI. 384 tests.

Sole author of the simulator. Parameters selected by leave-one-tournament-out
cross-validation across 12 historical tournaments, with a two-standard-error guard against
accepting a marginal winner. Nothing was ever tuned on market prices.

## [Prediction-Market Exchange](https://github.com/Duyanh090205/prediction-market-exchange)

A working exchange, built from the matching engine up — not a simulation of one. Built as
the engine for a private trading game; it has not been opened to outside users.

- **Central limit order book** with price–time priority, LIMIT and MARKET orders, atomic
  multi-level sweeps, `SELECT FOR UPDATE` locking so concurrent fills cannot double-spend a quote
- **Margin engine** reserving against worst-case aggregate P&L, swept across the whole strike
  ladder, and checked twice — once at submission, again inside the execution transaction,
  because the first check is stale by the time it matters
- **Atomic settlement** — positions, balances and P&L move in one transaction or not at all
- **103 unit tests**, ~15.6k lines: Next.js 15, PostgreSQL, Prisma, Socket.IO

I designed and built the matching engine, margin engine and settlement layer — the entire
trading core, and 88% of the codebase. The remainder is deployment configuration for the
original host and its SSO bridge, contributed by teammates.

## [Pairs Trading Engine](https://github.com/Duyanh090205/pairs-trading-engine) — a strategy I killed

Three months building a statistical arbitrage pipeline, then finding it didn't work. The result
is negative. That is the point of the project.

- **Zero pairs survived** the full filter funnel over 12 months of 2022 data — an all-pairs
  cointegration scan across the S&P 500 with Benjamini–Hochberg correction. Roughly 125,000
  hypothesis tests; correcting for that honestly leaves nothing
- Static OLS hedge ratios drift **25.5%** in a year, so hedge ratios come from a 2-D Kalman filter
- **Four classes of look-ahead bias injected into 20 deliberately corrupted datasets** to
  measure how much each inflates Sharpe. Full-dataset normalization leakage is the dangerous
  one: it inflates only moderately, which is exactly what makes it near-undetectable
- 45-fold monthly walk-forward validation, 2022–2026, defended across bull and bear regimes

## [Natural-Gas Storage Pricing](https://github.com/Duyanh090205/natgas-storage-pricing)

Harmonic regression on a gas price curve feeding a storage-contract pricer. Out-of-sample
walk-forward, it beats SARIMA and both naive benchmarks on every metric — MAE 0.179 against
0.253 for SARIMA and 0.574 for seasonal naive, the only baseline that counts.

The result worth reading is the pricing one: the optimal storage trade is **not** the widest
seasonal spread. Holding longer earns more spread but pays more rent, and the optimum lands
in early winter — buy September, sell December, about $823K, with a break-even storage fee
near $212K/month. Built from the JPMorgan Forage brief and extended well past it.

## Bond fund flow-performance research — research assistant

Research assistant to Prof. Gunsu Son, University of South Florida, since October 2025.
Authorship has not been determined. No code, data, figures or results from this work are
published here.

The work: building a panel from CRSP mutual fund share-class data — 10M+ raw records
reduced to a 400K+ bond fund-month panel (1992–2014) and a 1.2M-observation equity panel —
and replicating Goldstein, Jiang & Ng (2017, *JFE*) Table 2 on it, reproducing the
published specification to adj. R² 0.066 against the paper's 0.065, with Stata cross-checks.

From there, the same relationship estimated with a ladder of methods on identical
chronological splits: hinge OLS, a Robinson partially linear model (Numba-JIT local-linear
kernel, Fan–Gijbels bandwidth), a partial-linear neural network in Keras, and 17 AutoML
models (Optuna GBMs, AutoGluon, H2O, EBM). Alongside it, a data-quality audit of extreme
observations, machine-precision regression guards (Δ ≈ 1e-16), and a pytest suite.

Findings are with my advisor and are not described here.

---

## Contact

[LinkedIn](https://linkedin.com/in/duyanh0902) · duyanhtrannguyen@usf.edu
