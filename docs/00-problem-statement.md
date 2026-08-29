# 0. Problem Statement and Engineering Requirements

## 0.1 The safety gap

Entry-level electric two-wheelers in the Indian market do not reliably meet the
braking performance required by IS 14664:2010.

| Quantity | Value | Source |
|---|---|---|
| Typical observed deceleration, entry-level electric two-wheelers | 4.2 – 4.5 m/s² | Design study observation |
| Minimum required deceleration (IS 14664:2010, Category 3-3 CBS @ 60 km/h) | 5.4 m/s² | IS 14664:2010 |
| Performance shortfall vs regulatory benchmark | 18 – 22% | Derived from the two rows above |
| Observed stopping distance, budget EV @ 60 km/h | 35 – 36 m | Design study observation |
| IS 14664 stopping distance limit @ 60 km/h | 31.6 m | IS 14664:2010 |

## 0.2 Why it matters at scale

- Approximately **1.28 million** electric two-wheelers were sold in India in 2025.
- Entry-level models represent the **fastest-growing segment** of that market.
- A **four-metre** increase in stopping distance at 60 km/h significantly
  increases crash severity.

The gap is therefore concentrated precisely in the highest-volume, most
cost-sensitive part of the market.

## 0.3 Why existing solutions do not close it

| Architecture | Unit cost | Barrier to adoption in this segment |
|---|---|---|
| Hydraulic CBS | ₹2,800 | ~5.5× the target cost ceiling |
| Electronic CBS | ₹4,200 | Requires sensors, ECU, wiring harness |
| ABS | ₹5,500 | Cost prohibitive; high-end vehicles only |
| Basic drum | ₹1,000 | Performs near regulatory minimum only |

Adequate braking architectures exist. None of them are economically viable at
entry-level EV price points, which is the actual constraint this design targets.

## 0.4 Design requirements

**Functional**

1. Peak MFDD ≥ 5.4 m/s² at 60 km/h (IS 14664:2010, Category 3-3).
2. Stopping distance ≤ 31.6 m at 60 km/h, measured per the IS 14664 protocol
   including the brake build-up phase.
3. Hand lever force ≤ 200 N.
4. Secondary (single-circuit) braking ≥ 2.5 m/s² per Clause 4.1.9 — the system
   must retain useful braking after a single cable failure.

**Cost and manufacturing**

5. Target manufacturing cost < ₹600 per unit.
6. Manufacturable on standard 3-axis CNC, with no 5-axis dependency.
7. No electronics, no sensors, no hydraulic fluid.

**Durability**

8. Design life of 50,000 km, established analytically.
9. Maintenance interval no shorter than 10,000 km.

## 0.5 Design approach

A purely mechanical, variable-ratio cam mechanism that redistributes braking
force between the front and rear wheels as a continuous function of lever input
— shifting from a comfort-biased 65:35 split at low braking effort to a
safety-biased 72:28 split at high braking effort, without electronics, sensors
or hydraulic circuits.

The subsequent sections document that design:

| Section | Content |
|---|---|
| [01 — Braking dynamics](01-braking-dynamics.md) | Load transfer and axle load distribution |
| [02 — Cam profile](02-cam-profile.md) | The variable-ratio mechanism |
| [03 — Contact stress](03-contact-stress.md) | Hertzian analysis of the cam–follower interface |
| [04 — Fatigue life](04-fatigue-life.md) | High-cycle fatigue and wear |
| [05 — Materials rationale](05-materials-rationale.md) | Material selection against failure modes |
| [06 — Cost model](06-cost-model.md) | Bottom-up BOM |
| [07 — FMEA](07-fmea.md) | Failure mode and effects analysis |
| [08 — IS 14664 compliance](08-is14664-compliance.md) | Clause-by-clause mapping |
| [09 — Limitations](09-limitations.md) | Scope, assumptions and open items |
