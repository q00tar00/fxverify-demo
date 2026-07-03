# How to read the three red flags

Every fxverify evidence pack opens with the same three-row checklist. This page
explains what each flag means, using the real numbers from the sample failing
pack ([`evidence_pack/fail/report.md`](evidence_pack/fail/report.md)) and the
sample passing pack ([`evidence_pack/pass/report.md`](evidence_pack/pass/report.md)).

> This does not certify profitability; it documents robustness checks.

The checklist has three statuses: **OK** (nothing suspicious), **WARN** (worth a
second look), **FLAG** (a serious overfit / validity concern).

---

## 1. Min-trades gate

> *Did any fold trade too little to mean anything?*

A walk-forward run splits the data into folds and tests each out-of-sample. If a
fold only produced a handful of trades, its metrics are noise — a profit factor
of 9 on 3 trades tells you nothing.

- **In the failing pack:** `OK` — every evaluated fold met the min-trades floor,
  so the failure is *not* an artifact of too-few trades. The strategy genuinely
  loses.
- **In the passing pack:** `OK` — folds cleared the floor (5+ trades each).

**Why a seller should care:** buyers who know what they're doing discount any
result built on tiny trade counts. Showing the min-trades gate passed removes
that objection up front.

---

## 2. Parameter OOS drift

> *Does the edge survive neighboring parameter sets, or does the verdict flip
> outside the tuned point?*

This is the single most important overfit test. fxverify re-runs the strategy
across a grid of nearby parameter values and checks whether the verdict is
stable. If the strategy only "works" at one exact parameter setting, you have
curve-fit to the past.

- **In the failing pack:** `FLAG` — **0/10** parameter sets passed;
  `verdict_flip=true`, `pf_range=0.32`, `sharpe_range=0.95`. Every neighbor
  fails, and the Sharpe swings across a wide range. Classic overfit signature:
  no robust edge, just a point that happened to look okay.
- **In the passing pack:** `WARN` — **4/10** parameter sets passed. The edge
  survives in a neighborhood around the tuned point, but not everywhere, so it's
  flagged as WARN rather than OK. Honest: a real edge that still has boundaries.

**Why a seller should care:** this is what separates "I found a curve fit" from
"I found something that generalizes." A buyer who sees `0/10` neighbors passing
knows the strategy is fragile before they risk a cent.

---

## 3. Look-ahead risk

> *Do signals stay stable when the future is truncated?*

Look-ahead bias — accidentally using data the strategy couldn't have known at
decision time — is one of the most common ways a backtest lies. fxverify probes
this by truncating the future and checking whether the historical signals stay
the same. If they change, the strategy was peeking.

- **In both packs:** `OK` — signals were stable across truncated probes, and
  fills use a same-bar close policy (disclosed in the report, not hidden). No
  evidence of look-ahead.

**Why a seller should care:** a strategy that changes its past decisions when you
hide the future is using information it wouldn't have live. Passing this check is
table stakes for a credible backtest.

---

## Putting it together

The failing sample earns a top-line **`FAIL_STRATEGY`** verdict driven almost
entirely by red flag #2 (parameter OOS drift). The min-trades gate and
look-ahead checks are clean — so the pack tells an honest story: *there are
enough trades and no look-ahead cheating, the strategy simply does not
generalize.*

That is exactly the kind of "before" artifact that builds trust with a buyer.
Publishing the failing pack alongside a passing one shows you test strategies
the same way whether they pass or fail — which is the whole value proposition of
an evidence pack.
