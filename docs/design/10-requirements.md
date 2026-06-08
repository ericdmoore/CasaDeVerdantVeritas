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
| REQ-STR-1 | MUST | Withstand local wind loads per Dallas/TX building code (design wind speed ~115 mph, *verify* current IBC/local amendment). As a public school building this needs a **sealed architect/engineer design** — see [regulatory governance](../build/10-regulatory-governance.md). | Safety |
| REQ-STR-2 | MUST | Glazing within child reach (below ~5 ft) shall be impact-resistant polycarbonate, not glass. | Safety, Dallas (hail) |
| REQ-STR-3 | SHOULD | Twin- or triple-wall polycarbonate glazing for light diffusion + insulation + hail resistance. | Dallas, Production |
| REQ-STR-4 | MUST | Anchored to a foundation rated for uplift; not a free-standing kit staked to soil. | Safety, Resilience |
| REQ-STR-5 | SHOULD | Clear interior footprint ≥ ~800 sq ft (e.g. 20×40) to hold a class of 20–25 plus growing zones. | Education |
| REQ-STR-6 | SHOULD | Roof pitch and gutters sized to shed Dallas downpours and feed rainwater capture. | Dallas, Affordability |

## A2. Foundation & slab — *the one-way door*

> Everything here gets locked in concrete. Once the slab is poured, changes are demolition, not edits. These must all be finalized **before the pour** — see the forthcoming `docs/build/` pre-pour checklist.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-SLAB-1 | MUST | Floor plan (zones, beds, benches, paths) finalized before pour — slab features depend on it. | Education, all |
| REQ-SLAB-2 | MUST | Integrated drainage: slope to floor/trench drains with a daylight or French-drain outlet, formed before pour. A greenhouse floor is wet by design. | Safety, Resilience |
| REQ-SLAB-3 | MUST | Electrical conduit + stub-ups embedded for the control panel, fans, sensors, and the off-grid PV/battery feed. | Off-grid, Safety |
| REQ-SLAB-4 | MUST | Plumbing stub-ups for irrigation supply, rainwater line, and drains, placed per the floor plan. | Resilience |
| REQ-SLAB-5 | MUST | Anchor bolts / embeds set for the custom structure's base, per the wind-uplift design (ties to REQ-STR-1/4). | Safety |
| REQ-SLAB-6 | SHOULD | Perimeter edge insulation + vapor barrier under slab; design whether slab thermal mass is exposed to buffer day/night swings. | Resilience, Dallas |
| REQ-SLAB-7 | SHOULD | Slab finish flush and level for ADA access (ties to REQ-ACC-1). | Accessibility |

## B. Cooling & ventilation — *the headline system*

> The governing scenario is a ~100–105 °F summer afternoon with full sun. Design here, and the rest of the year is easy. **Because we're off-grid, a two-target rule applies:** the powered system holds the comfortable setpoint *when there's sun/battery*, but a **passive-only** layer must keep the greenhouse survivable when there isn't (the hot-and-cloudy stretch).

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-COOL-1 | MUST | **With powered assist available:** maintain interior ≤ ~95 °F on the design day (105 °F ambient, full sun). *(verify target with crop needs.)* | Resilience, Production |
| REQ-COOL-2 | MUST | **Passive-only survival (cloudy stretch / depleted battery):** shade + natural ventilation alone must hold the interior below the plant/people safety ceiling on the design day *(verify ceiling, ~110–115 °F)* and never trap heat. This is the off-grid worst case. | Safety, Resilience |
| REQ-COOL-3 | MUST | **Passive ventilation sized as the primary system:** combined roof + sidewall vent area ≥ ~20–25% of floor area, roof-vent area roughly equal to sidewall area to drive stack effect. *(verify)* | Dallas, Resilience |
| REQ-COOL-4 | MUST | **Passive failsafe openers** independent of power — wax-piston auto vent openers and/or large roll-up sides — opening on rising temperature with zero electricity. | Safety, Resilience |
| REQ-COOL-5 | SHOULD | **Powered exhaust as a solar-correlated assist:** prefer solar-direct DC fans that run off PV without draining the battery; size for ≥ ~1 air change/min when power is available (CFM ≈ floor area × 8 → ~6,400 CFM for 800 sq ft, up toward ~8–12k on the design day). *(verify)* | Off-grid, Dallas |
| REQ-COOL-6 | SHOULD | Evaporative (swamp) cooling as an assist — viable because TX summer humidity still leaves headroom; pad area ≈ exhaust CFM ÷ ~250. Note its **water draw** counts against the off-grid water budget. *(verify pad type.)* | Dallas, Production |
| REQ-COOL-7 | MUST | On power or controller failure, powered vents/louvers **fail open**, never closed. | Safety, Resilience |
| REQ-COOL-8 | SHOULD | Cross-ventilation aligned to prevailing summer breeze (intake low, exhaust high/opposite). | Dallas |

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
| REQ-WATER-5 | SHOULD | **Off-water autonomy:** rainwater storage sized to carry irrigation *and* evaporative-cooling demand through a dry summer stretch. Emergency backup source = **campus garden hose** (with backflow per REQ-WATER-4); a tank delivery is the fallback. *(verify storage sizing.)* | Off-grid, Resilience |

