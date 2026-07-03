# fxverify report - SAMPLE_PASS

**Verdict: PASS**

This does not certify profitability; it documents robustness checks.

## Strategy
- name: sma_crossover
- params: fast=3, slow=6

## Audit summary
- verdict: GO
- reason: GO: estimated 50.0 trades vs gate 20 (drop<0.5x, pivot<1.0x), pairs 1/1 required

## Red-flag checklist
| item | status | detail |
|---|---|---|
| Min-trades gate | OK | All evaluated folds met the min-trades floor. |
| Parameter OOS drift | WARN | 4/10 parameter sets passed; verdict_flip=true, pf_range=62.04, sharpe_range=6.85. |
| Look-ahead risk | OK | Signals were stable across truncated probes; fills still use same-bar close policy. Same-bar close fills are used by this simulator. |

## Parameter robustness
Drift summary: 4/10 parameter sets passed; verdict_flip=true; pf_range=62.04; sharpe_range=6.85.

| params | PF | Sharpe | trades | OOS pass ratio | verdict |
|---|---|---|---|---|---|
| fast=3, slow=6 | 62.0438 | 2.7488 | 21 | 1.00 | PASS |
| fast=3, slow=8 | 9.99 | 3.9532 | 20 | 1.00 | PASS |
| fast=4, slow=10 | 9.99 | 2.2832 | 20 | 1.00 | PASS |
| fast=5, slow=12 | 9.1452 | 0.6504 | 20 | 1.00 | PASS |
| fast=5, slow=15 | 0.1219 | -0.8848 | 20 | 0.00 | FAIL_STRATEGY |
| fast=6, slow=18 | 0.0263 | -1.8037 | 20 | 0.00 | FAIL_STRATEGY |
| fast=8, slow=20 | 0.0135 | -2.4696 | 20 | 0.00 | FAIL_STRATEGY |
| fast=8, slow=24 | 0.0114 | -2.5737 | 20 | 0.00 | FAIL_STRATEGY |
| fast=10, slow=30 | 0.0 | -2.8989 | 20 | 0.00 | FAIL_STRATEGY |
| fast=12, slow=36 | 0.0147 | -2.3059 | 20 | 0.00 | FAIL_STRATEGY |

## Data period
- start: 2024-01-01 00:00:00
- end: 2024-03-24 07:00:00
- bars: 2000
- symbol: SAMPLE_PASS

## Assumptions
- spread: 5e-05
- fee: 5e-05
- contract_multiplier: 100000.0

## Fold settings
- train_bars: 200
- test_bars: 100
- folds: 4
- min_oos_pass_ratio: 0.6
- min_trades_floor: 5

## OOS pass ratio: 1.00

## Aggregate metrics
| PF | max DD% | Sharpe | trades |
|---|---|---|---|
| 62.0438 | 0.0373 | 2.7488 | 21 |

## Folds
| fold | PF | DD% | Sharpe | trades | verdict |
|---|---|---|---|---|---|
| 1 | 18.3076 | 0.0373 | 1.5104 | 6 | PASS |
| 2 | 9.99 | 0.0 | 10.205 | 5 | PASS |
| 3 | 9.99 | 0.0 | 3.5665 | 5 | PASS |
| 4 | 9.99 | 0.0 | 6.0854 | 5 | PASS |

## Reproducibility
- input file hash: 9c06b03860a62f30e6384d3ca963de9706fe63ac9514339f9462aa70792a7661
- config hash: 0f3419a642025c6ccb8afc5a271592030d53f6d9f4e7ad779899e06ce11a1004