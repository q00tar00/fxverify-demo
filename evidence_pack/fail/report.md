# fxverify report - SAMPLE_FAIL

**Verdict: FAIL_STRATEGY**

This does not certify profitability; it documents robustness checks.

## Strategy
- name: sma_crossover
- params: fast=3, slow=8

## Audit summary
- verdict: GO
- reason: GO: estimated 20.0 trades vs gate 20 (drop<0.5x, pivot<1.0x), pairs 1/1 required

## Red-flag checklist
| item | status | detail |
|---|---|---|
| Min-trades gate | OK | All evaluated folds met the min-trades floor. |
| Parameter OOS drift | FLAG | 0/10 parameter sets passed; verdict_flip=true, pf_range=0.32, sharpe_range=0.95. |
| Look-ahead risk | OK | Signals were stable across truncated probes; fills still use same-bar close policy. Same-bar close fills are used by this simulator. |

## Parameter robustness
Drift summary: 0/10 parameter sets passed; verdict_flip=true; pf_range=0.32; sharpe_range=0.95.

| params | PF | Sharpe | trades | OOS pass ratio | verdict |
|---|---|---|---|---|---|
| fast=3, slow=6 | 0.1458 | -0.8258 | 45 | 0.00 | FAIL_STRATEGY |
| fast=3, slow=8 | 0.1288 | -0.8374 | 31 | 0.00 | FAIL_STRATEGY |
| fast=4, slow=10 | 0.2683 | -0.5105 | 21 | 0.00 | FAIL_STRATEGY |
| fast=5, slow=12 | 0.2658 | -0.5066 | 17 | 0.00 | FAIL_STRATEGY |
| fast=5, slow=15 | 0.3175 | -0.4309 | 17 | 0.00 | FAIL_STRATEGY |
| fast=6, slow=18 | 0.2388 | -0.6268 | 13 | 0.00 | FAIL_STRATEGY |
| fast=8, slow=20 | 0.1087 | -0.9518 | 10 | 0.00 | FAIL_STRATEGY |
| fast=8, slow=24 | 0.0 | 0.0 | 0 | 0.00 | INSUFFICIENT_DATA |
| fast=10, slow=30 | 0.0 | 0.0 | 0 | 0.00 | INSUFFICIENT_DATA |
| fast=12, slow=36 | 0.0 | 0.0 | 0 | 0.00 | INSUFFICIENT_DATA |

## Data period
- start: 2024-01-01 00:00:00
- end: 2024-02-03 07:00:00
- bars: 800
- symbol: SAMPLE_FAIL

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

## OOS pass ratio: 0.00

## Aggregate metrics
| PF | max DD% | Sharpe | trades |
|---|---|---|---|
| 0.1288 | 0.5282 | -0.8374 | 31 |

## Folds
| fold | PF | DD% | Sharpe | trades | verdict |
|---|---|---|---|---|---|
| 1 | 0.3438 | 0.1212 | -0.4227 | 7 | FAIL_STRATEGY |
| 2 | 0.1737 | 0.1883 | -0.7864 | 9 | FAIL_STRATEGY |
| 3 | 0.0 | 0.14 | -1.4293 | 8 | FAIL_STRATEGY |
| 4 | 0.0 | 0.1409 | -1.0812 | 7 | FAIL_STRATEGY |

## Fail reasons
- oos_pass_ratio 0.00 < 0.6
- aggregate PF 0.1288 < 1.1
- aggregate Sharpe -0.8374 < 0.05

## Reproducibility
- input file hash: 644c8e9e289b9a5ab1d746b28788efb136812d79de02687a57cf666059ae9726
- config hash: 0f3419a642025c6ccb8afc5a271592030d53f6d9f4e7ad779899e06ce11a1004