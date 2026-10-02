# NIDS-EFS Web Decision Tool — Final Version

This version uses your final, verified benchmark and AHP data (post Ensemble
fix, real TCO formula, real model sizes).

## What's real here

- **Benchmark metrics** (`data/benchmark.json`): all 32 model-dataset
  measurements, copied directly from your actual `benchmark_runner.py` and
  `cnn_lstm_runner.py` console output. Ensemble_RF_XGB's `throughput` and
  `memory_mb` are `null` (not fabricated) because your latest benchmarking
  run printed training time and latency for the ensemble, but did not print
  memory or throughput — if you have the real values in your saved
  `benchmark_results_v2.csv`, replace the two `null`s in those 4 Ensemble
  rows with the real numbers.
- **AHP composite scores** (`data/ahp_scores.json`): copied directly from
  your `ahp_scorer.py` console output (empirical weights, per-dataset and
  mean). XGBoost ranks first; Ensemble now ranks lower, reflecting its real
  (no longer zeroed-out) latency.
- **Criterion weights** (`data/weights.json`): empirical weights, Section 4.4.
- **TCO**: computed live in the browser from each model's real training
  time and throughput, using the same formula as `tco_calculator.py`
  (included here for reference). Ensemble shows "pending" since its
  throughput wasn't captured.

## Hosting on GitHub Pages

1. Push this folder's contents to a new GitHub repository.
2. Settings → Pages → Deploy from branch → `main` / root.
3. You'll get a live URL within a minute, typically
   `https://<username>.github.io/<repo-name>/`.
4. Share that URL with SUS participants.

## Editing data later

Edit any file in `data/` directly on GitHub (pencil icon → edit → commit).
The live page picks up changes automatically on refresh, no redeploy needed.

## Running locally before you push

```bash
python -m http.server 8000
```
Then open `http://localhost:8000`. Opening `index.html` by double-clicking
will NOT work — browsers block local file fetch() for security reasons.

## Filling the Ensemble data gap

If you re-run `benchmark_runner.py` (or already have the real
memory/throughput values saved from your last run), update the 4
`Ensemble_RF_XGB` rows in `data/benchmark.json`: replace `null` in the
throughput (7th) and memory (8th) positions with the real numbers. Once
that's done, the Ensemble's TCO will compute automatically too.
