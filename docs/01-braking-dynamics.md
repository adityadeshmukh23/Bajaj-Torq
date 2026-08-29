# 1. Braking Dynamics and Axle Load Distribution

> All results in this section are **analytically calculated**. No values were
> obtained from instrumented measurement or vehicle testing.

## 1.1 Longitudinal weight transfer

**Method** — Quasi-static longitudinal load transfer, taken as a moment balance
about the front tyre contact patch. The vehicle is treated as a rigid body;
suspension pitch compliance and aerodynamic drag are neglected.

**Formula**

```
ΔW = (m · a · h) / L
```

**Inputs**

| Symbol | Quantity | Value | Unit | Source |
|---|---|---|---|---|
| `m` | Laden mass (vehicle + rider) | 150 | kg | Design deck |
| `a` | Peak design deceleration | 6.12 | m/s² | Design deck |
| `h` | Centre of gravity height | 0.60 | m | Design deck |
| `L` | Wheelbase | 1.40 | m | Design deck |

**Substitution**

```
ΔW = (150 × 6.12 × 0.60) / 1.40
   = 550.8 / 1.40
   = 393.4 N
```

**Result — ΔW = 393 N** transferred from the rear axle to the front axle at peak
deceleration.

## 1.2 Dynamic axle load distribution

**Result (from the design deck)**

| Axle | Share of total load at 6.12 m/s² |
|---|---|
| Front | 76.7% |
| Rear | 23.3% |

**Consistency check** — the source does not state the static axle split, but it
can be recovered from the values above. This check is performed here; it is not
a source value.

```
Total weight       W  = m · g = 150 × 9.81         = 1471.5 N
Front dynamic load    = 0.767 × 1471.5             = 1128.6 N
Static front load     = 1128.6 − 393.4             =  735.2 N
Static front share    = 735.2 / 1471.5             =  50.0%
```

The stated dynamic distribution is therefore internally consistent with a
**50:50 static axle split**, which is a reasonable assumption for a scooter-type
two-wheeler with a centrally seated rider. The 50:50 static split is treated as
an implied assumption throughout this document rather than a stated input.

## 1.3 Brake force distribution vs available adhesion

The cam mechanism delivers a **72:28** front:rear force split at peak braking
(see [02 — Cam profile](02-cam-profile.md)), while the dynamic load split at the
same deceleration is 76.7:23.3.

The tyre–road friction coefficient each axle must sustain to deliver its share
of the braking force without locking follows from:

```
μ_required = (brake force share × a) / (dynamic load share × g)
```

**Front axle**

```
μ_front = (0.72 × 6.12) / (0.767 × 9.81)
        = 4.406 / 7.524
        = 0.59
```

**Rear axle**

```
μ_rear  = (0.28 × 6.12) / (0.233 × 9.81)
        = 1.714 / 2.286
        = 0.75
```

**Result** — the rear axle requires **μ ≥ 0.75** and the front axle **μ ≥ 0.59**.
The rear axle is therefore the limiting axle: under decreasing surface friction,
**the rear wheel reaches lock-up first**.

> **⚠️ Open item.** The source material describes the 72:28 split as giving a
> "≈4.7% margin to avoid rear lock", where 4.7 is the arithmetic difference
> between the 28% rear force share and the 23.3% rear load share. As set out
> above, allocating the rear axle a *larger* share of brake force (28%) than its
> share of dynamic load (23.3%) biases the system *toward* rear lock rather than
> away from it. Either the force split or the characterisation of the margin
> requires review. **[TODO: confirm intended rear brake force share.]**
> On dry asphalt (μ ≈ 0.8–0.9) the stated split remains feasible; on wet or
> loose surfaces it does not, and the fixed mechanical ratio cannot adapt.

## 1.4 Performance summary

| Quantity | Value | Requirement | Status |
|---|---|---|---|
| Peak MFDD @ 60 km/h | 6.12 m/s² | ≥ 5.4 m/s² | Meets requirement |
| Stopping distance @ 60 km/h | 28.7 m | ≤ 31.6 m | Meets requirement |
| Hand lever force | 180 N | ≤ 200 N | Meets requirement |

Stopping distance is quoted per the IS 14664 protocol, which includes the brake
build-up phase.

**Literature comparison** — Lin et al. (2021) report a variable CBS achieving
6.37 m/s² MFDD. The 6.12 m/s² calculated here falls in a comparable range, which
supports the feasibility of the mechanism but does not constitute validation of
this specific design.

## 1.5 Secondary braking (single-cable failure)

| Failure case | Residual MFDD | IS 14664 Cl. 4.1.9 minimum | Margin |
|---|---|---|---|
| Front circuit only (rear cable failed) | 4.4 m/s² | 2.5 m/s² | +76% |
| Rear circuit only (front cable failed) | 2.9 m/s² | 2.5 m/s² | +16% |

Both single-failure cases retain braking above the regulatory secondary-brake
requirement, so the system has **no single point of total brake failure**.
