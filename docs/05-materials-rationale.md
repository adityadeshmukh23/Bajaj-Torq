# 5. Materials Rationale

> **How to read this section.** Each material is presented in the same order:
> *what was selected*, *why it was selected*, *which failure mode drove the
> selection*, and *how the design sits against the material's known limit*.
>
> Property values are taken from the source material where stated. Where a
> comparison or a property is not documented in the source, it is marked
> `[TODO: confirm value]` rather than filled in. Qualitative rejection reasoning
> for alternative materials is **design reasoning recorded here, not a formal
> trade study from the source material** — see §5.6.

---

## 5.1 EN31 bearing steel — cam disc {#cam-disc}

**Selected** — EN31 bearing steel, through-hardened to 58–62 HRC, tempered
martensite. One per assembly. ₹220, the most expensive line in the
[bill of materials](06-cost-model.md).

**Design driver** — **rolling/sliding contact fatigue** at the cam–follower
interface. This is the binding constraint: the cam disc carries the highest
severity rating in the [FMEA](07-fmea.md) (10/10 for fatigue cracking), because a
cam fracture is the one failure that could compromise both brake circuits
simultaneously.

**Why this material and condition**

- **Bearing steel, because the duty is a bearing duty.** The cam flank sees
  repeated concentrated Hertzian contact against the follower — the same loading
  mode a rolling-element bearing race sees, and EN31 (100Cr6 / SAE 52100) is the
  standard material for that duty.
- **Through-hardened rather than case-hardened.** Through-hardening gives uniform
  properties across the section, with no case-depth to specify, verify or risk
  grinding through at the cam flank where the profile is finish-ground. A
  case-hardened alternative would add a case-depth inspection requirement to a
  part that already requires 100% NDT.
- **58–62 HRC.** High enough to keep contact stress below the endurance limit
  (see [04 — Fatigue life](04-fatigue-life.md)), and hard enough to act as the
  harder half of the contact pair so that wear is concentrated in the sacrificial
  POM follower rather than the cam.
- **Tempered martensite.** Tempering after hardening relieves quench stress and
  restores toughness, which matters for a part whose dominant failure mode is
  crack initiation.

**Margin against limit**

| Property | Design value | Material limit | Safety factor |
|---|---|---|---|
| Contact fatigue | see [03](03-contact-stress.md) | [TODO: confirm endurance limit] | [TODO: confirm — source states both 2.0 and 6.0] |

**Quality control** — 100% magnetic particle inspection. Specified because the
severity of this failure mode (10/10) does not permit sampling inspection.

---

## 5.2 POM (acetal) — followers {#pom-followers}

**Selected** — POM (polyoxymethylene / acetal), self-lubricating, moulded. Two
per assembly. ₹12 for the pair — the **cheapest components in the assembly**.

**Design driver** — **compressive stress at the Hertzian contact.** Not wear, not
temperature, not creep. The peak contact stress of 75.6 MPa against a 110 MPa
allowable is what sizes this part, and it produces the lowest safety factor
anywhere in the design.

**Why this material**

- **Self-lubricating.** This is the property that makes the whole "no
  electronics, no fluid" architecture viable. A material requiring external
  lubrication would introduce a service item, a contamination path and a failure
  mode that the mechanical-simplicity argument is specifically trying to avoid.
- **Low friction against hardened steel.** The cam must sweep the follower
  through the full ratio transition under load; friction at that interface
  directly degrades the lever-force budget, which has only a 10% margin against
  the 200 N regulatory limit.
- **Dimensionally stable.** The follower position *is* the ratio schedule. A
  material that swelled with humidity would shift the front:rear split in
  service, which is a safety-relevant drift rather than a comfort one.
- **Mouldable.** At ₹6 per follower, the part must be produced by injection
  moulding; the cost target does not survive a machined follower.

**Margin against limit**

| Property | Design value | Material limit | Utilisation | Safety factor |
|---|---|---|---|---|
| Compressive / contact stress | 75.6 MPa | 110 MPa | 69% | **1.46** |

**Honest read on the lowest margin in the design.** SF = 1.46 is the smallest
safety factor in the assembly, and this is deliberate. The follower is the
cheapest part, it is the designated wear item measured at the 20,000 km service
interval, and loading it closest to its limit is what keeps the ₹220 cam disc —
the part with the 10/10 severity rating — operating well inside its own margin.
This is a sacrificial-component strategy, not an unnoticed weak point. The
trade-off it accepts is that follower condition, rather than cam condition,
governs the service schedule.

---

## 5.3 Aluminium — housing {#housing}

**Selected** — Aluminium housing, anodised. ₹65.

