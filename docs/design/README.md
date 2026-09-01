# Design — what we're building, and why

*The reasoning chain for the Kramer Elementary greenhouse: **principles → requirements → site → sub-domain designs → the floor plan → the quantities.** Everything in [`build/`](../build/README.md) and [`operate/`](../operate/README.md) traces back to a row in this folder. Read in file order the first time; after that, [`10-requirements.md`](10-requirements.md) is the doc you'll keep coming back to.*

---

## Reading order

| # | Doc | What it decides | Read this if… |
|---|-----|-----------------|---------------|
| 00 | [Design Principles](00-design-principles.md) | The seven values and their **priority order — Safety → Education → Resilience → Production → Showcase** — plus the project constraints already settled (off-grid, slab, ~20×40 ft, Dallas). When two good options conflict, this order decides. | …you want to know *why* anything else here is the way it is. |
| 10 | [Requirements](10-requirements.md) | **The spine.** Checkable `REQ-*` rows grouped A–O (structure, slab, cooling, shading, heating, water, electrical, off-grid power, safety, accessibility, education, data, controls architecture, network, passive, resource cycles). Every BOM line, checklist item and SOP cites one. | …you are the designer, contractor, or anyone asked "does it meet spec?" |
| 20 | [Site & Orientation](20-site-and-orientation.md) | *Where* on campus and *which way it faces* — Dallas sun and wind facts, orientation logic, site criteria, a candidate scorecard. Gates the solar array, drainage, and the slab. | …the site isn't fixed yet, or you're evaluating a candidate location. |
| 30 | [Electronics & Controls](30-electronics-and-controls.md) | Sub-principles for the electronics: poka-yoke connectors, RJ45-inside / M12-at-the-wet-boundary, core/edge separation, design-around-failure, commodity-in-a-managed-enclosure, SELV DC in wet zones, surge protection. | …you're specifying or wiring anything with a sensor, actuator, or controller. |
| 40 | [Network & Connectivity](40-network-and-connectivity.md) | **HA is not the safety system** — the rule everything else here follows. Uplink sized to the alert, segmented network (kids / public / QR invite), network gear as a tiered off-grid load, self-recovering design, the locked band-diverse transport stack, the QR/dashboard experience. | …you touch Home Assistant, the switch, the APs, or the cellular uplink. |
| 50 | [Passive Architecture](50-passive-architecture.md) | The survival layer — what keeps plants alive with **zero electricity and zero human attention**: air turnover, shade, gravity irrigation, freeze, thermal mass, structural fail-safes. Flags which features are **construction-locked**. | …you want to understand how the building survives a dead battery in August. |
| 60 | [Power Architecture](60-power-architecture.md) | The off-grid system: three-layer resilience, Tier 1/2/3 load shedding, two isolated 48 V LiFePO₄ banks — the fixed **house bank** and the mobile **"power cow"** — and the emergency-only campus tether. | …you're sizing, wiring, or explaining the solar + battery system. |
| 70 | [Resource Cycles](70-resource-cycles.md) | Closing the loops: water harvested by *quality* (rain / condensate / grey), four composting methods, how the cycles integrate, and the construction-locked pieces. | …you work on water, compost, or the "produce no waste" story. |
| 80 | [Zone Layout](80-zone-layout.md) | **The floor plan.** The synthesis doc that lands every system in physical space (zones IZ1–8 + functional zones). The keystone that unblocks the BOMs and the slab. | …you need to know where anything goes. |
| 90 | [Bed & Device Schedule](90-bed-and-device-schedule.md) | **The quantities.** Beds, devices, watts and power tier per zone — the load envelope that sizes the array and battery and fills the BOM quantity columns. | …you're filling in a `TBD` in a BOM. |
| — | [images/](images/) | Drawings. Currently the Keynote floor plan (`floorPlan.key`). | |

## How the docs depend on each other

```
00 principles ──► 10 requirements ──► every BOM row / checklist item / SOP
                        │
   20 site ─────────────┤   30 electronics ─► 40 network
                        │   50 passive ──┐
                        ▼                ├──► 80 zone layout ──► 90 bed & device schedule
   60 power ◄───────────┘   70 cycles ───┘          │                     │
                                                    ▼                     ▼
                                          build/00 slab checklist   build/bom/* quantities
```

- **Sub-domain docs (30–70) are principles first, hardware second.** Each ends by naming the `REQ-*` rows it feeds; the hardware lands in the [BOMs](../build/bom/README.md).
- **Construction-locked** items — anything that has to exist before the slab pours — are called out in 50, 70 and 80 and roll up into the [slab pre-pour checklist](../build/00-slab-prepour-checklist.md).
- Every doc ends with its own `> **OPEN QUESTION:**` block; resolutions are recorded in place as `✅ RESOLVED (date)`.

## Status

🟡 **Design in progress.** Principles and requirements are stable; site, zone layout and the device schedule are the live fronts — they're what unblock the slab and the BOM quantities.

*Up: [`../README.md`](../README.md) (docs map) · [`../../README.md`](../../README.md) (project). Next: [`../build/`](../build/README.md).*
