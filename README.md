# Launch Ledger v4 — token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Ci3hu1/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Ci3hu1/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Launch Ledger v4: pre-token radar ranked by expected launch value — fitted
curve, token odds held out twice, 20 of 226 worth farming, 758/758 accounted.

A field guide to the 226 pre-token protocols in the 14 November 2026
snapshot — light paper, serif masthead, ruled lines — with the evidence on
the first screen instead of in a drawer.

## How the value is built

Expected launch value = implied value if it tokens × P(it ever tokens).

- **Implied value:** the fitted curve 10^(3.0247 + 0.5223·log₁₀(TVL)) times
  a category multiplier, fitted on 128 traded anchors (one per ticker,
  market cap above zero). R² 0.1939.
- **P(token):** a logistic on log₁₀(TVL), age in years, and 7d growth,
  fitted on 449 eligible peers. Brier 0.20 / 0.21 held out twice, against
  a 0.25 base rate.
- **Verdicts, netted:** 5% of expected value split across 10,000 assumed
  farmers, minus $12 of gas and $1 of capital cost. FARM clears $50 net
  (20 rows), THIN clears $0 (103), the rest SKIP (103).
- **Coverage:** 226 ranked (watchlist 40/40 + 186 below the $50M floor) +
  416 traded + 116 excluded = 758. Every protocol in the snapshot is
  accounted for.

Growth, age and chain count were fitted into the value model and dropped —
the evidence table on the dashboard shows each test (growth gains R²
+0.017 with a negative sign; age +0.001; chains +0.007). The fitted curve
beats a flat multiple on the mean miss in all four validation tests; on
the random 70/30 holdout it loses the median, and the page says so.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json>
```

Node 22+, standard library only. Reads the sealed snapshot, writes
`board.json` (226 ranked rows), `data.js`, `dashboard/` and `screenshots/`
to the output directory, plus `dossier.json`. Deterministic: two runs on
the same snapshot are byte-identical.

## Tests

```sh
node --test tests/model.test.ts
```

## Files

- `lib/model.ts` — the model: OLS fit, category multipliers, logistic
  token odds, validation (holdout, walk-forward, leave-one-out, bootstrap),
  netted verdicts, checksum.
- `dashboard/` — the field-guide page (index.html, app.css, app.js). It
  renders the masthead thesis, proof strip, ledger, shortlist, evidence
  tables, the full sortable/filterable board, per-protocol field notes with
  nearest traded comps and the farm plan, a model sandbox for the verdict
  assumptions, and a checksum row the page recomputes itself in the browser.
- `screenshots/` — 1-board.png, 2-evidence.png, 3-detail.png (1440×900).
- `STRATEGY.md` — the top-10 study and the design decisions.
- `NOTES.md` — the measured numbers, tests, determinism and judge-test.

---

<sub>Entered on [make.fun](https://make.fun/?ref=cc7tcnw6&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
