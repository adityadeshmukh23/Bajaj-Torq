# Data Sources and Provenance

## Source documents

| Document | Description |
|---|---|
| CBS design deck (TORQ 2026) | Primary source for all design values, BOM, FMEA and benchmark data |
| Technical analysis report — Team Blue Popcorn | Supporting engineering analysis |

Source documents are not redistributed in this repository (see `.gitignore`).

## Provenance of every value

All values in `data/` fall into exactly one of three categories:

| Category | Meaning | How it is marked |
|---|---|---|
| **Sourced** | Transcribed directly from the design deck or technical report | `source` column names the document |
| **Derived** | Arithmetic performed in this repository on sourced values | Labelled "derived" in the relevant `docs/` section |
| **Unsourced** | Not stated in the source material, or stated inconsistently | `[TODO: confirm value]` |

**No value in this repository was invented, estimated, or filled in by
assumption.** Where a number was needed and not available, the placeholder was
left in place instead.

## Method

All engineering results were **derived analytically by hand**. No solver was
written, no simulation was run, and no physical testing was performed. See
[`../docs/09-limitations.md`](../docs/09-limitations.md) for the full scope
statement.

## File index

| File | Contents | Notes |
|---|---|---|
| `bom.csv` | Bill of materials, 8 line items | Sums to ₹625 gross |
| `fmea.csv` | Failure mode register, 5 entries | O and D ratings unsourced |
| `benchmark.csv` | Competing brake architectures | Two unsourced cells marked |
| `materials.csv` | Material properties used in the analysis | SS302 properties unsourced |
| `results.yaml` | Consolidated results with formulas and substitutions | Provenance block at top |

## Reference values

Two standard reference values appear in
[`../docs/03-contact-stress.md`](../docs/03-contact-stress.md) as part of a
consistency check on the stated equivalent modulus `E′ = 3.37 GPa`:

- POM: E ≈ 3.0 GPa, ν ≈ 0.35
- EN31: E ≈ 210 GPa, ν ≈ 0.30

These are **general reference values for the material pair, not values from the
source material**, and are labelled as such at the point of use. They are used
only to verify a stated result, never to produce a new one.

## Literature

- Lin et al., 2021 — variable CBS reported 6.37 m/s² MFDD. Cited in the source
  material as a feasibility benchmark, not as validation of this design.