> **⚠️ Unresolved — alloy and process conflict.** The source material specifies
> this component two incompatible ways:
>
> | Source location | Specification |
> |---|---|
> | Bill of materials | Housing, **die-cast** aluminium, ₹65 |
> | Structural analysis | **Al 6061-T6**, yield strength 275 MPa |
>
> **6061-T6 is a wrought heat-treatable alloy and cannot be die-cast.** The two
> statements describe different parts. The resolution matters because it changes
> both the cost and the structural margin:
>
> - **If wrought 6061-T6** (machined from bar or extrusion): the 275 MPa yield and
>   the stated factor of safety hold, but ₹65 requires re-costing against a
>   machining rather than casting process route.
> - **If pressure die-cast** (A380 / ADC12 or similar): ₹65 is plausible at
>   volume, but yield strength is materially lower than 275 MPa and the factor of
>   safety must be recalculated.
>
> **[TODO: resolve alloy and process route, then restate cost and FoS.]**

**Design driver** — **von Mises yield under peak braking reaction load.** The
housing reacts the full cam force into the vehicle structure.

**Why aluminium (either route)**

- **Corrosion resistance.** The part is exposed to road spray and monsoon
  conditions for a 50,000 km life with only visual inspection at 10,000 km
  intervals. Aluminium's self-passivating oxide layer provides base protection,
  and anodising — specified in the FMEA as the housing corrosion mitigation —
  thickens it to a controlled, durable depth.
- **Mass.** An unsprung, vehicle-mounted component on a cost- and
  range-sensitive electric two-wheeler, where a steel housing would carry a
  significant mass penalty for no functional gain.
- **Manufacturability at volume.** Both candidate routes support the stated
  18,000 units/year capacity on standard equipment.

**Margin against limit**

| Property | Design value | Material limit | Safety factor |
|---|---|---|---|
| Von Mises stress | Below 50% of yield | 275 MPa (as stated, pending §5.3 resolution) | [TODO: confirm — source states both >2.5 and 5.75] |

---

## 5.4 SS302 stainless — cables {#cables}

**Selected** — SS302 stainless steel cable, front and rear. ₹130 for the pair.

**Design driver** — **tensile fracture with corrosion as the initiating
mechanism.** Cable failure carries the highest RPN in the
[FMEA](07-fmea.md) (72 for the front cable) — not because the severity is the
highest, but because a cable is harder to inspect internally than a cam disc is
to NDT.

**Why stainless, specifically**

- **Corrosion is the failure path, not overload.** A galvanised carbon steel
  cable is cheaper and adequate on day one, but zinc coating is sacrificial and
  finite; strand corrosion under the outer sheath is the classic mechanism by
  which brake cables fail in monsoon service, and it progresses invisibly.
  Stainless removes the mechanism rather than delaying it.
- **Work-hardened strength.** SS302 in spring temper retains high tensile
  strength in drawn wire form, which is what a stranded brake cable requires.

**Margin against limit**

| Property | Design value | Material limit | Safety factor |
|---|---|---|---|
| Tensile load | [TODO: confirm value] | [TODO: confirm value] | [TODO: confirm value] |

**Mitigation in service** — visual inspection and lever travel verification at
every 10,000 km interval. Lever travel is the practical early indicator of cable
stretch or strand loss.

---

## 5.5 Design margin summary

| Component | Material | Governing failure mode | Design | Limit | SF |
|---|---|---|---|---|---|
| Cam disc | EN31, 58–62 HRC | Contact fatigue | — | — | [TODO: 2.0 or 6.0] |
| Followers | POM | Compressive/contact stress | 75.6 MPa | 110 MPa | **1.46** |
| Housing | Al, alloy TBC | Von Mises yield | < 50% yield | 275 MPa | [TODO: 2.5 or 5.75] |
| Cables | SS302 | Tensile fracture | [TODO] | [TODO] | [TODO] |
| Spring | [TODO] | Fatigue | — | — | 2.5 |

**The governing margin in the assembly is the POM follower at SF = 1.46**, by
design. Every other component is intended to sit further from its limit.

---

## 5.6 Note on the alternatives reasoning

The rejection rationale given in §5.1–5.4 for alternative materials (case-hardened
steel, externally lubricated bushings, hygroscopic engineering plastics,
galvanised cable) is **design reasoning documented here for the first time**. The
source material states the selections and their key properties but does not
contain a formal trade study with cited property values for the rejected
candidates.

A complete materials submission would include a weighted decision matrix with
sourced property values for each candidate. That is a known gap and is listed in
[09 — Limitations](09-limitations.md).
