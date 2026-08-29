# 9. Limitations, Assumptions and Open Items

This section states plainly what this design study does and does not establish.
It exists because the distinction is easy to blur and expensive to get wrong.

## 9.1 What this repository is

A **documented design study**. All engineering results were derived analytically
by hand and are reproduced here with their formulas, inputs and substituted
values shown, so that each figure can be checked.

## 9.2 What this repository is not

| Not a… | Because |
|---|---|
| Validated computational model | No solver was written; results are documented, not computed live |
| Simulation | Nothing here is numerically integrated or iterated at runtime |
| Test report | No prototype was built; no component or vehicle was tested |
| Compliance certificate | Analytical compliance is not homologation |

**Specifically:**

- **No physical prototype was built.**
- **No component underwent rig, endurance, or road testing.**
- **No instrumented braking measurement was taken.** The 6.12 m/s² MFDD and
  28.7 m stopping distance are calculated design values.
- **The 50,000 km design life is an analytical fatigue and wear estimate**, not a
  demonstrated service life. Any phrasing suggesting field validation or
  zero-failure field experience would be incorrect.
- **No FEA model, mesh or boundary conditions are included here**, so the stated
  von Mises results cannot be independently reproduced from this repository.

## 9.3 Key assumptions

| Assumption | Value | Basis |
|---|---|---|
| Static axle load split | 50 : 50 | Implied by the stated dynamic split; not stated directly |
| Vehicle treated as rigid body | — | Suspension pitch compliance neglected |
| Aerodynamic drag | Neglected | Reasonable at 60 km/h for this vehicle class |
| Contact analysis | Static, frictionless | Tangential traction at the cam–follower interface neglected |
| Brake applications per km | [TODO: confirm value] | Required to convert 50,000 km into the stated >10⁶ cycles |
| Tyre–road friction | Dry asphalt | The rear-lock analysis assumes high available μ |

## 9.4 Open items

Values that appear inconsistently in the source material, carried here as
unresolved rather than silently reconciled:

| # | Item | Conflict | Location |
|---|---|---|---|
| 1 | Cam fatigue safety factor | Stated as both **2.0** and **6.0** | [04](04-fatigue-life.md) |
| 2 | Housing safety factor | Stated as both **> 2.5** and **5.75** | [04](04-fatigue-life.md) |
| 3 | Housing alloy and process | **Die-cast** vs **Al 6061-T6** — incompatible | [05](05-materials-rationale.md#housing) |
| 4 | Rear brake force share | 28% force share vs 23.3% dynamic load share biases *toward* rear lock, not away | [01](01-braking-dynamics.md) |
| 5 | Cam contact force | **612 N** in the schematic vs **600 N** in the contact analysis | [02](02-cam-profile.md) |
| 6 | MFDD margin | "+20%" claimed; 6.12/5.4 gives **+13.3%** | [08](08-is14664-compliance.md) |
| 7 | Stopping distance margin | "+14%" and "20% vs IS 14664" claimed; neither reconciles with 31.6 m | [08](08-is14664-compliance.md) |
| 8 | Revenue model | Revenue computed at unit **cost**, then a 35% margin applied on top | [06](06-cost-model.md) |
| 9 | Tooling amortisation | Unclear whether ₹28/unit sits inside or outside the ₹510 | [06](06-cost-model.md) |
| 10 | FMEA occurrence & detection | Not recorded; RPN values are asserted, not derivable | [07](07-fmea.md) |
| 11 | Polynomial transition | Order and coefficients not stated | [02](02-cam-profile.md) |
| 12 | Linkage geometry | 3.4:1 mechanical advantage not derived from lever geometry | [02](02-cam-profile.md) |
| 13 | Materials trade study | No weighted decision matrix with cited property values for rejected candidates | [05](05-materials-rationale.md#note-on-the-alternatives-reasoning) |

## 9.5 What would be required to close the gaps

**To validate the performance claims**

1. Build a single prototype assembly.
2. Instrument a representative vehicle and run the IS 14664 protocol at a
   certified facility, measuring MFDD, stopping distance and lever force.
3. Compare measured against calculated values and report the delta.

**To validate the durability claims**

4. Rig-test the cam–follower interface to the assumed cycle count, with a stated
   duty cycle, and measure follower wear depth against the analytical prediction.

**To close the design questions**

5. Sweep the rear-lock analysis across μ = 0.4–0.9 to establish the wet-surface
   lock threshold that the fixed mechanical ratio cannot adapt to (item 4).
6. Complete the housing alloy/process trade study and restate cost and factor of
   safety from the resolved choice (item 3).
7. Document the linkage geometry that produces the 3.4:1 mechanical advantage
   (item 12).
8. Record the FMEA occurrence and detection ratings with their scale definitions
   (item 10).

## 9.6 Terminology used in this repository

To avoid overstating what was done, the following phrasing is used consistently:

| Used | Not used |
|---|---|
| Analytically calculated | Tested, measured, field validated |
| Documented design value | Validated result |
| Design study / design toolkit | Solver, simulation, computational model |
| Analytical fatigue life estimate | Proven service life, zero-failure validation |
| Meets requirement (analytically) | Certified, homologated, compliant |
