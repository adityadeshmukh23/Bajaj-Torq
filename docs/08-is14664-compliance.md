# 8. IS 14664:2010 Compliance Mapping

> **Compliance status here is analytical.** Every figure in the "This design"
> column is a calculated design value. **No homologation testing, type approval
> testing, or instrumented vehicle testing was carried out.** This section
> demonstrates that the design is *dimensioned to meet* the standard; it does not
> demonstrate that a built system *does* meet it.

**Standard** — IS 14664:2010, Category 3-3 (Combined Braking System), 60 km/h.

## 8.1 Compliance summary

| Clause / requirement | Requirement | This design | Margin | Status |
|---|---|---|---|---|
| Minimum MFDD @ 60 km/h | ≥ 5.4 m/s² | 6.12 m/s² | +13.3% | Meets requirement |
| Maximum stopping distance @ 60 km/h | ≤ 31.6 m | 28.7 m | 9.2% shorter | Meets requirement |
| Maximum hand lever force | ≤ 200 N | 180 N | 10% | Meets requirement |
| Cl. 4.1.9 — secondary brake, front only | ≥ 2.5 m/s² | 4.4 m/s² | +76% | Meets requirement |
| Cl. 4.1.9 — secondary brake, rear only | ≥ 2.5 m/s² | 2.9 m/s² | +16% | Meets requirement |

Stopping distance is quoted **per the IS 14664 protocol**, which includes the
brake build-up phase — not as an idealised `v²/2a` figure.

## 8.2 Margin derivations

All margins are computed here from the two source values in each row.

**MFDD**

```
6.12 / 5.4 = 1.133   →   +13.3% above the minimum
```

**Stopping distance**

```
(31.6 − 28.7) / 31.6 = 0.092   →   9.2% shorter than the limit
```

**Hand lever force**

```
(200 − 180) / 200 = 0.10   →   10% margin
```

The 200 N limit is not stated directly in the source material; it is implied by
the stated "180 N, 10% margin" pairing. **[TODO: confirm the lever force limit
against the standard text.]**

**Secondary braking**

```
Front only:  4.4 / 2.5 = 1.76   →   +76%
Rear only:   2.9 / 2.5 = 1.16   →   +16%
```

## 8.3 Discrepancies against the source material

> **⚠️ These three claims in the source material do not reconcile with its own
> stated baselines and are not reproduced elsewhere in this repository.**

**1. "+20% above IS 14664 minimum" (MFDD)**

The source states the design exceeds the minimum by 20%. Against the stated
5.4 m/s² baseline, the actual figure is +13.3%. A +20% margin would require a
baseline of 5.10 m/s², which is not the value the source gives.
**[TODO: confirm the regulatory baseline; use +13.3% against 5.4 m/s².]**

**2. "+14%" (stopping distance)**

Against the stated 31.6 m limit, 28.7 m is 9.2% shorter, or a ratio of 10.1%.
Neither produces 14%. **[TODO: confirm; use 9.2% against the 31.6 m limit.]**

**3. "20% shorter stopping distance (vs IS 14664)"**

This headline figure does not hold against the IS limit, but it does reconcile
against the *observed budget-EV baseline* stated elsewhere in the same source:

```
(35.5 − 28.7) / 35.5 = 19.2%   ≈ 20%
```

The figure appears to be correct but attributed to the wrong baseline. The claim
should read **"~20% shorter than observed budget-EV stopping distances (35–36 m)"**,
not "vs IS 14664". **[TODO: correct the attribution.]**

## 8.4 Compliance items not addressed

The analysis covers the performance clauses above. A full IS 14664 submission
would additionally require evidence against clauses not treated in this design
study:

- Brake fade / heat cycling performance
- Wet braking performance
- Endurance and durability test sequences
- Cable and component environmental conditioning

These are recorded as gaps in [09 — Limitations](09-limitations.md) rather than
claimed as satisfied.

## 8.5 Standing caveat

Analytical compliance is a design gate, not a certification. Converting the
figures in §8.1 into demonstrated compliance requires an instrumented vehicle,
the IS 14664 test protocol, and a certified test facility. That work has not been
performed.
