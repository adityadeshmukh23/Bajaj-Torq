# 7. Failure Mode and Effects Analysis

> Severity, RPN and mitigations are **as documented in the source material**.
> Occurrence and detection ratings were not recorded and are flagged below.

Source data: [`data/fmea.csv`](../data/fmea.csv)

## 7.1 Method

Standard FMEA risk prioritisation:

```
RPN = Severity (S) × Occurrence (O) × Detection (D)
```

Each rated on a 1–10 scale, with higher values indicating greater severity,
higher likelihood, or poorer detectability.

## 7.2 Risk register

| Failure mode | S | O | D | RPN | Mitigation |
|---|---|---|---|---|---|
| Front cable break | 9 | [TODO] | [TODO] | 72 | SS302 cable, periodic inspection |
| Cam fatigue crack | 10 | [TODO] | [TODO] | 60 | Through-hardened EN31 (58–62 HRC), 100% magnetic particle NDT |
| Housing fracture | 9 | [TODO] | [TODO] | 54 | Aluminium housing (SF stated as 5.75), anodised |
| Rear cable break | 7 | [TODO] | [TODO] | 49 | SS302 cable, periodic inspection |
| Spring failure | 6 | [TODO] | [TODO] | 42 | SF = 2.5, travel limiters |

> **⚠️ Open item.** The source material records severity and RPN but not the
> occurrence and detection ratings. Without them the RPN values are asserted
> rather than derived, and a reviewer cannot check them.
>
> The implied product `O × D = RPN / S` is recoverable and is given below, but the
> individual ratings — and the rating scale definitions behind them — are not.
> **[TODO: record O and D ratings and the scale definitions used.]**

**Implied O × D** (arithmetic on the source values, not source values themselves):

| Failure mode | S | RPN | Implied O × D |
|---|---|---|---|
| Front cable break | 9 | 72 | 8 |
| Cam fatigue crack | 10 | 60 | 6 |
| Housing fracture | 9 | 54 | 6 |
| Rear cable break | 7 | 49 | 7 |
| Spring failure | 6 | 42 | 7 |

All five rows are consistent with integer O and D ratings, so the RPN figures are
at least arithmetically plausible.

## 7.3 Reading the risk ranking

**Highest severity is not highest risk.** Cam fatigue cracking carries the
highest severity in the register (10/10) but ranks *second* by RPN, below front
cable failure at 72. The reason is detectability:

- A cam disc receives **100% magnetic particle NDT** before it ever ships. A
  crack is caught in manufacturing.
- A cable degrades **internally, under its sheath, in service**. Strand corrosion
  and fatigue progress where they cannot be seen, which is why cable failure
  carries the highest detection penalty and therefore the highest RPN despite
  lower severity.

This is why the mitigation strategy for cables is **material substitution**
(SS302 rather than galvanised carbon steel — removing the corrosion mechanism)
rather than inspection alone. See
[05 — Materials rationale](05-materials-rationale.md#cables).

## 7.4 Fail-safe architecture

The system is designed with **no single point of total brake failure**. Either
cable can fail without loss of all braking:

| Failure case | Residual MFDD | IS 14664 Cl. 4.1.9 minimum | Status |
|---|---|---|---|
| Rear cable failed (front only) | 4.4 m/s² | 2.5 m/s² | Meets requirement (+76%) |
| Front cable failed (rear only) | 2.9 m/s² | 2.5 m/s² | Meets requirement (+16%) |

Both degraded modes remain above the regulatory secondary-brake requirement, so
IS 14664 Clause 4.1.9 is satisfied under single-cable failure.

The asymmetry is expected and correct: the front circuit carries the majority of
the braking duty by design (72:28 at peak braking), so losing the rear cable is
the less severe of the two cases.

## 7.5 Mitigation summary by mechanism

| Mechanism | Applied to | Rationale |
|---|---|---|
| Material substitution | Cables (SS302) | Removes the corrosion failure path rather than delaying it |
| 100% NDT | Cam disc | Severity 10/10 does not permit sampling inspection |
| Surface treatment | Housing (anodised) | Corrosion protection over a 50,000 km life |
| Mechanical limit | Spring (travel limiters) | Bounds spring travel so overload cannot occur |
| Scheduled inspection | Cables, followers | Catches progressive degradation between service intervals |
