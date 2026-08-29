# 6. Cost Model

> All figures are **analytically calculated design values** from a bottom-up bill
> of materials. No supplier quotations were obtained and no parts were procured.

## 6.1 Bill of materials

Line items as sourced: [`data/bom.csv`](../data/bom.csv)

| Item | Category | Unit cost (₹) |
|---|---|---|
| EN31 hardened cam disc | Component | 220 |
| Housing (aluminium) | Component | 65 |
| Cables (front + rear) | Component | 130 |
| Lever arm | Component | 85 |
| POM followers (2×) | Component | 12 |
| Spring + hardware | Component | 48 |
| Assembly labour | Process | 35 |
| Testing + packaging | Process | 30 |
| **Total (pre-negotiation)** | | **625** |

**Verification** (arithmetic performed here on the source line items):

```
220 + 65 + 130 + 85 + 12 + 48 + 35 + 30 = 625   ✓
```

## 6.2 Batch discount

**Formula**

```
C_net = C_gross × (1 − d)
```

**Result**

| Quantity | Value |
|---|---|
| Gross BOM cost | ₹625 |
| **Net cost after batch discounts** | **₹510** |
| Implied discount `d` | 18.4% |

```
d = (625 − 510) / 625 = 0.184 = 18.4%
```

The implied discount rate is derived here; the source states the ₹625 and ₹510
endpoints but not the discount rate.

**Against target** — the design requirement was a manufacturing cost below ₹600
per unit. At ₹510, the target is met with a ₹90 margin.

## 6.3 Tooling amortisation

**Formula**

```
C_tooling_per_unit = T_total / V_amortisation
```

**Inputs and result**

| Symbol | Quantity | Value |
|---|---|---|
| `T_total` | Total tooling cost | ₹2,80,000 (₹2.8 lakh) |
| `V_amortisation` | Amortisation volume | 10,000 units |
| `C_tooling_per_unit` | **Tooling cost per unit** | **₹28** |

```
280,000 / 10,000 = ₹28 per unit
```

> **⚠️ Open item.** The source material does not state whether the ₹28/unit
> tooling amortisation is included within the ₹510 net cost or sits on top of it.
> The distinction matters: ₹510 versus ₹538 changes the cost-per-performance
> figure in §6.4. **[TODO: confirm whether tooling is inside or outside the ₹510.]**

## 6.4 Cost-performance benchmark

Source data: [`data/benchmark.csv`](../data/benchmark.csv)

**Metric** — rupees per unit of braking performance:

```
Cost efficiency = unit cost / MFDD
```

| Architecture | Unit cost (₹) | MFDD (m/s²) | ₹ per m/s² | Market position |
|---|---|---|---|---|
| **This CBS** | **510** | **6.12** | **83** | Budget EVs |
| Hydraulic CBS | 2,800 | 6.5 | 431 | Premium only |
| Basic drum | 1,000 | 4.2 | 238 | Below regulation |
| ABS | 5,500 | 7.2 | 764 | High-end only |

**Headline comparison against hydraulic CBS**

```
Performance retained = 6.12 / 6.5   = 94%
Cost fraction        = 510 / 2,800  = 18%
Cost reduction       = (2800 − 510) / 2800 = 82%
```

Approximately **94% of hydraulic CBS braking performance at 18% of the cost**.

> **⚠️ Minor inconsistency in source.** The cost advantage is variously stated as
> "82% cheaper", "~1/5th the cost" (= 20%) and "~1/4th the cost" (= 25%) across
> different slides. The 18% / 82% pair is the one consistent with the stated ₹510
> and ₹2,800 figures. **[TODO: standardise on one phrasing.]**

## 6.5 Manufacturing readiness

| Parameter | Value |
|---|---|
| Part count | 12 |
| Assembly yield | 98% |
| Assembly time | 50 minutes |
| Machining requirement | Standard 3-axis CNC — no 5-axis dependency |
| Fixturing | Simple re-clamping fixtures |
| Production capacity | 18,000 units/year on 2 CNC machines |

**Process route** — CNC mill → heat treatment (through-hardening) → precision
grinding → housing machining → POM follower moulding → assembly → functional
testing → packaging.

The absence of a 5-axis requirement is a deliberate cost decision: it keeps the
part manufacturable by tier-2 suppliers on commonly available equipment rather
than restricting sourcing to specialist machine shops.

## 6.6 Market model

| Parameter | Value |
|---|---|
| Addressable budget EV market, 2026 | 600,000 units |
| Target capture | 2.5% |
| Target volume | 15,000 units/year |
| Projected revenue | ₹76.5 lakh |
| Gross margin | 35% (₹26.8 lakh) |
| ROI | ~108% by Year 2 |

> **⚠️ Open item — the revenue model does not close.** The projected revenue
> reconciles as:
>
> ```
> 15,000 units × ₹510 = ₹76,50,000 = ₹76.5 lakh   ✓ arithmetic checks
> ```
>
> but ₹510 is the **unit manufacturing cost**, not a selling price. Revenue
> computed at cost implies a selling price equal to cost, which is inconsistent
> with the 35% gross margin claimed on top of it. Both cannot hold.
>
> To carry a 35% gross margin on a ₹510 cost, the selling price would need to be
> approximately ₹785, giving revenue nearer ₹1.18 crore at the same volume.
> **[TODO: state the selling price explicitly and recompute revenue, margin and
> ROI from it.]**
>
> The volume assumptions (600,000 addressable, 2.5% capture, 15,000 units) are
> unaffected by this and stand on their own.
