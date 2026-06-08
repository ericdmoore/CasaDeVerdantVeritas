# Design Principles

*The values that guide every design decision for the Kramer Elementary greenhouse. When a specific choice is unclear or two good options conflict, we resolve it by returning to these principles — in order.*

---

## The order of priorities

This greenhouse serves four missions, but they are **not equal**. When they conflict, we decide in this order:

1. **Safety** — it is full of children. Nothing else matters if someone gets hurt, or worse keeps getting hurt.
1. **Education** — it is a classroom first. A lower-yield design that teaches better wins.
1. **Resilience** — it must survive nights, weekends, and summer break with minimal attention.
1. **Production** — it should really grow plants.
1. **Showcase** — it should look like something to be proud of, last on the list because pride follows from doing the rest well.

> Keep this hierarchy in mind. Most of the principles below are just this list applied to a specific question.

---

## Project constraints (decided)

These are settled facts the rest of the design must respect. They came out of the open questions below — recorded here at the top because they shape everything.

- **Foundation: concrete slab.** This creates a one-way door — floor plan, drainage, conduit, plumbing stub-ups, and structure anchors must all be finalized *before the pour*. The slab also doubles as **thermal mass** (a free buffer against temperature swings). *(Decided 2026-06-08.)*
- **Power: totally off-grid.** Solar + battery, no utility connection. The design must **lean on passive systems to survive the worst case — a hot *and* cloudy multi-day summer stretch** — when cooling demand peaks while solar generation and battery reserves bottom out. Powered systems are an assist, not the survival path. *(Decided 2026-06-08.)*
- **Build: custom / semi-custom, not kit-limited.** We'll lean on basic construction skills and build what meets our goals rather than accept a kit's limits. This frees us to oversize ventilation and tune the floor plan — but moves the wind-load and code engineering responsibility onto us. *(Decided 2026-06-08.)*
- **Site & orientation: still open.** See open questions.

---

## 1. Safe by default

Children, including small ones, will be inside and around this structure.

- **No sharp edges, no pinch points, no glass at child height.** Glazing within reach must be impact-resistant polycarbonate, not glass — this also covers the Dallas hail requirement, so it's a "twofer".
- **No standing water deeper than a few inches** that a young child could fall into. Reservoirs and tanks are covered or fenced.
- **Electrical is GFCI-protected, conduit-run, and out of reach.** Water and electricity share the building; treat every circuit accordingly.
- **Heat is the real hazard here.** A closed greenhouse in a Dallas summer can exceed lethal temperatures within minutes. Doors must never lock occupants in, ventilation failure must fail *open*, and there must be a clear, fast exit. See Principle 4.
- **Non-toxic materials and treatments.** No arsenic-treated lumber, no pesticides incompatible with an environment full of kids. Assume everything will be touched and occasionally tasted.

## 2. Teach, don't just grow

The building itself is a teaching tool. Design it to be *legible* — kids should be able to see how it works.

- **Make systems visible.** Expose the water lines, the sensors, the airflow. A transparent reservoir teaches more than a hidden one. Label things.
- **Build for small hands and short heights.** Work surfaces, beds, and controls reachable by a 2nd grader, not just an adult.
- **Sightlines for supervision and curiosity.** A teacher should see the whole space at a glance; a child should be able to watch what's happening.
- **Zones for different lessons.** Room for a hands-in-the-dirt bed, a hydroponic demo, a germination station, a data corner. Variety is curriculum.
- **Capacity for a class, not a couple.** Circulation and bench layout should let ~20–25 students move through without crowding.

## 3. Designed for Dallas, not for a catalog photo

The dominant engineering problem here is **getting heat out**, not keeping it in. Most greenhouse marketing assumes a cold climate; we must invert that thinking. And because we're **off-grid**, the cooling that *survives the worst day* cannot depend on electricity at all.

- **Passive cooling is the primary survival system — powered cooling is an assist.** The cheapest cooling is the heat you never let in: aggressive shade, oversized natural ventilation (roll-up sides + ridge/gable vents), wax-piston auto-vents that open on heat with zero power, and the slab as thermal mass. These must hold the line on a hot, cloudy stretch when there's little solar and a low battery. Size the *passive* vent area for the 100 °F+ design day, not just the fans.
- **Let powered cooling ride the sun.** Exhaust fans and evaporative cooling are an assist that runs hardest when the sun is strongest — which is conveniently when it's hottest. Favor **solar-direct DC fans** that spin off the panels without draining the battery, so cooling scales with the heat load for free. (Evaporative cooling works here because TX summer humidity still leaves headroom — but it also *consumes water*, a real cost off-grid.)
- **Shade is a first-class system, not an afterthought.** Retractable or seasonal shade cloth (30–50%) to shed solar load in summer and let light in during winter.
- **Glazing tuned for diffusion and impact.** Twin/triple-wall polycarbonate diffuses harsh direct sun (better for plants and people) and shrugs off hail far better than glass.
- **Modest, targeted freeze protection.** We don't need to heat all winter — we need to survive the occasional hard freeze. Frost protection for water lines and a way to protect tender plants on the handful of freezing nights.
- **Orientation and siting** chosen for sun path, prevailing summer breeze (for cross-ventilation), and storm-water drainage. Decided in the site doc, but flagged as a principle because it's nearly impossible to fix later.

