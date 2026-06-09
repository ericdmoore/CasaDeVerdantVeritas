# Slab Pre-Pour Checklist — *the one-way door*

*Once concrete is poured, every decision below becomes demolition rather than an edit. This is the single highest-stakes artifact in the build. Nothing gets poured until every **MUST** line here is signed off. It implements the `REQ-SLAB-*` requirements and the conduit/plumbing needs of the off-grid and water systems.*

> **Status:** ⚪ Not started — blocked on a chosen site ([`20-site-and-orientation.md`](../design/20-site-and-orientation.md)) and a finalized floor plan.
> **Rule:** No pour without the [sign-off block](#sign-off-before-the-pour) complete.

---

## Before anything: two upstream blockers

The slab cannot be designed — let alone poured — until:

1. **Site is chosen** and a **geotechnical/soils assessment** is done. Dallas sits on **expansive clay** (shrink-swell soils); this drives whether we need a simple slab-on-grade, a stiffened/post-tensioned slab, or pier support. *Get this wrong and the slab cracks and heaves.* This is the #1 reason not to rush.
2. **Floor plan is final** (REQ-SLAB-1). Every embed below is located off the floor plan — beds, benches, paths, zones, door positions, the control panel, and the PV/battery feed.

---

## The checklist

Grouped by trade. Walk it on site with the plan in hand before the pour crew arrives.

### 1. Subgrade & soil (the foundation under the foundation)
- [ ] Geotech report in hand; slab type selected to suit expansive clay (slab-on-grade vs. stiffened/PT vs. pier). **(MUST)**
- [ ] Sub-base compacted to spec; moisture conditioning per geotech.
- [ ] Vapor barrier under slab (REQ-SLAB-6). **(MUST)**
- [ ] Perimeter / edge insulation placed if slab thermal mass is to be decoupled from ground (REQ-SLAB-6).

### 2. Drainage — *a greenhouse floor is wet by design* (REQ-SLAB-2)
- [ ] Floor slopes to drains designed and formed (typical ¼" per ft toward drains). **(MUST)**
- [ ] Floor and/or trench drains located per floor plan and roughed in. **(MUST)**
- [ ] Drain outlet to daylight or French drain confirmed — water actually leaves the building. **(MUST)**
- [ ] Site graded so surface water flows *away* from the slab, not toward it.

### 3. Electrical conduit & stub-ups — *off-grid* (REQ-SLAB-3, REQ-PWR-*)
- [ ] Conduit + stub-up at the **control panel** location. **(MUST)**
- [ ] Conduit run for the **PV array → charge controller/battery → load center** feed. **(MUST)**
- [ ] Stub-ups for **fans, vent actuators, and sensors** per plan (so wiring isn't surface-run at child height — REQ-ELEC-1). **(MUST)**
- [ ] Stub-up for any **grow-light / Tier-3** circuits.
- [ ] Pull strings left in all conduits.
- [ ] Spare/empty conduit run for future additions (cheap now, impossible later).

### 4. Plumbing stub-ups (REQ-SLAB-4)
- [ ] Irrigation supply stub-up located per plan. **(MUST)**
- [ ] Rainwater line route to/from tank stubbed (REQ-WATER-3/5). **(MUST)**
- [ ] **White / grey / pure tank lines + sink-station supply & drains** roughed in (water architecture, [REQ-CYCLE](../design/10-requirements.md#o-resource-cycles)). **(MUST)**
- [ ] **Soil-catch potting-table drain** stubbed (returns soil to beds). 
- [ ] **Aquaponics rough-in** — capped plumbing stub + space allowance for a future fish tank ([growing program](../operate/30-growing-program.md) phasing).
- [ ] Any reservoir/hydroponic drain lines roughed in.
- [ ] Backflow prevention / **air-gap provision** for the campus tether fill (REQ-WATER-4).
- [ ] All penetrations sleeved/protected before pour.

### 4b. Built-in educational features (construction-locked, [REQ-EDU-5](../design/10-requirements.md#i-education--layout))
- [ ] **Root-window** bed structure + viewing-pane recess + drainage located per plan.
- [ ] **Worm-window** bin recess located.
- [ ] **Data station** power/data drops; **seedling & repotting stations** power + water + drains.
- [ ] **Tall-crop trellis** anchor points set with the structure anchors.

### 5. Structural anchors & embeds (REQ-SLAB-5, REQ-STR-1/4)
- [ ] Anchor bolts / embed plates set per the **wind-uplift design**, located to the structure's base plan. **(MUST)**
- [ ] Anchor layout matches the (custom) frame — verified against shop drawings. **(MUST)**
- [ ] Anchor/embed design is **sealed by the licensed architect/engineer** before pour — required for a public school building per [regulatory governance](10-regulatory-governance.md). **(MUST)**
- [ ] **Elevated water-tank tower foundation/anchors** set per the engineered stand (dead + wind load — a full tank is ~1,700 lb and a wind sail). **(MUST)**

### 6. Accessibility & finish (REQ-SLAB-7, REQ-ACC-1)
- [ ] Finished floor flush/level at the accessible entry; no lip or step. **(MUST)**
- [ ] Slip-resistant finish specified (wet floor + kids). **(MUST)**
- [ ] Thresholds at doors meet accessible rise.

### 7. Final dimensional & "measure twice" pass
- [ ] Building footprint dimensions and squareness verified against the plan. **(MUST)**
- [ ] Every embed cross-checked against the floor plan **and** the structure shop drawings — locations, heights, projections.
- [ ] Photograph the full layout (embeds, conduit, drains) before pour — invaluable for later work and as a teaching artifact.

---

## Sign-off before the pour

> Do not give the pour crew the go-ahead until each owner has signed.

| Area | Verified by | Date | OK? |
|------|-------------|------|-----|
| Geotech & slab type | | | ☐ |
| Floor plan final | | | ☐ |
| Drainage | | | ☐ |
| Electrical conduit/stub-ups | | | ☐ |
| Plumbing stub-ups | | | ☐ |
| Structural anchors/embeds | | | ☐ |
| Accessibility & finish | | | ☐ |
| Final dimensional pass | | | ☐ |
| **Authorized to pour** | | | ☐ |

---

## Open questions

> **OPEN QUESTION:** Geotech results → which slab type? (Blocks the whole document.)
> ✅ **RESOLVED:** The structure needs a sealed architect/engineer design (public school building). Anchor/embed design must be stamped before pour. See [regulatory governance](10-regulatory-governance.md).
> **OPEN QUESTION:** Roof-mount vs. ground-mount PV changes whether the structure carries array loads — affects anchors and conduit routing.

*Upstream: [`docs/design/20-site-and-orientation.md`](../design/20-site-and-orientation.md), [`docs/design/10-requirements.md`](../design/10-requirements.md) (REQ-SLAB-*, REQ-PWR-*, REQ-WATER-*).*
