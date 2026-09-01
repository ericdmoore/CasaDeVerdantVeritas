# Docs — the map

*Everything about the Kramer Elementary greenhouse lives under this folder, split by project phase: **design** (what and why) → **build** (how it gets made) → **operate** (how it runs). Files are numbered (`00-`, `10-`, `20-`…) so the reading order inside each folder is obvious and new docs can be inserted without renumbering. Project overview, site context, and contribution rules are in the [top-level README](../README.md).*

---

## Start here, by who you are

| You are… | Read first | Then |
|----------|------------|------|
| **A teacher or student** running the greenhouse | [SOP-01 Daily Check](operate/sops/SOP-01-daily-check.md) | [SOP-04 Something Isn't Working](operate/sops/SOP-04-something-isnt-working.md) · [Growing calendar](operate/40-growing-calendar.md) |
| **A volunteer** (weekly / summer) | [Roles & Tiers](operate/10-roles-and-tiers.md) — know which color you are | [SOP-02 Weekly](operate/sops/SOP-02-weekly-check.md) · [SOP-03 Summer Survival](operate/sops/SOP-03-summer-survival.md) |
| **An 🟠 Amber (infra) volunteer** | [Troubleshooting Runbook](operate/20-troubleshooting-runbook.md) | [Electronics & Controls](design/30-electronics-and-controls.md) · [Controls BOM](build/bom/controls.md) |
| **The 🔴 Red designer / contractor** | [Requirements](design/10-requirements.md) | [Slab Pre-Pour Checklist](build/00-slab-prepour-checklist.md) · [Regulatory Governance](build/10-regulatory-governance.md) · the [BOMs](build/bom/README.md) |
| **A donor, district staffer, or curious parent** | [Design Principles](design/00-design-principles.md) | [Growing Program](operate/30-growing-program.md) · [Zone Layout](design/80-zone-layout.md) |

---

## [`design/`](design/) — what we're building, and why

The reasoning chain: **principles → requirements → sub-domain designs → the floor plan → the quantities.** Everything downstream traces back here.

| Doc | What it is |
|-----|------------|
| [00-design-principles.md](design/00-design-principles.md) | The values, in priority order — **Safety → Education → Resilience → Production → Showcase**. When two good options conflict, this order decides. Also records the project constraints already settled (off-grid, slab, ~20×40 ft). |
| [10-requirements.md](design/10-requirements.md) | The spine. Concrete, checkable `REQ-*` rows (REQ-SAFE, REQ-COOL, REQ-PWR, REQ-WATER, REQ-CTRL, REQ-NET…), each traced to a principle. Every BOM line and build checklist item cites one. |
| [20-site-and-orientation.md](design/20-site-and-orientation.md) | Decision doc for *where on campus* and *which way it faces* — sun path, summer breeze, drainage, and the solar array all hang off this. |
| [30-electronics-and-controls.md](design/30-electronics-and-controls.md) | Sub-principles for the electronics: poka-yoke connectors, the core/edge split, design-around-failure, commodity-in-a-managed-enclosure, SELV DC in wet zones, surge protection. |
| [40-network-and-connectivity.md](design/40-network-and-connectivity.md) | How sensors, actuators, the controller core, Home Assistant, and the outside world talk — and the locked, band-diverse transport stack. |
| [50-passive-architecture.md](design/50-passive-architecture.md) | The survival layer: what keeps the greenhouse alive with **zero electricity and zero human attention** — solar chimney, shade, thermal mass, gravity irrigation. |
| [60-power-architecture.md](design/60-power-architecture.md) | The off-grid system: three-layer resilience, tiered load shedding, the two isolated 48 V banks (house + the mobile "power cow"), and the emergency campus tether. |
| [70-resource-cycles.md](design/70-resource-cycles.md) | Closing the loops — rain/condensate/greywater harvesting and composting; the "produce no waste" design. |
| [80-zone-layout.md](design/80-zone-layout.md) | **The floor plan.** The synthesis doc that lands every system in physical space; the keystone that unblocks the BOMs and the slab. |
| [90-bed-and-device-schedule.md](design/90-bed-and-device-schedule.md) | **The quantities.** Beds, sensors, actuators and their power tier — the Tier 1/2/3 load list that sizes the battery and array. |
| [images/](design/images/) | Drawings — currently the Keynote floor plan (`floorPlan.key`). |

## [`build/`](build/) — how it gets built

Siteworks, approvals, wiring concepts, and procurement. The BOMs are the procurement tracker; the slab checklist is the one document that can't be edited after the fact.

| Doc | What it is |
|-----|------------|
| [00-slab-prepour-checklist.md](build/00-slab-prepour-checklist.md) | **The one-way door.** Every conduit, stub-up, anchor and drain that must exist before concrete is poured. Nothing pours until every MUST is signed off. |
| [10-regulatory-governance.md](build/10-regulatory-governance.md) | Who and what governs building on Dallas ISD land — authorities, codes, approvals, and the one classification question that decides the whole regulatory lane. |
| [power-wiring-concept.md](build/power-wiring-concept.md) | Conceptual block diagrams for the off-grid power system — two candidate platforms (modular Victron vs. EG4 all-in-one) side by side. |
| [bom/](build/bom/README.md) | **Bills of materials**, one per subsystem, in a shared column format with `REQ` traces and a `proposed → approved → ordered → installed` status. |
| ↳ [bom/off-grid-power.md](build/bom/off-grid-power.md) | Array, batteries, charge control, DC distribution — opens with the sizing basis. |
| ↳ [bom/controls.md](build/bom/controls.md) | Compute core, sensors, actuators, comms, connectors, enclosure. |
| ↳ [bom/irrigation.md](build/bom/irrigation.md) | Harvest → storage → gravity drip, fertigation, freeze protection. |
| ↳ [bom/structure.md](build/bom/structure.md) | Frame, glazing, vents, doors, beds, and the storage that makes a class of 25 workable. |
| ↳ [bom/BOM_considered.md](build/bom/BOM_considered.md) | **Decision log** — every product or approach evaluated for controls, valve drivers, hydro, and charge control, marked Selected / Pending / Disregarded with the rationale. Read before re-buying a rejected part. |

## [`operate/`](operate/) — how it runs

The human system around the building. A greenhouse fails from neglect far more often than from bad construction, so this folder is about rotas, tiers, and procedures a new volunteer can follow in 15 minutes.

| Doc | What it is |
|-----|------------|
| [00-operating-principles.md](operate/00-operating-principles.md) | How it gets run day to day and season to season — the operating counterpart to the design principles. |
| [10-roles-and-tiers.md](operate/10-roles-and-tiers.md) | **🟢 Green · 🟠 Amber · 🔴 Red** — who does what, and who is *allowed* to touch what. The tier is a safety boundary, not a skill label. |
| [20-troubleshooting-runbook.md](operate/20-troubleshooting-runbook.md) | For Amber: localize a fault fast from the telemetry the system already collects, fix what's in the low-voltage domain, hand the rest to Red. |
| [30-growing-program.md](operate/30-growing-program.md) | What we grow, who grows it, where it goes, and how the program funds itself — the four missions made operational. |
| [40-growing-calendar.md](operate/40-growing-calendar.md) | Season-by-season anchor crops for Dallas zone 8a/8b, tuned to K–5 and growing through summer. A draft for the garden teacher to refine. |
| [sops/](operate/sops/README.md) | **Laminated, point-of-use procedures.** One page each, photographable, owned by a tier. |
| ↳ [SOP-01 Daily Check](operate/sops/SOP-01-daily-check.md) | Teacher + students, every school day, ~5 min. |
| ↳ [SOP-02 Weekly Check](operate/sops/SOP-02-weekly-check.md) | Volunteer, weekly year-round, ~30 min. |
| ↳ [SOP-03 Summer Survival](operate/sops/SOP-03-summer-survival.md) | The summer-break rota and the emergency campus tether — set up *before* school lets out. |
| ↳ [SOP-04 Something Isn't Working](operate/sops/SOP-04-something-isnt-working.md) | Green's 2-minute triage and escalation path. |
| ↳ [SOP-05 Compost Care](operate/sops/SOP-05-compost-care.md) | Weekly compost routine, teacher + students. |
| ↳ [SOP-06 Water-System Check](operate/sops/SOP-06-water-system-check.md) | Weekly tanks / filters / valves walk-through; escalate to Amber. |

---

## Conventions used across the docs

- **Traceability.** Requirements are `REQ-AREA-n` (e.g. `REQ-COOL-2`, `REQ-PWR-10`). BOM rows, checklists and SOPs cite the requirement they satisfy, so any line item can be defended back to a principle.
- **Open questions** are called out inline as `> **OPEN QUESTION:** …` and resolved in place as `> ✅ **RESOLVED (date):** …` — decisions keep their reasoning next to them.
- **Tiers** color every task: 🟢 Green (anyone), 🟠 Amber (low-voltage infra volunteers), 🔴 Red (licensed / professional). Defined in [Roles & Tiers](operate/10-roles-and-tiers.md).
- **Power tiers** are separate from people tiers: Tier 1 (safety/control, shed last) · Tier 2 (cooling assist) · Tier 3 (HA, dashboards, lights — shed first). Defined in [Power Architecture](design/60-power-architecture.md).
- **"or equal."** BOM specs are written as biddable specifications, not locked part numbers, because district procurement may require competitive bids.
- **Numbering** gives reading order within a folder; docs without a number (e.g. `power-wiring-concept.md`) are side references.

*Parent: [`../README.md`](../README.md).*
