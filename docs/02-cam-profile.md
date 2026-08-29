# 2. Variable-Ratio Cam Profile

> All results in this section are **analytically calculated**. The mechanism
> described here was not built or bench-tested.

## 2.1 Design intent

A fixed brake force split must be chosen as a compromise: a rear-biased split is
comfortable and stable at low braking effort, while a front-biased split is
required at high deceleration, because forward weight transfer unloads the rear
axle (see [01 — Braking dynamics](01-braking-dynamics.md)).

The variable-ratio cam resolves this by making the split a **continuous function
of lever input** rather than a fixed constant:

| Braking regime | Front : rear split | Rationale |
|---|---|---|
| Low braking effort | **65 : 35** | Comfort; stable, progressive feel |
| High braking effort | **72 : 28** | Safety; follows forward weight transfer |

The transition between the two is **continuous and polynomial — no discrete
steps**, so there is no step change in brake force felt at the lever and no
impulsive load applied to the mechanism.

This is achieved with **no electronics, no sensors and no hydraulic fluid**: the
cam geometry itself encodes the force distribution schedule, and a load-sensing
spring sets where on that schedule the system operates.

## 2.2 Force chain

| Station | Force | Source |
|---|---|---|
| Hand lever input | 180 N | Design deck schematic |
| Cam contact force | 612 N | Design deck schematic |
| Front output | [TODO: confirm value] | Design deck schematic is not legible on this label |
| Rear output | [TODO: confirm value] | Design deck schematic is not legible on this label |

**Derived mechanical advantage** (calculated here, not stated in the source):

```
MA = F_cam / F_lever = 612 / 180 = 3.4 : 1
```

> **⚠️ Open item.** The cam contact force is given as 612 N here, while the
> Hertzian contact analysis in [03 — Contact stress](03-contact-stress.md) uses
> **600 N**. The 12 N difference is small (2%) and 600 N is plausibly a rounded
> design case, but the two figures should be reconciled and one of them stated as
> the governing value. **[TODO: confirm governing cam contact force.]**

> **⚠️ Open item.** The lever-to-cam mechanical advantage of 3.4:1 is derived
> from the two stated forces above; it is **not** derived from linkage geometry
> anywhere in the source material. The lever arm lengths and pivot locations that
> produce this ratio are undocumented. **[TODO: document linkage geometry.]**

## 2.3 Ratio transition function

Let `s` be the normalised lever travel, `s ∈ [0, 1]`, and `φ(s)` the front brake
force share.

**Boundary conditions** (from the design intent above):

```
φ(0) = 0.65        (comfort regime)
φ(1) = 0.72        (safety regime)
```

**Continuity requirement** — for the transition to be free of discrete steps as
specified, `φ(s)` must be at least C¹ continuous across the full travel, with:

```
dφ/ds = 0    at s = 0 and s = 1
```

so that the ratio does not change abruptly at either end of the sweep. A C²
continuous form (second derivative also zero at both ends) additionally avoids a
jerk discontinuity in the rate of ratio change.

> **⚠️ Open item.** The source material states that the transition is a "smooth
> polynomial transition — no discrete steps" but **does not state the polynomial
> order or its coefficients**. The boundary conditions above are what the stated
> behaviour requires; the specific curve is not documented.
> **[TODO: confirm polynomial order and coefficients.]**
>
> Standard cam design practice for this requirement would use a quintic
> (3-4-5 polynomial) or higher-order law, but that is a general reference point,
> **not** a value taken from this design.

## 2.4 Cam–follower interface

| Element | Specification | Source |
|---|---|---|
| Cam disc | EN31 bearing steel, through-hardened 58–62 HRC | Design deck |
| Followers | POM (acetal), self-lubricating, 2 off | Design deck |
| Contact length | 15 mm | Design deck |
| Equivalent contact radius | 7.5 mm | Design deck |

The contact stress analysis for this interface — which is the design driver for
the follower material — is documented in
[03 — Contact stress](03-contact-stress.md).