## F. Electrical & controls

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-ELEC-1 | MUST | All circuits GFCI-protected; wiring in conduit, connections out of child reach. | Safety |
| REQ-ELEC-2 | MUST | The critical safety loop (vent/exhaust on overtemp) operates without the data/automation layer — and has passive backup per REQ-COOL-4. | Safety, Resilience |
| REQ-ELEC-3 | SHOULD | Controller for temperature-driven ventilation and scheduled irrigation, using standard repairable components. | Resilience, Simplicity |
| REQ-ELEC-4 | SHOULD | Remote alerting (temp/moisture/power, plus battery state-of-charge) to a phone. | Resilience |

## F2. Off-grid energy — *solar + battery, no utility*

> No grid means "power loss" is a normal cloudy-week event, not a rare fault. Size and prioritize accordingly.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-PWR-1 | MUST | PV array + battery sized against the Tier 1/2/3 load list and a worst-case cloudy stretch; design days-of-autonomy target set explicitly. *(verify, see OQ.)* | Off-grid, Resilience |
| REQ-PWR-2 | MUST | **Tier 1 (shed last):** control brain, temp sensing, alerting, and night irrigation are battery-protected and survive a multi-day low-solar stretch. | Safety, Resilience |
| REQ-PWR-3 | SHOULD | **Tier 2:** cooling assist (fans, evap pump) prefers solar-direct operation; runs when sun/battery allow. | Off-grid, Dallas |
| REQ-PWR-4 | SHOULD | **Tier 3 (shed first):** grow lights, data logging, hydroponic pumps drop automatically on low battery state-of-charge. | Off-grid, Simplicity |
| REQ-PWR-5 | MUST | The greenhouse survives a fully depleted battery on passive means alone (ties to REQ-COOL-2). | Safety, Resilience |
| REQ-PWR-6 | SHOULD | PV/battery enclosure sited and secured out of child reach, ventilated, and weather/hail protected. | Safety |
| REQ-PWR-7 | SHOULD | **Emergency campus tether** (temporary extension cord + garden hose) as a last-resort backstop — *not* a dependency, kept temporary (permanent feed = licensed Red work). Hose needs backflow protection ([REQ-WATER-4](#e-irrigation--water)). | Resilience |
| REQ-PWR-8 | MUST | **Two independent banks:** a **house bank** (critical: Tier 1 + 2, always present) and an **isolated, charge-only "power cow"** (Tier-3 sub-panel + events). The cow **never parallels the house bus.** | Safety, Resilience |
| REQ-PWR-9 | SHOULD | Cow **charge-in and load-out** use **keyed, arc-safe connectors** (Anderson SB / Powerpole class), terminal-protected in transit; moved by Amber/Red only, never Green/students. | Safety |
| REQ-PWR-10 | MUST | **House → cow charging is one-way via a current-limited DC-DC charger** (no inrush at any SOC), **gated to run only when the house is healthy** so it never competes with critical loads. Block sub-freezing charging. | Safety, Resilience |
| REQ-PWR-11 | MUST | **House bank sized to carry its critical loads (Tier 1, + Tier 2 not covered solar-direct) for the autonomy window on its own** (~35% of total); cow capacity is independent/bonus. | Safety, Resilience |
| REQ-PWR-12 | MUST | **Cow → dedicated sub-panel, discharge-only**, live **only when docked AND above the cow's LVD**; de-energizes automatically when the cow leaves or runs low. | Safety, Resilience |
| REQ-PWR-13 | SHOULD | Campus tether can **power loads + recharge the house** via an AC→DC charger / inverter-charger (Layer-3, emergency/temporary). | Resilience |
| REQ-PWR-14 | MUST | **No DC coupling/paralleling of the two banks** — charge-in and load-out are separate one-way paths, eliminating inrush/back-feed by design (no coupler, selector, or combiner). | Safety, Resilience |
| REQ-PWR-15 | SHOULD | **Integrated, locally-controllable single-bank house EMS** (inverter/charger, MPPT, monitor, controller). *(Platform open — EG4 / Victron / Sol-Ark / DIY; single-bank = no multi-bank orchestration needed.)* | Resilience, Off-grid |

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
| REQ-DATA-2 | SHOULD | The data layer is **not** in the critical safety/survival path — if it fails, plants and people are unaffected. | Safety, Simplicity |
| REQ-DATA-3 | MAY | Simple dashboard/export for classroom experiments. | Research, Education |
| REQ-DATA-4 | SHOULD | The Data Layer should allow for class rooms to setup experiments and monitor them from the class room. (A Webcam, an automated lamp, a ruler in view, then watch timelapse/ AV artifacts of growth rate.) | Research, Simplicity |
| REQ-DATA-3 | MUST | Data Must be local-first, there can be a cloud-enabled observability / extension storage option too | Research, Simplicity |

## K. Electronics & controls architecture

> Derived from [`30-electronics-and-controls.md`](30-electronics-and-controls.md). Makes those sub-principles checkable.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-CTRL-1 | MUST | Connectors are **keyed and color-coded by function** so a wrong connection is physically impossible (power can't seat in data, 12 V can't seat in 5 V). | Safety, Simplicity |
| REQ-CTRL-2 | MUST | **Sealed connectors (e.g. M12 X-coded, IP67) on any run that crosses the wet/exposed environment;** commodity RJ45/PoE++ only inside controlled enclosures. Minimize exposed runs. | Resilience, Dallas |
| REQ-CTRL-3 | MUST | **Data and power separated at the core** (controller, critical-loop power, alerting); convergence (PoE++) allowed only at the edge. | Safety, Resilience |
| REQ-CTRL-4 | MUST | Electronics **serviceable without special access** — nothing critical buried/potted or needing a ladder + two people; optimize for low repair time. | Resilience |
| REQ-CTRL-5 | SHOULD | **Commodity hardware in a managed sealed enclosure** over rugged gear — *with* thermal siting (shade/cool, reflective), a breather/membrane vent + desiccant, and conformal-coated boards. | Simplicity, Affordability |
| REQ-CTRL-6 | SHOULD | **Low-voltage SELV DC (≤ ~48 V)** in wet and child-accessible zones; reserve line-voltage AC for where genuinely needed, away from hands and water. | Safety |
| REQ-CTRL-7 | SHOULD | **Surge protection (SPD) + proper ground** shielding the Tier 1 core (off-grid PV + TX storms). | Resilience, Off-grid |
| REQ-CTRL-8 | SHOULD | **Wiring conventions:** on any low-voltage DC pair the **marked conductor = positive (+)**; **Wago Lever-Nuts** for wire-to-wire splices (non-terminations), *not* the high-current bus. | Safety, Simplicity |

## L. Network & connectivity

> Derived from [`40-network-and-connectivity.md`](40-network-and-connectivity.md).

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-NET-1 | MUST | The safety loop (overtemp→vent, irrigation, alarm) runs with **Home Assistant, the LAN, and the internet all down**. HA is orchestration/observability, never the safety system. | Safety, Resilience |
| REQ-NET-2 | MUST | A **critical-alert channel** (e.g. low-power cellular/SMS from the safety controller) that survives independently of the full HA + access-point stack. | Safety, Resilience |
| REQ-NET-3 | MUST | **Network segmentation:** isolated IoT/control segment; guest (QR) segment is **read-only and cannot reach any actuator**. | Safety |
| REQ-NET-4 | MUST | **No inbound port-forwarding to HA.** Remote access via outbound tunnel only (Nabu Casa / Tailscale / WireGuard); no default credentials. | Safety |
| REQ-NET-5 | SHOULD | External uplink **sized to the alert path**, not the dashboard; full remote/dashboard traffic is Tier 3 sheddable. Recommended primary: **own LTE**. | Off-grid, Resilience |
| REQ-NET-6 | SHOULD | Self-recovery: **watchdog/auto power-cycle**, an **RTC** for off-grid timekeeping, and **SSD (not SD card)** for the HA host. | Resilience |
| REQ-NET-7 | SHOULD | **Per-node heartbeat / last-seen + a reachability diagnostic**, surfaced so an Amber volunteer can localize a fault post-escalation; alerts when a node drops off. This is what lets a Green SOS resolve without Green diagnosing. | Resilience |
| REQ-NET-8 | SHOULD | Transport = **as few as the physics needs, band-diverse, each earning its keep:** wired PoE backbone (wired-first) + one 2.4 GHz mesh (Zigbee, Thread-capable HW) + sub-GHz/LoRa for far/canopy nodes + WiFi for powered/bandwidth nodes. Guardrails: one transport per niche; each gateway a budgeted power line; spares + ≥2 Amber people per transport; one HA integration pattern. | Resilience, Simplicity |
| REQ-NET-9 | SHOULD | Visitor access via **two QR codes** (guest WiFi join + local dashboard URL, mDNS `greenhouse.local`); optional **public read-only dashboard** for showcase. | Education, Showcase |
| REQ-NET-10 | SHOULD | **Camera/data privacy:** any webcam points at plants not students, local-first, with a written data-governance note. | Safety, Education |

## M. Passive architecture

> Derived from [`50-passive-architecture.md`](50-passive-architecture.md). The zero-power survival layer.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-PASV-1 | MUST | The passive layer (shade + natural/stack ventilation + thermal mass) alone holds the interior below the survival ceiling with **zero electricity** (realizes [REQ-COOL-2](#b-cooling--ventilation--the-headline-system)). | Safety, Resilience |
| REQ-PASV-2 | SHOULD | **Solar chimney / thermal stack** for buoyancy-driven air turnover that scales with the heat load. | Resilience, Dallas |
| REQ-PASV-3 | SHOULD | **Fixed sun-tuned overhangs / awnings** (foolproof, no moving parts) as the shade baseline, plus adjustable louvers to fine-tune. | Resilience, Dallas |
| REQ-PASV-4 | SHOULD | **Gravity-fed irrigation** from an elevated rainwater header tank — waters with no pump / dead battery. | Resilience, Off-grid |
| REQ-PASV-5 | SHOULD | **Wicking beds / sub-irrigation** to buffer multiple untended days. | Resilience |
| REQ-PASV-6 | SHOULD | **Thermal mass** (slab + water containers) buffering heat and freeze; water mass doubles as irrigation store. | Resilience, Dallas |
| REQ-PASV-7 | SHOULD | **Manual override on every powered system** + gravity/counterweight fail-open vents. | Safety, Resilience |
| REQ-PASV-8 | SHOULD | **Deciduous / living shade** on the west/south for self-regulating seasonal shading. | Dallas, Education |
| REQ-PASV-9 | MAY | **Earth-tube intake** (chimney-driven) *only if* the humid-climate mold/condensation/radon risk is engineered out — else omit. | Resilience |

## N. Power architecture (off-grid system)

> Derived from [`60-power-architecture.md`](60-power-architecture.md). See also [REQ-PWR](#f2-off-grid-energy--solar--battery-no-utility). The mobile-battery and tether requirements live in REQ-PWR-7/8/9.

## O. Resource cycles (water + nutrient)

> Derived from [`70-resource-cycles.md`](70-resource-cycles.md). Closes the "produce no waste" gap.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-CYCLE-1 | SHOULD | **Multi-surface rainwater harvest** (greenhouse roof + PV array) with first-flush diverter + screening → cistern. | Off-grid, Education |
| REQ-CYCLE-2 | SHOULD | **Interior condensation capture** (twin-wall channels / eave gutters) to a separate **pure-water** store for evap pads, battery top-up, and sensitive hydroponics. | Resilience, Off-grid |
| REQ-CYCLE-3 | SHOULD | **Tiered, covered storage** ([REQ-WATER-2](#e-irrigation--water)) + an **elevated header tank** for gravity feed ([REQ-PASV-4](#m-passive-architecture)). | Resilience, Safety |
| REQ-CYCLE-4 | SHOULD | **Overflow routed to soil / swale / compost beds**, never to waste. | Off-grid, Education |
| REQ-CYCLE-5 | SHOULD | **Composting program** — vermicompost, bokashi, hot compost, hügelkultur — sited in an **outdoor service zone** (pests/pathogens out of the growing house); finished product returns inside. | Education, Production |
| REQ-CYCLE-6 | SHOULD | **Cafeteria-scrap loop** via **bokashi pre-treatment**; requires health-dept/district sign-off ([REQ-REG](../build/10-regulatory-governance.md)) and sealed, rodent-proof handling. | Education, Production |
| REQ-CYCLE-7 | SHOULD | **Fertigation path** — compost / worm tea into the irrigation system. | Production, Education |
| REQ-CYCLE-8 | MAY | **Hügelkultur beds** merging water storage + in-place composting (build-time). | Resilience, Production |
| REQ-CYCLE-9 | SHOULD | **LiFePO₄ end-of-life recycling plan** named (the hardware half of "produce no waste"). | Resilience |

## P. Zone layout

> Derived from [`80-zone-layout.md`](80-zone-layout.md). Realizes REQ-EDU / REQ-ACC / REQ-CTRL spatially.

| ID | Pri | Requirement | Trace |
|----|-----|-------------|-------|
| REQ-ZONE-1 | MUST | **Central ADA circulation spine** giving single-glance supervision of the whole interior. | Safety, Education |
| REQ-ZONE-2 | SHOULD | **Light gradient:** full-sun crops south, shade-tolerant + work zones north. | Production, Education |
| REQ-ZONE-3 | SHOULD | **Primary gathering on the covered outdoor pad** — keep a full class out of the interior to preserve Group U. | Safety, Education |
| REQ-ZONE-4 | SHOULD | **Controls + power infra in the cool/shaded corner, out of child reach.** | Safety, Resilience |
| REQ-ZONE-5 | SHOULD | **~8 growing/irrigation zones** (IZ1–8): balanced soil beds + a hydroponic demo + wicking beds. | Education, Production |

---

## Traceability check

Every **MUST** above maps to **Safety** or **Resilience** (the top of the priority hierarchy) or to **code** — as it should. *Off-grid* and *Dallas* appear as trace tags too: they're project constraints (the decided context), not goals that compete in the hierarchy — a MUST tagged `Off-grid` still earns its MUST from Safety or Resilience. Production and Showcase goals appear only as **SHOULD**/**MAY**. If you ever find a Production requirement marked MUST that overrides a Safety SHOULD, that's a smell — re-check it against [the priority order](00-design-principles.md#the-order-of-priorities).

---

## Open questions feeding back into design

> ⭐ **OPEN QUESTION (highest leverage):** Occupancy classification — accessory **Group U** greenhouse vs. **occupied instructional space (E/B)**. Decides egress (REQ-SAFE-2), fire requirements, and overall cost. See [regulatory governance](../build/10-regulatory-governance.md#-the-decision-that-governs-everything-occupancy-classification).
> ✅ **RESOLVED:** Sealed architect/engineer design **is required** — this is a public school building under 19 TAC §61.1040, which overrides the agricultural/small-building seal exemptions. *(2026-06-08; see [regulatory governance](../build/10-regulatory-governance.md).)*
> **OPEN QUESTION:** Confirm current Dallas wind-speed and snow/live-load figures + code edition/local amendments with the AHJ before fixing REQ-STR-1.
> **OPEN QUESTION:** Crop list drives REQ-COOL-1/2 and REQ-HEAT-2 targets — warm-season vs. cool-season changes both the comfortable setpoint and the survivable ceiling.
> **OPEN QUESTION:** Days-of-autonomy target for REQ-PWR-1 — how long a cloudy stretch must the battery carry Tier 1 loads?
> **OPEN QUESTION:** Water budget for REQ-WATER-5 — does rainwater storage cover irrigation + evaporative cooling through a dry summer, or do we need a backup source?

*Related: [`docs/operate/00-operating-principles.md`](../operate/00-operating-principles.md) — how the building actually gets run once these requirements are met.*
