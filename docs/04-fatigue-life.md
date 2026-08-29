# 4. Fatigue Life and Wear

> **Scope statement.** The 50,000 km design life quoted throughout this document
> is an **analytically calculated** figure derived from high-cycle fatigue and
> wear analysis. **No prototype was built, and no component was subjected to
> physical endurance, rig or road testing.** Any reference to "50,000 km" in this
> repository means calculated design life, not demonstrated service life.

## 4.1 Design life target

| Quantity | Value | Source |
|---|---|---|
| Design life | 50,000 km | Design deck |
| Fatigue regime | High-cycle, > 10⁶ cycles | Design deck |

### Load cycle derivation

The design life is stated in kilometres and the fatigue analysis in cycles, but
the conversion between them is not documented in the source material:

```
N_cycles = distance × (brake applications per km)
         = 50,000 km × [TODO: confirm value]
```

> **⚠️ Open item.** For the stated ">10⁶ cycles" to follow from 50,000 km, the
> analysis must assume approximately **20 brake applications per kilometre**.
> That assumption is not stated anywhere in the source material, and it is the
> link on which the entire fatigue result depends.
> **[TODO: confirm brake applications per km and cite the duty cycle used.]**

## 4.2 EN31 cam disc — contact fatigue

**Method** — High-cycle fatigue assessment against the endurance limit. The
component operates in the regime where contact stress remains below the material
endurance limit, giving nominally infinite life.

**Material condition**

| Property | Value | Source |
|---|---|---|
| Material | EN31 bearing steel | Design deck |
| Heat treatment | Through-hardened | Design deck |
| Hardness | 58–62 HRC | Design deck |
| Microstructure | Tempered martensite | Design deck |

**Stated condition** — contact stress is below the endurance limit, placing the
component in the high-cycle regime above 10⁶ cycles.

| Quantity | Value |
|---|---|
| Applied contact stress | See [03 — Contact stress](03-contact-stress.md) |
| Endurance limit | [TODO: confirm value — not stated in source material] |
| **Safety factor** | **[TODO: confirm value]** |

> **⚠️ Open item — conflicting values.** The source material states the cam
> fatigue safety factor as **6.0** in the performance compliance table and in the
> closing summary, but as **~2.0** in the lifecycle validation section. These
> cannot both be correct. The endurance limit and applied stress that produce the
> governing figure should be stated explicitly so the safety factor is derivable
> rather than asserted. **[TODO: resolve to a single value and show the working.]**

**Quality control** — 100% magnetic particle inspection (NDT) of cam discs is
specified as the mitigation for fatigue cracking in the [FMEA](07-fmea.md).

## 4.3 POM followers — wear

**Method** — Wear life assessment at the Hertzian contact, cross-referenced
against the contact stress result.

| Quantity | Value | Source |
|---|---|---|
| Material | POM (acetal), self-lubricating | Design deck |
| Contact stress verified | 75.6 MPa vs 110 MPa allowable | Design deck |
| Wear life | > 10⁶ cycles | Design deck |
| Wear coefficient `k` | [TODO: confirm value — not stated in source material] |
| Predicted wear depth at design life | [TODO: confirm value] |

The source material presents a wear-depth-versus-cycles relationship but does not
state the wear model, the wear coefficient, or the resulting wear depth. The
standard method for this assessment is the Archard wear relation:

```
V = k · F · s / H
```

where `V` is worn volume, `F` normal load, `s` sliding distance and `H` material
hardness. **[TODO: confirm the wear model and coefficient actually used.]**

**Design intent** — the follower is the intended wear component. Follower wear is
measured at the 20,000 km service interval and the assembly is replaced at
50,000 km (§4.5).

## 4.4 Housing — structural

| Quantity | Value | Source |
|---|---|---|
| Material | [TODO: confirm — see below] | Design deck |
| Yield strength | 275 MPa | Design deck |
| Peak von Mises stress | Below 50% of yield | Design deck |
| Peak stress, absolute | [TODO: confirm value — not stated in source material] |
| **Factor of safety** | **[TODO: confirm value]** |

> **⚠️ Open item — conflicting values.** The source states the housing factor of
> safety as **> 2.5** in the FEA validation section and as **5.75** in the FMEA.
> Stating the absolute peak stress in MPa would make the figure derivable and
> resolve the conflict. **[TODO: resolve to a single value.]**

> **⚠️ Open item — material/process conflict.** The bill of materials specifies a
> **die-cast aluminium** housing at ₹65, while the structural analysis specifies
> **Al 6061-T6** with a 275 MPa yield strength. These are incompatible: 6061-T6 is
> a *wrought* heat-treatable alloy and is not die-castable. Either the housing is
> machined or extruded 6061-T6, in which case the ₹65 cost requires review, or it
> is die-cast in a casting alloy such as A380/ADC12, in which case the yield
> strength — and therefore the factor of safety — is substantially lower than
> 275 MPa. See [05 — Materials rationale](05-materials-rationale.md#housing).
> **[TODO: resolve alloy and process.]**

**Surface treatment** — anodised, specified in the FMEA as the corrosion
mitigation for the housing.

## 4.5 Lifecycle maintenance schedule

| Interval | Action |
|---|---|
| 10,000 km | Visual cable inspection; lever travel verification |
| 20,000 km | Grease replenishment; follower wear measurement |
| 50,000 km | Full system replacement (design life limit) |

The 10,000 km inspection interval compares favourably with the 5,000 km fluid
service interval of a hydraulic CBS, as the mechanical system has no fluid to
degrade or seals to leak.

## 4.6 Summary

| Component | Failure mode | Design life basis | Safety factor |
|---|---|---|---|
| EN31 cam disc | Contact fatigue | Stress below endurance limit, > 10⁶ cycles | [TODO: confirm value] |
| POM followers | Adhesive/abrasive wear | > 10⁶ cycles | 1.46 (on contact stress) |
| Aluminium housing | Von Mises yield | Peak stress < 50% of yield | [TODO: confirm value] |
| SS302 cables | Tensile fracture | Periodic inspection at 10,000 km | [TODO: confirm value] |