## 4. Resilient when no one is watching

Teachers leave at 3 pm. Volunteers cover weekends imperfectly. And **summer break — the hottest, most dangerous growing window — is when the school is emptiest.** The design must assume gaps in attention.

- **Fail safe, fail open.** On power or controller failure, vents open and fans default to a safe state. Never trap heat. Never trap people. Off-grid, "power failure" isn't a rare grid outage — it's a *predictable* outcome of a cloudy stretch, so the fail-open passive layer is the everyday backstop, not an edge case.
- **Automate the life-or-death loop.** Temperature-triggered ventilation and irrigation should run without a human. This is not a luxury feature; in a Dallas summer it's the difference between a thriving greenhouse and a dead one (or worse) by Monday.
- **Budget the battery by priority, and shed loads.** With no grid to fall back on, define power tiers: **Tier 1** — the tiny critical loop (control brain, temp sensing, alerting, night irrigation) is battery-protected and shed last; **Tier 2** — cooling assist (fans, evap pump), ideally solar-direct; **Tier 3** — program loads (grow lights, data logging, hydroponic pumps) shed first when the battery runs low. The greenhouse must survive a dead battery on passive means alone.
- **Alerting.** Remote temperature/moisture alerts to a phone so a volunteer knows *before* there's a crisis. (This also feeds Mission 4 — research/data.)
- **Choose plants and schedules that match the coverage.** Summer planting plans should assume minimal human help. Don't design a system that requires daily expert attention the school can't provide.

## 5. Simple to run, instrumented to learn

There's a tension between Mission 1 (simple for teachers/volunteers) and Mission 4 (rich data). Resolve it by **layering**:

- **The base system is dead simple** — a volunteer with no training can keep plants alive following a one-page SOP.
- **The data layer sits on top and is optional.** Sensors and logging enrich lessons and research but are *not* in the critical path. If the data system breaks, the plants are fine.
- **Standard, repairable, locally-sourced parts.** Favor components a Dallas hardware store or irrigation supplier stocks over proprietary kit-only parts. A broken part should be fixable in a weekend, not a six-week order.
- **Document everything as SOPs.** Every recurring task gets a written, photographed procedure (lives in `docs/operate/`).

## 6. Affordable to build, cheaper to keep

A school budget builds it once; a school budget also has to *keep* it running for years.

- **Favor low operating cost over low purchase price.** Passive cooling, rainwater capture, and efficient fans cost more upfront and save the program's life over time.
- **Water-wise by design.** Drip/recirculating irrigation, rainwater harvesting from the large roof area, and mulching. Water is both a cost and a lesson.
- **Phaseable.** Design so the core structure goes up first and the showcase/research extras can be added as grants and donations arrive. Don't let a missing nice-to-have block the opening.
- **Build a maintenance reserve into the plan**, not just a construction budget.

## 7. Accessible and inclusive

- **ADA-aware paths and at least one accessible work height**, so every student — including those using a wheelchair — can fully participate.
- **Sensory-friendly options.** The greenhouse is a great space for students who benefit from quiet, tactile, nature-based learning; design at least one calm zone.

---

## How to use these principles

When you're writing a requirement, choosing a kit, or settling a debate, **cite the principle**. For example:

> *Chose polycarbonate over glass glazing — Principle 1 (no glass at child height) and Principle 3 (hail resistance).*

This keeps the reasoning traceable and keeps us honest about the trade-offs we're making.

---

## Open questions

**Still open:**

> **OPEN QUESTION:** Exact site and orientation on the Kramer campus — drives sun path, prevailing summer breeze for cross-ventilation, drainage, and where the solar array goes. The biggest remaining unknown.

**Resolved (see [Project constraints](#project-constraints-decided)):**

> ✅ **Foundation** → concrete slab. *(2026-06-08)*
> ✅ **Power** → totally off-grid, solar + battery, passive-survives-worst-case. *(2026-06-08)*
> ✅ **Build approach** → custom / semi-custom, not kit-limited. *(2026-06-08)*

**New questions these decisions raise:**

> **OPEN QUESTION:** Slab pre-pour checklist — floor plan, drainage (slope + trench/floor drains), conduit runs, plumbing stub-ups, and anchor embeds must all be designed before the pour. This is a one-way door; it needs its own build doc.
> **OPEN QUESTION:** Power budget — size the PV array + battery against the Tier 1/2/3 loads and the worst-case cloudy stretch. How many days of autonomy do we design for?
> **OPEN QUESTION:** Custom structure engineering — a custom build still must meet local wind/hail/code. Do we need an engineer's stamp, and who carries that?
> **OPEN QUESTION:** Water autonomy — off-grid likely means off-water too. Can rainwater capture + storage carry irrigation *and* evaporative cooling through a dry summer, or do we need a tank/well?

*Next document: `10-requirements.md` — turning these principles into concrete, checkable requirements.*
