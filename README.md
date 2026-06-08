# Casa de Verdant Veritas

> House of Truth & Learning Covered In Greenery

**Specifications for designing, building, and operating a greenhouse at Kramer Elementary School — Dallas, Texas.**

This repository is the single source of truth for the project: the design intent, the build documentation, and the day-to-day operating procedures for a to-be-constructed teaching greenhouse. It is a living document set — written to be read by teachers, parents, volunteers, district staff, and the contractors and donors who help bring it to life.

---

## What we're building

A **mid-size, custom-built greenhouse** (roughly 20×40 ft on a concrete slab, **totally off-grid** on solar + battery) that serves four overlapping missions:

1. **Hands-on education** — a living classroom where students grow plants and learn science, ecology, and nutrition. *This is the primary mission; every other goal yields to it when they conflict.*
2. **Food production** — fresh produce for the cafeteria and garden-to-table learning.
3. **Community & showcase** — a visible point of pride for the school and neighborhood, usable for events and demonstrations.
4. **Research & data** — sensors and monitoring that let students collect real environmental data and run controlled experiments.

**Operated by** teachers and students during the school year, with a **parent/volunteer group** providing upkeep and summer coverage. This operating model drives a hard design constraint: systems must be **safe, simple, and resilient to gaps in human attention** (nights, weekends, and the long Texas summer break).

**Being off-grid sharpens that constraint.** The worst case is a *hot-and-cloudy* multi-day summer stretch — peak cooling demand exactly when solar generation and battery reserves bottom out. So the design leans on **passive systems that survive with zero electricity**, with powered cooling as a solar-correlated assist. See the [design principles](docs/design/00-design-principles.md#project-constraints-decided).

## Site context

- **Location:** Kramer Elementary School, Dallas, TX
- **USDA Hardiness Zone:** 8a/8b
- **Climate drivers that shape the design:**
  - Long, hot, humid summers (sustained 95–105 °F) → **cooling and ventilation are the dominant engineering challenge**, not heating
  - Mild winters with occasional hard freezes (cf. Feb 2021) → freeze protection for pipes and tender plants
  - Intense solar load → shade management and glazing choice
  - Hail and severe thunderstorms → impact-resistant glazing and structural wind rating
  - The summer break overlaps the hottest, highest-stress growing months → automation and volunteer SOPs must cover it

## Repository structure

```
.
├── README.md                ← you are here
├── LICENSE                  ← MIT
└── docs/
    ├── design/              ← what we're building and why (principles → requirements → drawings)
    │   ├── 00-design-principles.md
    │   ├── 10-requirements.md
    │   ├── 20-site-and-orientation.md
    │   ├── 30-electronics-and-controls.md
    │   ├── 40-network-and-connectivity.md
    │   ├── 50-passive-architecture.md
    │   ├── 60-power-architecture.md
    │   └── 70-resource-cycles.md
    ├── build/               ← how it gets built (siteworks, procurement, assembly, inspections)
    │   ├── 00-slab-prepour-checklist.md
    │   ├── 10-regulatory-governance.md
    │   └── bom/             ← bills of materials (one per subsystem)
    │       ├── README.md
    │       ├── off-grid-power.md
    │       ├── controls.md
    │       └── irrigation.md
    └── operate/             ← how it runs (growing calendar, SOPs, maintenance, safety, curriculum)
        ├── 00-operating-principles.md
        ├── 10-roles-and-tiers.md
        ├── 20-troubleshooting-runbook.md
        └── sops/            ← laminated, point-of-use procedures
            ├── SOP-01-daily-check.md
            ├── SOP-02-weekly-check.md
            ├── SOP-03-summer-survival.md
            └── SOP-04-something-isnt-working.md
```

Each phase gets its own folder. Documents are numbered (`00-`, `10-`, `20-`…) so the intended reading order is obvious and new docs can be inserted without renumbering everything.

## Project phases

| Phase | Folder | Status |
|-------|--------|--------|
| **Design** — principles, requirements, site & structure decisions | `docs/design/` | 🟡 In progress |
| **Build** — procurement, foundation, assembly, inspections | `docs/build/` | 🟡 In progress |
| **Operate** — growing program, maintenance, safety, curriculum | `docs/operate/` | 🟡 In progress |

## How to contribute

This is a specs repo, not a code repo — contributions are written documents, decisions, and drawings.

- Keep each document focused on one topic; link between them rather than duplicating.
- Record *decisions* with their *reasoning* — a future volunteer should understand not just what we chose but why.
- Flag open questions explicitly (e.g. `> **OPEN QUESTION:** …`) so they don't get lost.

## Status

🌱 **Early design.** We're establishing design principles before committing to a specific kit, foundation, or systems package.

---

*Casa de Verdant Veritas — "house of green truth." A place where kids grow things and learn what's real.*
