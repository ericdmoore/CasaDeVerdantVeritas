# Requirements

*Concrete, checkable requirements derived from the [design principles](00-design-principles.md). These turn "cooling is the headline system" into "the greenhouse shall maintain ≤ X °F on the design day." Every requirement traces back to a principle, so we can defend it later.*

---

## How to read this document

Each requirement has:

- **ID** — `REQ-<area>-<n>`, stable so other docs can cite it.
- **Priority** — **MUST** (non-negotiable / safety / code), **SHOULD** (strong preference, deviate only with a recorded reason), **MAY** (nice-to-have, phase-able).
- **Trace** — which design principle it serves.

> Numbers marked *(verify)* are engineering targets to confirm in detailed design with a local greenhouse supplier or engineer. They're defensible starting points, not sealed figures.

---

## A. Structure & envelope

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-STR-1 | MUST | Withstand local wind loads per Dallas/TX building code (design wind speed ~115 mph, *verify* current IBC/local amendment). | Safety |
| REQ-STR-2 | MUST | Glazing within child reach (below ~5 ft) shall be impact-resistant polycarbonate, not glass. | Safety, Dallas (hail) |
| REQ-STR-3 | SHOULD | Twin- or triple-wall polycarbonate glazing for light diffusion + insulation + hail resistance. | Dallas, Production |
| REQ-STR-4 | MUST | Anchored to a foundation rated for uplift; not a free-standing kit staked to soil. | Safety, Resilience |
| REQ-STR-5 | SHOULD | Clear interior footprint ≥ ~800 sq ft (e.g. 20×40) to hold a class of 20–25 plus growing zones. | Education |
| REQ-STR-6 | SHOULD | Roof pitch and gutters sized to shed Dallas downpours and feed rainwater capture. | Dallas, Affordability |

## B. Cooling & ventilation — *the headline system*

> The governing scenario is a ~100–105 °F summer afternoon with full sun. Design here, and the rest of the year is easy.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-COOL-1 | MUST | Maintain interior ≤ ~95 °F on the design day (105 °F ambient, full sun) with cooling active. *(verify target with crop needs.)* | Resilience, Production |
| REQ-COOL-2 | MUST | Mechanical exhaust capacity to achieve ≥ ~1 air change/min. Rule of thumb: CFM ≈ floor area × 8, then add factors for light/temp. For 800 sq ft → ~6,400 CFM baseline, size up toward ~8–12k for the Dallas design day. *(verify)* | Dallas, Resilience |
| REQ-COOL-3 | SHOULD | Evaporative (swamp) cooling — viable because TX summer humidity still leaves headroom. Pad area ≈ exhaust CFM ÷ ~250. *(verify pad type.)* | Dallas, Production |
| REQ-COOL-4 | MUST | **Passive failsafe ventilation** independent of power — e.g. wax-piston auto vent openers and/or large roll-up sides — that opens on rising temperature with no electricity. | Safety, Resilience |
| REQ-COOL-5 | MUST | On power or controller failure, powered vents/louvers **fail open**, never closed. | Safety, Resilience |
| REQ-COOL-6 | SHOULD | Cross-ventilation aligned to prevailing summer breeze (intake low, exhaust high/opposite). | Dallas |

## C. Shading & light

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-LIGHT-1 | SHOULD | Retractable or seasonal shade cloth, 30–50% shade, to cut summer solar load and admit winter light. | Dallas, Production |
| REQ-LIGHT-2 | MAY | Supplemental grow lighting for a germination/demo zone (winter day-length lessons). | Education, Production |

## D. Heating & freeze protection

> We do **not** heat all winter — we survive the handful of hard-freeze nights.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-HEAT-1 | MUST | Protect all water lines and reservoirs from freezing (heat tape, drain-down, or insulation). | Resilience, Affordability |
| REQ-HEAT-2 | SHOULD | Targeted frost protection (small heater or row cover) to hold ≥ ~38 °F around tender plants on freeze nights. *(verify)* | Production |
| REQ-HEAT-3 | SHOULD | Freeze event triggers a remote alert so a volunteer can act. | Resilience |

