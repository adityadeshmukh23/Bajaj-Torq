# Figures

This directory is reserved for generated figures supporting the analysis in
[`../../docs/`](../../docs/).

**Status: empty.** No figures are committed yet. The plots shown in the original
TORQ 2026 design deck were presentation graphics rather than generated output,
and are deliberately not reproduced here — the underlying values live in
[`../../data/`](../../data/) instead, so that any figure generated from them is
traceable to a sourced number.

Planned figures, each driven by `data/results.yaml`:

| File | Content | Source data |
|---|---|---|
| `cam_profile.svg` | Front:rear force ratio vs lever travel (65:35 → 72:28) | `results.yaml → cam_profile` |
| `axle_load_transfer.svg` | Static vs dynamic axle load, with weight transfer | `results.yaml → braking_dynamics` |
| `sn_curve.svg` | EN31 S-N curve with operating point | `results.yaml → fatigue_life` |
| `cost_breakdown.svg` | BOM line-item breakdown, ₹625 gross → ₹510 net | `data/bom.csv` |
| `benchmark_scatter.svg` | MFDD vs unit cost across four architectures | `data/benchmark.csv` |
