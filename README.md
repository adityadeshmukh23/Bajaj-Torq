# Bajaj-Torq — Variable-Ratio Cam Combined Braking System

> A documented design study for a low-cost, purely mechanical Combined Braking
> System (CBS) for entry-level electric two-wheelers.
> Winner, In-Campus Hackathon Round — Bajaj Auto **TORQ 2026** (National Level
> Campus Challenge).

---

## ⚠️ Scope and methodology

**This repository documents and presents a completed design analysis.**

All engineering results here were **derived analytically by hand** and are
reproduced with their formulas, inputs and substituted values shown. Nothing in
this repository was produced by a live solver, and **no physical prototype was
built or road-tested**. Where this document refers to a "50,000 km design life"
or similar, that is an **analytically calculated** figure, not a measured or
field-validated one.

See [`docs/09-limitations.md`](docs/09-limitations.md) for the full statement of
what this analysis does and does not establish.

---

## Problem statement

Entry-level electric two-wheelers in the Indian market show observed
decelerations of approximately **4.2–4.5 m/s²**, against the IS 14664:2010
Category 3-3 CBS requirement of **5.4 m/s² at 60 km/h** — a shortfall of roughly
**18–22%** relative to the regulatory benchmark. In a segment where about
**1.28 million** electric two-wheelers were sold in India in 2025 and where
entry-level models are the fastest-growing share, this gap matters: observed
budget-EV stopping distances of **35–36 m** at 60 km/h sit well beyond the
**31.6 m** IS limit, and a four-metre increase in stopping distance at that speed
significantly increases crash severity. Hydraulic CBS architectures close the
performance gap but at roughly **₹2,800 per unit**, which is economically
prohibitive at this price point. This study documents a variable-ratio,
cam-driven mechanical CBS intended to reach regulatory compliance at a target
unit cost below ₹600.

---

## Results summary

All values below are **analytically calculated design values**.

| Metric | This design | Reference | Margin |
|---|---|---|---|
| Peak MFDD @ 60 km/h | **6.12 m/s²** | 5.40 m/s² (IS 14664 min) | +13.3% ¹ |
| Stopping distance @ 60 km/h | **28.7 m** | 31.6 m (IS 14664 limit) | −9.2% ¹ |
| Hand lever force | **180 N** | ≤ 200 N (IS 14664) | 10% margin |
| Secondary brake, front only | **4.4 m/s²** | ≥ 2.5 m/s² (Cl. 4.1.9) | +76% |
| Secondary brake, rear only | **2.9 m/s²** | ≥ 2.5 m/s² (Cl. 4.1.9) | +16% |
| Unit cost (post batch discount) | **₹510** | ₹2,800 (hydraulic CBS) | −82% |
| Cost per m/s² of MFDD | **₹83** | ₹431 (hydraulic CBS) | −81% |
| Peak contact stress (POM follower) | **75.6 MPa** | 110 MPa (POM allowable) | SF = 1.46 |
| Design life | **50,000 km** | — | analytically calculated |

¹ Derived from the two source values in the same row. **Note:** the source deck
states "+20% above IS 14664 minimum" and "+14%" on stopping distance; neither
reconciles with the stated 5.40 m/s² and 31.6 m baselines.
See [`docs/08-is14664-compliance.md`](docs/08-is14664-compliance.md).

### Architecture comparison

| Parameter | This CBS | Hydraulic CBS | Basic Drum | Electronic CBS |
|---|---|---|---|---|
| MFDD (m/s²) | 6.12 (calculated) | 6.5–6.8 (industry typical) | near regulatory minimum | 7.0–7.5 |
| Unit cost (₹) | 510 | 2,800 | 1,000 | 4,200 |
| Maintenance interval | 10,000 km | 5,000 km (fluid service) | 8,000 km | 15,000 km (sensor calibration) |
| Primary failure mode | Mechanical wear | Fluid leak, seal failure | Lining wear | Sensor / ECU failure |
| System complexity | Low | Medium | Very low | High |

---

## Method summary

| Section | Method | Headline result |
|---|---|---|
| [Braking dynamics](docs/01-braking-dynamics.md) | Quasi-static longitudinal load transfer | ΔW = 393 N; dynamic split 76.7 : 23.3 |
| [Cam profile](docs/02-cam-profile.md) | Variable-ratio cam, continuous polynomial transition | 65:35 → 72:28 front:rear |
| [Contact stress](docs/03-contact-stress.md) | Hertzian line contact, POM on EN31 | p_max = 75.6 MPa, SF = 1.46 |
| [Fatigue life](docs/04-fatigue-life.md) | High-cycle S-N, Archard wear, FEA von Mises | > 10⁶ cycles, 50,000 km calculated life |
| [Materials rationale](docs/05-materials-rationale.md) | Property-driven selection against failure modes | EN31 / POM / aluminium / SS302 |
| [Cost model](docs/06-cost-model.md) | Bottom-up BOM roll-up + batch discount | ₹625 gross → ₹510 net |
| [FMEA](docs/07-fmea.md) | Severity-ranked risk assessment with RPN | Max RPN = 72, no single-point failures |
| [IS 14664 compliance](docs/08-is14664-compliance.md) | Clause-by-clause requirement mapping | All documented clauses met |

---

## Repository structure

```
Bajaj-Torq/
├── README.md
├── LICENSE
├── .gitignore
├── docs/                        # Design analysis, one file per engineering area
│   ├── 00-problem-statement.md
│   ├── 01-braking-dynamics.md
│   ├── 02-cam-profile.md
│   ├── 03-contact-stress.md
│   ├── 04-fatigue-life.md
│   ├── 05-materials-rationale.md
│   ├── 06-cost-model.md
│   ├── 07-fmea.md
│   ├── 08-is14664-compliance.md
│   └── 09-limitations.md        # Scope, assumptions, open items
├── data/                        # Structured inputs and results
│   ├── bom.csv
│   ├── fmea.csv
│   ├── materials.csv
│   ├── benchmark.csv
│   └── results.yaml
└── output/
    └── figures/                 # Generated figures (see figures/README.md)
```

Each `docs/` file follows the same structure: **method → formula → inputs table
(with source) → substituted values → result → margin against limit**. Numbers are
not presented bare.

---

## Open items

Values that could not be reconciled from the source material are marked
`[TODO: confirm value]` in place rather than resolved by assumption. The main
ones are collected in [`docs/09-limitations.md`](docs/09-limitations.md):

- Two different cam fatigue safety factors appear in the source (2.0 and 6.0).
- Two different housing safety factors appear in the source (>2.5 and 5.75).
- Housing is described as both die-cast and as Al 6061-T6, which are
  incompatible (6061-T6 is a wrought heat-treatable alloy, not die-castable).
- The rear brake force share (28%) exceeds the rear dynamic load share (23.3%).
- The revenue model applies a 35% gross margin to revenue computed at unit cost.

---

## Author

**Aditya Deshmukh** — [TODO: add year / degree / institution]

Team **Blue Popcorn**: Aditya Deshmukh (Team Leader), Ankit Kumar, Akshat Singhania.

Winner, In-Campus Hackathon Round, Bajaj Auto TORQ 2026 — a National Level
Campus Challenge.

## License

[MIT](LICENSE)