## E. Irrigation & water

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-WATER-1 | MUST | Automated irrigation (drip/recirculating) on a timer/controller — keeps plants alive over weekends and summer break. | Resilience |
| REQ-WATER-2 | MUST | Open water surfaces deeper than a few inches are covered or fenced. | Safety |
| REQ-WATER-3 | SHOULD | Rainwater harvesting from the roof, sized to offset a meaningful share of irrigation demand. *(verify capacity.)* | Dallas, Affordability, Education |
| REQ-WATER-4 | SHOULD | Backflow prevention on any municipal water connection (code). | Safety |

## F. Electrical & controls

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-ELEC-1 | MUST | All circuits GFCI-protected; wiring in conduit, connections out of child reach. | Safety |
| REQ-ELEC-2 | MUST | The critical safety loop (vent/exhaust on overtemp) operates without the data/automation layer — and has passive backup per REQ-COOL-4. | Safety, Resilience |
| REQ-ELEC-3 | SHOULD | Controller for temperature-driven ventilation and scheduled irrigation, using standard repairable components. | Resilience, Simplicity |
| REQ-ELEC-4 | SHOULD | Remote alerting (temp/moisture/power) to a phone. | Resilience |

## G. Safety & egress

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-SAFE-1 | MUST | Doors openable from inside without a key or tool at all times — **occupants can never be locked or trapped in.** | Safety |
| REQ-SAFE-2 | MUST | A clear, unobstructed exit path; door width and count per occupancy/code for a classroom-sized group. *(verify code.)* | Safety |
| REQ-SAFE-3 | MUST | No sharp edges, pinch points, or trip hazards at child height. | Safety |
| REQ-SAFE-4 | MUST | All materials, treatments, and amendments non-toxic / child-safe (no arsenic-treated lumber, no incompatible pesticides). | Safety |
| REQ-SAFE-5 | SHOULD | High-temperature alarm audible/visible before the space becomes dangerous. | Safety, Resilience |

## H. Accessibility & inclusion

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-ACC-1 | MUST | At least one accessible (ADA-compliant) entry and path of travel. | Accessibility |
| REQ-ACC-2 | SHOULD | At least one wheelchair-height work surface / raised bed with knee clearance. | Accessibility, Education |
| REQ-ACC-3 | SHOULD | One calm/sensory-friendly zone. | Accessibility, Education |

## I. Education & layout

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-EDU-1 | SHOULD | Distinct zones: in-ground/raised soil beds, a hydroponic demo, a germination station, and a data corner. | Education |
| REQ-EDU-2 | SHOULD | Work surfaces and controls reachable by a 2nd grader (~30 in counter height option). | Education, Safety |
| REQ-EDU-3 | SHOULD | Unobstructed sightlines so one adult can supervise the whole interior. | Safety, Education |
| REQ-EDU-4 | MAY | Key systems left visible and labeled (exposed water lines, clear reservoir, airflow indicators) as teaching aids. | Education |

## J. Data & monitoring — *the optional layer*

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-DATA-1 | SHOULD | Sensors (temp, humidity, soil moisture, light) logging to a student-accessible record. | Research |
| REQ-DATA-2 | MUST | The data layer is **not** in the critical safety/survival path — if it fails, plants and people are unaffected. | Safety, Simplicity |
| REQ-DATA-3 | MAY | Simple dashboard/export for classroom experiments. | Research, Education |

---

## Traceability check

Every **MUST** above maps to **Safety** or **Resilience** (the top of the priority hierarchy) or to **code** — as it should. Production and Showcase goals appear only as **SHOULD**/**MAY**. If you ever find a Production requirement marked MUST that overrides a Safety SHOULD, that's a smell — re-check it against [the priority order](00-design-principles.md#the-order-of-priorities).

---

## Open questions feeding back into design

> **OPEN QUESTION:** Confirm current Dallas wind-speed and snow/live-load figures with the AHJ (authority having jurisdiction) before fixing REQ-STR-1.
> **OPEN QUESTION:** Crop list drives REQ-COOL-1 and REQ-HEAT-2 targets — warm-season vs. cool-season changes the setpoints.
> **OPEN QUESTION:** Occupancy classification for the structure (is it an accessory building, an assembly space?) drives egress requirements REQ-SAFE-2.

*Related: [`docs/operate/00-operating-principles.md`](../operate/00-operating-principles.md) — how the building actually gets run once these requirements are met.*
