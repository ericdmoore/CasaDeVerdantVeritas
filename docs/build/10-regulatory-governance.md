# Regulatory Governance — *who and what governs building on school land*

*A greenhouse on a Dallas ISD campus sits in a different regulatory lane than either a backyard hobby structure or a normal commercial build. This document maps the authorities, the codes, and the approvals that govern it — and isolates the one classification decision that swings the whole project's cost and complexity.*

> ⚠️ **Not legal advice.** This is a synthesis of Texas statutes and rules to orient the project. The binding authorities are **Dallas ISD's facilities/construction department** and a **Texas-licensed architect** — confirm everything here with them before relying on it. Code editions and local amendments change; treat every citation as "verify current version with the AHJ."
>
> **AHJ** = Authority Having Jurisdiction. **ISD** = Independent School District. **TEA** = Texas Education Agency. **TDLR** = Texas Department of Licensing and Regulation. **RAS** = Registered Accessibility Specialist. **AHJ/DISD** is who you actually call.

---

## The headline

**School land removes the city's *zoning* leverage but not the *building codes*.** A Texas ISD is a political subdivision of the state with governmental immunity, and the courts split it cleanly:

- **Location / zoning → district is largely exempt.** A city generally cannot use zoning to dictate where a school district places a building.
- **Construction safety → codes still apply.** The legislature did not preempt the city's police power over *how* a building is built.

So you may skip the city's zoning counter, but the technical codes still bind — administered through the state's school-facilities framework rather than (or alongside) the city.

## The layers of governance

| # | Authority | Instrument | What it governs |
|---|-----------|-----------|-----------------|
| 1 | **TEA** | **19 TAC §61.1040** — School Facilities Standards | The master rule for school construction; pulls in the technical codes below and sets the compliance/inspection model. |
| 2 | **ICC / NFPA codes** (as adopted) | IBC + I-codes, NEC, NFPA 101 Life Safety, NFPA 1 Fire | The physical construction, fire, electrical, egress requirements. |
| 3 | **TDLR** | 2012 Texas Accessibility Standards (TAS) + 2010 ADA | Accessibility; mandatory RAS review at ≥ $50k. |
| 4 | **TBAE / TBPELS** | Occupations Code Ch. 1051 / 1001 | Whether a sealed architect/engineer design is required. |
| 5 | **Dallas ISD** | Board policy, facilities standards, procurement, risk mgmt | Acceptance, design standards, insurance, bidding — even for donated work. |
| 6 | **State Fire Marshal / local fire** | NFPA / fire code | Fire safety inspection. |
| 7 | **TCEQ / local** | Stormwater, environmental | Site disturbance, drainage, any potable interface. |

### 1. TEA — 19 TAC §61.1040 (the master rule)
- Requires compliance with the **IBC** and I-code family (mechanical, plumbing, energy), **NEC**, **NFPA 101 + NFPA 1**, and **2010 ADA + 2012 TAS**. "Reasonably comply" with locally adopted codes, or the state model codes where the locality hasn't adopted.
- Requires a **licensed architect for new construction** as "prime design professional."
- **Where the local AHJ doesn't enforce codes on schools, the district must hire a third-party code-compliance officer** (an ICC Certified Building Official) who performs inspections and issues a third-party certificate of occupancy. *The oversight doesn't disappear — it shifts to a qualified third party.*

### 2. The technical codes
Standard IBC/NFPA/NEC stack. The greenhouse-specific provisions live in **IBC §312.1.1 / §3112**. Which edition + local amendments apply is a DISD/AHJ question.

