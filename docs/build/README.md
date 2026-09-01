# Build — how it gets built

*Siteworks, approvals, wiring concepts, and procurement for the Kramer Elementary greenhouse. This folder turns the [design](../design/README.md) into things that get poured, permitted, and purchased. Two documents here carry unusual weight: the [slab checklist](00-slab-prepour-checklist.md) is the one artifact that can't be edited after the fact, and [regulatory governance](10-regulatory-governance.md) holds the single classification decision that sets the whole approval lane.*

---

## The docs

| Doc | What it is | Read this if… |
|-----|------------|---------------|
| [00-slab-prepour-checklist.md](00-slab-prepour-checklist.md) | **The one-way door.** Every conduit, stub-up, drain, anchor and pull-string that must exist before concrete is poured, each traced to a `REQ-SLAB-*` row. Opens with the two upstream blockers (site, zone layout) and ends with the sign-off. **Nothing pours until every MUST is signed.** | …you are anywhere near the pour. |
| [10-regulatory-governance.md](10-regulatory-governance.md) | Who and what governs building on Dallas ISD land — the layers of governance, the **occupancy-classification decision** that everything else hangs on, citable governance requirements, and sources. | …you're talking to the district, the fire marshal, or a stamping engineer. |
| [power-wiring-concept.md](power-wiring-concept.md) | Conceptual block diagrams for the off-grid system — Option A (EG4 GridBOSS + FlexBOSS21, whole-home scale) vs. **Option B (EG4 6000XP, greenhouse scale — ✅ working direction)**, with the detailed 6000XP wiring. | …you're sizing or wiring the solar + battery system. |
| [bom/](bom/README.md) | **Bills of materials** — one per subsystem, shared column format, `REQ` traces, `proposed → approved → ordered → installed` status. The BOMs *are* the procurement tracker. | …you're buying, bidding, or quoting anything. |
| ↳ [bom/off-grid-power.md](bom/off-grid-power.md) | Array, batteries, charge control, DC distribution — opens with the sizing basis (fill that in before buying anything). | |
| ↳ [bom/controls.md](bom/controls.md) | Compute core, sensors, actuators, comms, connectors, enclosure. | |
| ↳ [bom/irrigation.md](bom/irrigation.md) | Harvest → storage → gravity drip, fertigation, freeze protection. | |
| ↳ [bom/structure.md](bom/structure.md) | Frame, glazing, vents, doors, beds, and the storage that makes a class of 25 workable. | |
| ↳ [bom/BOM_considered.md](bom/BOM_considered.md) | **Decision log** — every product or approach evaluated for controls, valve drivers, hydro and charge control, marked Selected / Pending / Disregarded with the rationale. Read before re-buying a rejected part. | |

## How the build is gated

```
design/20 site ─────┐
design/80 zone layout ──► 00 slab checklist ──► POUR (one-way door)
design/90 device schedule ──► bom/* quantities ──► procurement (TEC Ch. 44 "or equal" bids)
10 regulatory: occupancy classification ──► which code path, which approvals, who stamps
```

- **Sizing before parts.** BOM quantities stay `TBD` until the engineering calc behind them is done — the power BOM opens with its sizing basis for exactly this reason.
- **Spec, then SKU.** Because this is school land, BOMs are written as biddable specs with *"or equal"*, not locked part numbers ([REQ-REG-5](10-regulatory-governance.md)).
- **Tiers apply to the build too.** 🔴 Red work (anything licensed, stamped, or on the mains side) is named as such; see [Roles & Tiers](../operate/10-roles-and-tiers.md).

## Status

🟡 **Scaffolding.** Checklists and governance are drafted; BOMs await the zone layout and device schedule for quantities; the wiring concept has a working direction pending the Red designer.

*Up: [`../README.md`](../README.md) (docs map) · [`../../README.md`](../../README.md) (project). Previous: [`../design/`](../design/README.md). Next: [`../operate/`](../operate/README.md).*
