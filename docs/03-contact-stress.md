# 3. Hertzian Contact Stress — POM Follower on EN31 Cam

> All results in this section are **analytically calculated**. No contact stress
> was measured experimentally.

This is the **binding constraint on the follower design** and the most
load-critical interface in the mechanism.

## 3.1 Method

Hertzian **line contact** between two non-conforming elastic bodies with parallel
axes (cylindrical follower against the cam flank).

**Assumptions**

- Purely elastic deformation; no plastic yielding at the contact.
- Frictionless normal loading; tangential traction neglected.
- Contact dimensions small relative to body radii.
- Static load case at peak cam force.

## 3.2 Governing equations

```
1/E′   = (1 − ν₁²)/E₁ + (1 − ν₂²)/E₂

p_max  = √( F · E′ / (π · L · R*) )
```

where `E′` is the equivalent (reduced) elastic modulus of the contact pair and
`R*` the equivalent contact radius.

## 3.3 Inputs

| Symbol | Quantity | Value | Unit | Source |
|---|---|---|---|---|
| `F` | Applied contact force | 600 | N | Design deck |
| `E′` | Equivalent elastic modulus, POM on EN31 | 3.37 | GPa | Design deck |
| `R*` | Equivalent contact radius | 7.5 | mm | Design deck |
| `L` | Contact length | 15 | mm | Design deck |

## 3.4 Substitution

```
p_max = √( 600 × 3.37×10⁹ / (π × 0.015 × 0.0075) )
      = √( 2.022×10¹² / 3.534×10⁻⁴ )
      = √( 5.721×10¹⁵ )
      = 7.56×10⁷ Pa
```

## 3.5 Result

**p_max = 75.6 MPa**

### Cross-check via contact half-width

Performed here as an independent consistency check on the result above; the
intermediate half-width is not a source value.

```
b     = √( 4 · F · R* / (π · L · E′) )
      = √( 4 × 600 × 0.0075 / (π × 0.015 × 3.37×10⁹) )
      = √( 18 / 1.588×10⁸ )
      = 3.37×10⁻⁴ m  =  0.337 mm

p_max = 2F / (π · b · L)
      = 1200 / (π × 3.37×10⁻⁴ × 0.015)
      = 7.56×10⁷ Pa  =  75.6 MPa      ✓ agrees
```

### Consistency check on E′

The source states `E′ = 3.37 GPa` but does not state the constituent moduli. Using
standard reference values for the material pair — **not** values taken from the
source material — the stated `E′` is recovered:

```
E_POM ≈ 3.0 GPa,  ν_POM ≈ 0.35        (reference value)
E_EN31 ≈ 210 GPa, ν_EN31 ≈ 0.30       (reference value)

1/E′ = (1 − 0.35²)/3.0 + (1 − 0.30²)/210
     = 0.8775/3.0 + 0.91/210
     = 0.29250 + 0.00433
     = 0.29683 GPa⁻¹

E′   = 3.37 GPa                        ✓ matches stated value
```

## 3.6 Margin against material limit

| Quantity | Value | Unit |
|---|---|---|
| Peak contact stress | 75.6 | MPa |
| POM allowable compressive stress | 110 | MPa |
| Utilisation | 69% | — |
| **Safety factor** | **1.46** | — |

```
SF = 110 / 75.6 = 1.46
```

## 3.7 Interpretation

**SF = 1.46 is the lowest safety margin in the assembly.** This is a deliberate
consequence of the design hierarchy rather than an oversight:

- The POM follower is the **cheapest component** in the bill of materials
  (₹12 for the pair — see [06 — Cost model](06-cost-model.md)).
- It is the **intended wear item**, replaced at the scheduled service interval.
- Making the follower the softer, lower-margin element **protects the EN31 cam
  disc**, which is the most expensive component (₹220) and the one whose fatigue
  failure carries the highest severity rating in the
  [FMEA](07-fmea.md) (10/10).

This is a sacrificial-component strategy: the low-cost part is loaded closest to
its limit so that the high-cost, high-severity part is not. The trade-off is
discussed further in
[05 — Materials rationale](05-materials-rationale.md#pom-followers).