### 3. Accessibility — TDLR + RAS
- **Projects ≥ $50,000:** must be registered with TDLR and reviewed *and* inspected by a **Registered Accessibility Specialist** against TAS. Schools are explicitly covered.
- **Under $50k:** registration not required, but TAS compliance may still apply.
- Sits on top of federal **ADA + Section 504**. Ties to [REQ-ACC-1](../design/10-requirements.md#h-accessibility--inclusion).

### 4. The architect/engineer seal — the agricultural exemption won't save us
- Occupations Code Ch. 1051 exempts **agricultural buildings** and certain small structures (e.g., one-story ≤ 5,000 sq ft, limited spans) from needing a sealed architectural design. **That helps a farmer, not a public school.**
- Because §61.1040 independently requires an architect for new school construction, a **public building on district land needs a sealed design regardless** of the agricultural carve-out.
- **➡️ This resolves our earlier open question:** plan on a **sealed architect (and likely engineer) design**. See [REQ-STR-1](../design/10-requirements.md#a-structure--envelope) and the [slab checklist anchor sign-off](00-slab-prepour-checklist.md#5-structural-anchors--embeds-req-slab-5-req-str-14).

### 5. Dallas ISD process & procurement
Even a **donated or volunteer-built** structure typically must clear:
- **Board acceptance** of the gift / improvement to real property.
- **District facilities design standards** and review.
- **Risk management / insurance** sign-off.
- **Competitive procurement** (Texas Education Code Ch. 44) if district funds touch it or it becomes a district asset.

The finished structure is a public building on public land — it inherits the public-building requirements no matter who builds it.

### 6–7. Fire & environmental overlays
State Fire Marshal / local fire inspection; TCEQ stormwater (a SWPPP if site disturbance is large enough); and our **off-grid rainwater** plan raising plumbing-code and **cross-connection/backflow** questions at any potable interface (ties to [REQ-WATER-4](../design/10-requirements.md#e-irrigation--water)).

---

## ⭐ The decision that governs everything: occupancy classification

This is the fork that decides how regulated — and how expensive — the project is.

| Path | Classification | Consequence |
|------|----------------|-------------|
| **Accessory horticultural structure** | **IBC Group U** (utility/miscellaneous — barns, sheds, greenhouses) | Light-touch. Greenhouse provisions of §312.1.1/§3112. The cheap, simple path. |
| **Occupied instructional space** | **Group E (educational)** or **B** | Far heavier — egress, fire separation, possibly sprinklers, full occupied-building requirements. |

The tension is built into our own program: [REQ-EDU](../design/10-requirements.md#i-education--layout) wants "capacity for a class of 20–25 inside," but teaching a class *inside* is exactly what can push an AHJ to call it occupied instructional space rather than an accessory greenhouse.

**Possible resolutions to explore with DISD + architect:**
- Keep the greenhouse a **Group U horticultural structure** and conduct instruction *at/around* it (covered work area, adjacent pad) rather than seating a class inside — preserving the light path.
- Accept **Group E/B** and design to it from the start (budget and timeline change materially).
- A hybrid the AHJ will bless in writing.

**Do this early.** It's cheap to decide now and ruinously expensive to discover after design.

---

## Governance requirements (citable)

| ID | Pri | Requirement |
|----|-----|-------------|
| REQ-REG-1 | MUST | Confirm **occupancy classification** (Group U vs. E/B) with DISD + AHJ in writing before design is finalized. |
| REQ-REG-2 | MUST | Engage a **Texas-licensed architect** as prime design professional; produce a **sealed design** (per 19 TAC §61.1040). |
| REQ-REG-3 | MUST | Design to the codes adopted via §61.1040 (IBC/I-codes, NEC, NFPA 101/1) at the **edition/local amendments** the AHJ confirms. |
| REQ-REG-4 | MUST | If project cost ≥ $50k, **register with TDLR** and obtain **RAS** plan review + inspection for TAS. |
| REQ-REG-5 | MUST | Clear the **DISD process**: board acceptance, facilities review, risk/insurance, and procurement (TEC Ch. 44) as applicable — even if donated/volunteer-built. |
| REQ-REG-6 | SHOULD | Identify which code provisions the **local AHJ enforces** vs. require a **third-party ICC code-compliance officer** + third-party C of O. |
| REQ-REG-7 | SHOULD | Address fire (State Fire Marshal/local), stormwater (TCEQ/SWPPP), and **backflow/cross-connection** for the rainwater system. |

---

## Open questions

> **OPEN QUESTION:** ⭐ Occupancy classification — Group U accessory greenhouse, or occupied instructional space (E/B)? The highest-leverage decision in the project. (REQ-REG-1)
> **OPEN QUESTION:** Does DISD's AHJ enforce codes on this project directly, or must we procure a third-party ICC building official? (REQ-REG-6)
> **OPEN QUESTION:** Which code editions + Dallas local amendments apply? (REQ-REG-3)
> **OPEN QUESTION:** Project cost — does it cross the $50k TDLR/RAS threshold? (Almost certainly yes for a slab + custom build.) (REQ-REG-4)
> **OPEN QUESTION:** DISD's specific process and design standards for accepting a donated/grant-funded structure on a campus. (REQ-REG-5)

---

## Sources

- [TEA — Facilities Funding and Standards](https://tea.texas.gov/finance-and-grants/state-funding/facilities-funding-and-standards) · [19 TAC §61.1040 (Cornell LII)](https://www.law.cornell.edu/regulations/texas/19-Tex-Admin-Code-SS-61-1040)
- [TDLR — Texas Accessibility Standards](https://www.tdlr.texas.gov/ab/abtas.htm) · [$50k TAS review threshold](https://www.accessplanreview.com/tas-inspection/)
- [Occupations Code Ch. 1051 exemptions (Justia)](https://law.justia.com/codes/texas/occupations-code/title-6/subtitle-b/chapter-1051/subchapter-l/) · [TBAE "When an architect is required" flowchart](https://www.tbae.texas.gov/wp-content/uploads/2023/04/ArchRequiredFlowChartApril2023.pdf)
- [IBC §312.1.1 Greenhouses](https://codes.iccsafe.org/s/IBC2018/chapter-3-occupancy-classification-and-use/IBC2018-Ch03-Sec312.1.1) · [IBC Group U / Appendix C agricultural buildings](https://codes.iccsafe.org/content/IBC2018/appendix-c-group-u-agricultural-buildings)
- [School zoning vs. building-code distinction (Lawyers.com school-law)](https://blogs.lawyers.com/attorney/school-law/in-the-zone-does-city-zoning-control-where-schools-build-buildings-32899/)

*Upstream: [`docs/design/10-requirements.md`](../design/10-requirements.md). Related: [`00-slab-prepour-checklist.md`](00-slab-prepour-checklist.md).*
