# BOM · Off-Grid Power (Solar + Battery)

*Solar array, battery bank, charge control, and DC/AC distribution for the fully off-grid greenhouse. Implements [REQ-PWR-*](../../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility).*

> **Status:** 🟡 Scaffolding. Quantities marked **TBD** are blocked on the **sizing calc** below, which needs the finalized load list from [controls](../../design/30-electronics-and-controls.md) + [network](../../design/40-network-and-connectivity.md).

---

## Sizing basis — *do this before buying anything*

The parts list falls out of three inputs:

### 1. The load list (per power tier)

| Tier | Loads | Continuous? | Watts | Wh/day |
|------|-------|-------------|-------|--------|
| **Tier 1** (survives — shed last) | Safety controller, temp sensing, **critical alert channel** (cellular/SMS), night irrigation | mostly continuous | TBD | TBD |
| **Tier 2** (cooling assist) | Exhaust/circulation fans, evap pump — *prefer solar-direct* | sun-correlated | TBD | TBD |
| **Tier 3** (sheds first) | Full HA host, access point, dashboards, grow lights, data logging | continuous-ish | TBD | TBD |

> Fill from the actual device specs. Network gear alone is ~15–25 W continuous ([net §3](../../design/40-network-and-connectivity.md#3-network-gear-is-a-continuous-off-grid-load--split-it-by-tier)).

### 2. Days of autonomy — *the key insight that shrinks the battery*

**We do NOT size the battery to run cooling through a multi-day cloudy stretch** — that battery would be enormous. Per the design philosophy, **the greenhouse survives a dead battery on passive cooling alone** ([REQ-COOL-2](../../design/10-requirements.md#b-cooling--ventilation--the-headline-system)). So the battery only has to keep **Tier 1** alive across a cloudy stretch.

- **Autonomy target (Tier 1 only):** TBD days *(recommend 2–3)* — see [open question](../../design/10-requirements.md#open-questions-feeding-back-into-design).
- Tier 2/3 run when there's sun/charge; they gracefully shed otherwise.

### 3. The math (fill in once loads are known)

```
Battery (usable Wh)  = Tier1 Wh/day  × autonomy days  ÷ depth-of-discharge
Array (W)            = (daily Wh to replace) ÷ (sun-hours × system efficiency)
                       sized to recharge AND carry daytime Tier 2/3 on a normal day
```
- Dallas average **~5 peak sun-hours/day** (less in a cloudy stretch — that's what autonomy covers).
- LiFePO₄ depth-of-discharge ~80–90%; system efficiency ~0.7–0.8.

> **Result → TBD:** Array __ W · Battery __ kWh. These set the quantities below.

---

## Line items

> Columns per the [BOM format](README.md#standard-format). Costs/quantities firm up after sizing + quotes.

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| PV modules | Mono panels; ground- or roof-mount TBD | TBD | REQ-PWR-1 | TBD | TBD | TBD | TBD | proposed | Tilt ~30–33° (year-round) or ~20° (summer-favored); unshaded — [site §orientation](../../design/20-site-and-orientation.md) |
| Mounting / racking | Wind-rated for Dallas; matches mount choice | TBD | REQ-PWR-1, REQ-STR-1 | TBD | TBD | TBD | TBD | proposed | Roof-mount adds structural load — see open Q |
| **All-in-one hybrid inverter** | **EG4 6000XP-class *or equal*** — bundles MPPT(s) + inverter/charger + controller; 48 V; AC-in for tether | 1 | REQ-PWR-1, REQ-PWR-13, REQ-PWR-15 | TBD | TBD | TBD | TBD | proposed | **Working direction (Option B)**; collapses the next 3 rows |
| **House bank (48 V)** | **LiFePO₄**, **~35% of total**; always present | TBD | REQ-PWR-2, REQ-PWR-8, REQ-PWR-11 | TBD | TBD | TBD | TBD | proposed | Carries Tier 1 + 2 critical loads on its own |
| **Power cow (48 V)** | **LiFePO₄** rack batteries, **~65% of total**; *isolated, charge-only* | TBD | REQ-PWR-1, REQ-PWR-8 | TBD | TBD | TBD | TBD | proposed | Tier-3 sub-panel + event power; **fire-code siting** ↓; never parallels house |
| **House→cow DC-DC charger** | One-way 48→48 V, **current-limited** (Orion-Tr *or equal*; size up for rate) | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | No inrush; gated to "house healthy"; *or* give cow its own MPPT |
| **Cow sub-panel + LVD** | Dedicated Tier-3 sub-panel; BatteryProtect / BMS low-voltage disconnect | 1 | REQ-PWR-12 | TBD | TBD | TBD | TBD | proposed | Live only when docked + above LVD |
| ~~EMS controller~~ | *Bundled into the 6000XP all-in-one* (working direction). Separate Cerbo only for a modular Victron build. | — | REQ-PWR-15 | — | — | — | — | folded | See all-in-one row above |
| ~~House inverter/charger~~ | *Bundled into the 6000XP all-in-one* (tether-in charging included). | — | REQ-PWR-13 | — | — | — | — | folded | See all-in-one row above |
| Load-shed relay | SOC-triggered contactor on Tier-2/3 branches (SmartShunt/BatteryProtect-driven) | TBD | REQ-PWR-3, REQ-PWR-4 | TBD | TBD | TBD | TBD | proposed | Option B's shedding (vs. GridBOSS smart ports) |
| Cow cart | Hand truck, rated for pack weight, securing straps, ramp | 1 | REQ-PWR-9 | TBD | TBD | TBD | TBD | proposed | 100s of lb loaded; Amber/Red move only |
| Cow portable inverter | For event AC (travels with the cow) | 1 | REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | Greenhouse stays DC-first; inverter is for events |
| Battery mgmt (BMS) | Per bank (house + cow); cow BMS does the LVD | TBD | REQ-PWR-2, REQ-PWR-12 | TBD | TBD | TBD | TBD | proposed | |
| Cow connectors | **Keyed, arc-safe** charge-in + load-out (Anderson SB class) | TBD | REQ-PWR-9, REQ-CTRL-1 | TBD | TBD | TBD | TBD | proposed | Separate one-way paths; terminal-protected in transit |
| House→cow DC-DC charger | Victron **Orion-Tr 48/48** *or equal*, ~8 A; input-V lockout | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | **Tier-① baseline** — always-on, current-limited, gated house-healthy |
| Routable PV string | One string sized to **cow MPPT max** (fits 6000XP MPPT-2 too) | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | **Tier-② manual boost** |
| PV-rated DC changeover | Rated to string Voc/Isc; **switch no-load** (not a marine selector) | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | HOUSE→MPPT-2 / COW→cow MPPT |
| Cow MPPT | Solar charge controller on the cow (sized to the routable string) | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | Receives the string in COW position |
| Cow PV connector | Keyed PV connector at the dock; live only in COW position | 1 | REQ-PWR-9 | TBD | TBD | TBD | TBD | proposed | Switch HOUSE before undock |
| DC distribution + fusing | Bus, fuses/breakers per tier | TBD | REQ-PWR-2..4 | TBD | TBD | TBD | TBD | proposed | **Tier-separated** so shedding T3 can't brown out T1 |
| DC disconnect(s) | PV + battery isolators | TBD | Safety | TBD | TBD | TBD | TBD | proposed | |
| Surge protection (SPD) | DC + comms SPD | 1+ | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | TX storm surge |
| Grounding / bonding | Rod, conductors, lugs | 1 set | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | |
| Wiring / connectors | PV wire, MC4, lugs | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | Conduit stub-ups pre-poured ([REQ-SLAB-3](../../design/10-requirements.md#a2-foundation--slab--the-one-way-door)) |
| Combiner box | If multiple strings | TBD | — | TBD | TBD | TBD | TBD | proposed | |
| Battery/electronics enclosure | Ventilated, lockable, weather/hail | 1 | REQ-PWR-6 | TBD | TBD | TBD | TBD | proposed | **Out of child reach**; thermal-managed ([REQ-CTRL-5](../../design/10-requirements.md#k-electronics--controls-architecture)) |
| System monitor / shunt | SOC + production telemetry | 1 | REQ-ELEC-4 | TBD | TBD | TBD | TBD | proposed | Feeds alerts + the data layer |
| Campus tether inlet | Weatherproof emergency power inlet + **hose bib w/ backflow preventer** | 1 | REQ-PWR-7, REQ-WATER-4 | TBD | TBD | TBD | TBD | proposed | **Emergency only**, temporary — not a permanent feed |

**Running subtotal:** TBD

> **Architecture:** see [`60-power-architecture.md`](../../design/60-power-architecture.md) for the three-layer model, the **isolated charge-only cow + sub-panel**, and the tether.

---

## Safety & code notes
- **LiFePO₄ on a school campus** brings fire-code / State Fire Marshal siting + ventilation considerations — coordinate via [`10-regulatory-governance.md`](../10-regulatory-governance.md) (fire overlay) and the sealed-design requirement.
- Battery + PV gear **secured, ventilated, out of child reach** ([REQ-PWR-6](../../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)).
- All of this is part of the **sealed architect/engineer design** for a public school building.

## Open questions
> **OPEN QUESTION:** Tier 1/2/3 load list — the numbers that drive the whole sizing. (Needs controls + network device specs.)
> **OPEN QUESTION:** Autonomy days for Tier 1 (recommend 2–3).
> **OPEN QUESTION:** Roof-mount vs. ground-mount array — affects structure, racking, and conduit.
> **OPEN QUESTION:** Any AC loads at all, or can we stay all-DC and skip the inverter?

*Upstream: [`10-requirements.md`](../../design/10-requirements.md) (REQ-PWR), [`30-electronics-and-controls.md`](../../design/30-electronics-and-controls.md), [`40-network-and-connectivity.md`](../../design/40-network-and-connectivity.md). Format: [`README.md`](README.md).*
