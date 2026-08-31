# Duy Anh Nguyen

Quantitative research — probabilistic modelling, market microstructure, and the
unglamorous half of the job: proving a backtest isn't lying to you.

Undergraduate at the University of South Florida. Applying for 2027 quantitative
researcher and trader roles.

---

## Selected work

### WC2026 Monte Carlo — an outright pricing model, locked before kickoff

A tournament simulator that prices outright (champion) markets, then tracked itself
against Polymarket and Kalshi for the full 41 days of the World Cup.

The model was **locked on 10 June 2026, before the first match**, and never re-fitted
during the tournament — the daily rerun re-conditions on locked results only. Every
number below is out-of-sample.

|  | Model | Polymarket | Outcome |
|---|---|---|---|
| Spain to win | **19.11%** | 16.45% | Spain won |
| Top 4 by semifinal probability | Spain · France · England · Argentina | — | **all four reached the semifinals** |

- **25 of 31 knockout ties called correctly (80.6%)** — two-way Brier **0.156** against a
  0.25 coin-flip baseline
- The model was more confident than the market on *all four* correct semifinalists
  (43.9% vs 40.0%, 39.6% vs 37.3%, 34.5% vs 31.0%, 32.0% vs 27.4%) — the edge was
  directional, not one lucky team
- Five of the six knockout misses sat in the 50–64% band. No high-confidence blow-ups.
- 1,000,000 simulations per day, 41 consecutive days, run unattended in CI

Group stage, for completeness: 63.9% W/D/L hit rate, multiclass Brier 0.514 against a
1/3-each ignorance baseline of 0.667. That baseline is a sanity check, not a benchmark —
the knockout figures above are the ones worth reading.

Python · NumPy · Elo reconstruction + squad market value · Poisson goal grid ·
leave-one-tournament-out CV across 12 tournaments

---

### [Prediction-Market Exchange](https://github.com/Duyanh090205/prediction-market-exchange)

A working exchange, built from the matching engine up — not a simulation of one.

- **Central limit order book** with price–time priority, LIMIT and MARKET orders,
  atomic multi-level sweeps
- **Margin engine** that reserves against worst-case loss, checked twice: once when an
  order is submitted, again at execution
- **Atomic settlement** — positions, balances and P&L move in a single transaction or
  not at all
- UUIDv7 idempotency keys, CSRF protection, rate limiting, structured logging
- **103 unit tests** across matching, margin and P&L
- ~15.6k lines: Next.js 15, PostgreSQL, Prisma, Socket.IO over a custom Node server

I designed and built the matching engine, margin engine and settlement layer — 88% of
the codebase. Deployment configuration and the SSO integration were contributed by
teammates.

---

### [Pairs Trading Engine](https://github.com/Duyanh090205/Pairs-Trading-Engine-Backtest) — a strategy I killed

Six weeks building an institutional-grade statistical arbitrage pipeline, and then
finding it didn't work. The result is negative. That is the point of the project.

- Engle–Granger and Johansen cointegration scans across the S&P 500 with
  Benjamini–Hochberg FDR correction — **zero pairs survived the full filter funnel**
  over 12 months of 2022 data
- Static OLS hedge ratios drift **25.5%** over a year, so hedge ratios are estimated
  with a 2-D Kalman filter instead
- **Deliberately injected four classes of look-ahead bias into 20 corrupted datasets**
  to measure how much each inflates Sharpe. Full-dataset normalisation leakage is the
  dangerous one: it inflates moderately and is close to undetectable from the data
  file alone
- 45-fold monthly walk-forward validation, 2022–2026, defended across bull and bear
  regimes with one-at-a-time sensitivity analysis

Numba · Kalman filtering · microstructure-aware cost modelling · paper-trading deployment

---

### Natural-gas storage pricing

Harmonic regression on natural-gas forward curves (K=3 chosen by AIC) with closed-form
prediction intervals, feeding a seasonal storage-contract pricer. Extended well past the
original brief with credit-risk and FICO-bucketing work.

### Bond fund outflows — research assistant

Research assistant to Prof. Gunsu Son. Authorship has not been determined; no code, data
or results from this work are published here.

---

## Contact

[LinkedIn](https://linkedin.com/in/duyanh0902) · duyanhtrannguyen@usf.edu
