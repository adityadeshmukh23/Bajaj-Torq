# Design Documentation

Analysis for the variable-ratio cam Combined Braking System. Read in order, or
jump to a section.

| # | Section | Headline result |
|---|---|---|
| 00 | [Problem statement](00-problem-statement.md) | 18–22% shortfall vs IS 14664 in entry-level EVs |
| 01 | [Braking dynamics](01-braking-dynamics.md) | ΔW = 393 N; dynamic split 76.7 : 23.3 |
| 02 | [Cam profile](02-cam-profile.md) | 65:35 → 72:28 continuous transition |
| 03 | [Contact stress](03-contact-stress.md) | p_max = 75.6 MPa, SF = 1.46 |
| 04 | [Fatigue life](04-fatigue-life.md) | > 10⁶ cycles, 50,000 km calculated design life |
| 05 | [Materials rationale](05-materials-rationale.md) | EN31 / POM / aluminium / SS302 |
| 06 | [Cost model](06-cost-model.md) | ₹625 gross → ₹510 net |
| 07 | [FMEA](07-fmea.md) | Max RPN = 72; no single point of total failure |
| 08 | [IS 14664 compliance](08-is14664-compliance.md) | All documented performance clauses met analytically |
| 09 | [Limitations](09-limitations.md) | Scope, assumptions and 13 open items |

## Document format

Every analysis section follows the same structure, so that no number appears
without its derivation:

```
Method  →  Formula  →  Inputs (with source)  →  Substitution  →  Result  →  Margin
```

## Conventions

- **`[TODO: confirm value]`** marks a value that could not be sourced, or one that
  the source material states inconsistently. These are left in place deliberately
  rather than resolved by assumption. All are collected in
  [09 — Limitations](09-limitations.md#94-open-items).
- **Derived here** marks arithmetic performed in this repository on source values,
  as distinct from values transcribed from the source material.
- All results are **analytically calculated**. Nothing in this repository was
  measured, tested, or computed by a live solver. See
  [09 — Limitations](09-limitations.md).
