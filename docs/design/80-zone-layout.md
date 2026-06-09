# Zone Layout — the floor plan

*Where everything goes. This is the synthesis doc — it lands every system (growing, passive, power, water, controls) in physical space, and it's the **keystone that unblocks the BOMs and the slab.** Finalizing it satisfies [REQ-SLAB-1](../build/00-slab-prepour-checklist.md) (floor plan before pour) and sets the irrigation-zone and device counts the [controls](../build/bom/controls.md) and [irrigation](../build/bom/irrigation.md) BOMs need — which in turn yield the Tier 1/2/3 load list the [power BOM](../build/bom/off-grid-power.md) waits on.*

> **Status:** 🟡 Schematic v1. Arrangement is *relative to orientation*; absolute positions firm up once [site & orientation](20-site-and-orientation.md) and exact dimensions are set. **Decided:** balanced **soil beds + a hydroponic demo**; gathering **both** — a covered outdoor pad (primary) + a small indoor nook.

---

## The layout logic (what drives the arrangement)

Working assumption: **~20 × 40 ft, E–W long axis**, broad south face ([site rec](20-site-and-orientation.md)). The plan follows five rules:

1. **Light gradient** — full-sun crops on the **south** side; shade-tolerant + work zones to the **north** ([REQ-EDU-1](10-requirements.md#i-education--layout)).
2. **One-glance supervision** — a **central circulation spine** so one adult sees the whole interior ([REQ-EDU-3](10-requirements.md#i-education--layout)); ADA-width (≥ 48").
3. **Passive airflow** — **south roll-up sides = breeze intake**; **north wall = insulated/reflective + thermal-mass water drums**; **ridge vent + solar chimney = exhaust** ([REQ-COOL](10-requirements.md#b-cooling--ventilation--the-headline-system), [REQ-PASV](10-requirements.md#m-passive-architecture)).
4. **Teach outside, grow inside** — the **covered outdoor pad** is the primary gathering space, keeping a class *out* of the interior to preserve the light-touch **Group U** classification ([regulatory](../build/10-regulatory-governance.md#-the-decision-that-governs-everything-occupancy-classification)).
5. **Infra cool, shaded, out of reach** — controls enclosure and power gear sited in the coolest/shaded corner ([REQ-CTRL-5](10-requirements.md#k-electronics--controls-architecture)), never at child height.

## Schematic plan

```
                    N  — insulated/reflective wall + ▓ thermal-mass water drums ▓
  ┌──────────────────────────────────────────────────────────────────────┐
  │ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ thermal-mass water drums (north wall) ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │
  │ [IZ3 north raised beds]   [IZ5 germination/   [work/potting] [CONTROLS│
  │  (shade-tolerant)          propagation bench]  (child+ADA ht) ENCL.]  │
  │ ══════════════ central ADA circulation spine (≥48") ═════════════════ │
  │ [IZ1 south in-ground] [IZ2 south raised] [IZ4 ADA  [IZ6 hydro] [DATA / │
  │  (full sun)            beds              bed]       demo]      research]│
  │ ~~~~~~~~~~~~ south roll-up sides (breeze intake) + awnings ~~~~~~~~~~~~ │
  └──┬─────────────────────────────────┬──────────────────────────┬───────┘
     │ indoor nook / calm-sensory zone  │  [solar chimney]          │ ENTRY/
     │ (IZ7 wicking beds nearby)        │                           │ AIRLOCK (ADA)
     └──────────────────────────────────┘                          └───┬────
                    S — sun + prevailing breeze                         │ door
                                                          ┌─────────────┴──────┐
   header tank (elevated) · pure tank · cow dock          │ COVERED OUTDOOR PAD │
   near entry/service end; cistern just outside           │ instruction (primary│
                                                          │ gathering) + IZ8     │
                                                          │ planters · shade     │
                                                          └─────────────────────┘
```

*Schematic only — proportions not to scale. Mirror E↔W to suit the real entry approach from campus.*

## Zones

### Growing zones → irrigation zones (this sets the valve count)

| ID | Zone | Location / why | Irrigation |
|----|------|----------------|-----------|
| **IZ1** | South in-ground soil beds | Best light; hands-in-dirt | Drip, latching valve |
| **IZ2** | South raised soil beds | Light + back-friendly | Drip, latching valve |
| **IZ3** | North raised beds | Shade-tolerant crops | Drip, latching valve |
| **IZ4** | ADA wheelchair-height bed | Accessible participation ([REQ-ACC-2](10-requirements.md#h-accessibility--inclusion)) | Drip, latching valve |
| **IZ5** | Germination / propagation bench | Work height; optional grow light | Fine/low-flow line |
| **IZ6** | Hydroponic demo | Research/contrast; EC/pH | **Recirculating** (own loop, off the drip manifold) |
| **IZ7** | Wicking beds | Multi-day untended buffer | **Sub-irrigated** (separate fill) |
| **IZ8** | Outdoor pad planters | Edge growing; demo | Drip / hose-bib |

→ **~6 drip latching-valve zones (IZ1–5, IZ8) + 1 recirculating (IZ6) + 1 wicking fill (IZ7).** This is the count the [irrigation BOM](../build/bom/irrigation.md) needs.

### Functional & infrastructure zones

| Zone | Where | Notes |
|------|-------|-------|
| Entry / airlock | One end (campus-facing) | ADA entry; door never locks occupants in ([REQ-SAFE-1](10-requirements.md#g-safety--egress)) |
| Central circulation spine | Length of interior | ADA + sightline ([REQ-EDU-3](10-requirements.md#i-education--layout)) |
| Indoor flexible nook / calm-sensory | South corner | Bad-weather gathering + [REQ-ACC-3](10-requirements.md#h-accessibility--inclusion) calm zone |
| **Covered outdoor pad** | Attached, shaded | **Primary** instruction (Group U preserving) |
| Data / research corner | Interior, near power | Sensors hub, dashboards ([REQ-DATA](10-requirements.md#j-data--monitoring--the-optional-layer)) |
| Work / potting | North, mid | Child + one ADA height ([REQ-EDU-2](10-requirements.md#i-education--layout)) |
| Controls enclosure | Cool/shaded corner, high | [REQ-CTRL-5](10-requirements.md#k-electronics--controls-architecture); out of reach |
| Water infra | Service end | Elevated header tank, pure tank; cistern just outside |
| Power / cow dock | Near entry | Cow rolls out for events; fixed reserve stays ([REQ-PWR-8](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)) |
| Thermal mass | North wall | Water drums ([REQ-PASV-6](10-requirements.md#m-passive-architecture)) |
| Solar chimney + ridge vent | Ridge / S-center | Passive exhaust ([REQ-PASV-2](10-requirements.md#m-passive-architecture)) |

### Built-in educational features — *construction-locked*

From the science/garden teacher ([growing program](../operate/30-growing-program.md)). Each is designed *into* a bed/structure now — **one-way door** ([REQ-EDU-5](10-requirements.md#i-education--layout)):

| Feature | What / where | Build note |
|---------|--------------|-----------|
| **Root window** | Below-grade viewing glazing into a raised bed — taproot vs. fibrous, potatoes | Built into the bed wall; drainage + viewing pane |
| **Worm window** | Cutaway view into a vermicompost bin | Viewing pane; sited near work zone |
| **Hydroponic demo** | Small-scale, **visible reservoir** (IZ6) | Clear reservoir; own loop |
| **Data station** | Sensors + dashboard made visible (data corner) | Power/data drops ([REQ-SLAB-3](#a2-foundation--slab--the-one-way-door)) |
| **Tall-crop trellis** | Walk-under climbing-crop arch over the spine | Anchored to structure/slab |
| **Seedling station** | Germination bench + grow lights (IZ5) | Power + water + drainage |
| **Repotting station** | Work bench, child + ADA height | Water + drainage nearby |
| **Soil-catch potting table** | Table with an integrated **hole + catchment** to scrape soil into → returned to beds | Drain to soil-catch; closes the soil loop |
| **Aquaponics rough-in** | *Future* — stub plumbing + space/structural allowance near a future fish-tank spot | Roughed-in now, built later (like spare conduit) |

## What this unblocks
- **Slab** ([REQ-SLAB-1](../build/00-slab-prepour-checklist.md)) — drains, conduit, plumbing stub-ups, anchors **and the built-in features above** all place off this plan.
- **Irrigation BOM** — ~8 zones → valve/line counts.
- **Controls BOM** — sensors/actuators per zone → device counts → **Tier 1/2/3 load list** → unblocks the **power BOM** sizing.

## Open questions
> **OPEN QUESTION:** Final site orientation + exact dimensions → absolute positions, mirror direction, door location.
> **OPEN QUESTION:** Bed count/size within each zone → exact IZ valve count and growing area.
> **OPEN QUESTION:** Is the cistern inside the footprint or external? (Affects slab + the 800 sq ft budget.)
> **OPEN QUESTION:** Header-tank support structure + height for adequate gravity head.

*Parent: [`00-design-principles.md`](00-design-principles.md). Synthesizes: [`20-site`](20-site-and-orientation.md), [`50-passive`](50-passive-architecture.md), [`60-power`](60-power-architecture.md), [`70-cycles`](70-resource-cycles.md). Feeds: [`../build/00-slab-prepour-checklist.md`](../build/00-slab-prepour-checklist.md), [`../build/bom/`](../build/bom/).*
