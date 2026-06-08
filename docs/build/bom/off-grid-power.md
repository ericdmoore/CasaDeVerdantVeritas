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
| Charge controller | MPPT, sized to array V/I | TBD | REQ-PWR-1 | TBD | TBD | TBD | TBD | proposed | |
| **Fixed Tier-1 reserve 48v battery** | **LiFePO₄**, **~35% of total**; *never leaves* | TBD | REQ-PWR-2, REQ-PWR-8, REQ-PWR-11 | TBD | TBD | TBD | TBD | proposed | Sized for Tier-1 autonomy alone; alive when cow is away |
| **Mobile 48v ("power cow")** | **LiFePO₄** rack batteries, **~65% of total** | TBD | REQ-PWR-1, REQ-PWR-8 | TBD | TBD | TBD | TBD | proposed | Tier 2/3 storage + event power; **fire-code siting** ↓ |
| Bank coupler | Pre-charge contactor (default) **or** bidirectional DC-DC (e.g. Orion XS *or equal*) | 1 | REQ-PWR-10 | TBD | TBD | TBD | TBD | proposed | Never hard-parallel at mismatched SOC |
| Battery selector / isolator | Marine-style; **dual on/off** preferred; bulk pool only | 1 | REQ-PWR-14 | TBD | TBD | TBD | TBD | proposed | Tier-1 feed NOT behind it; BOTH only when matched |
| Energy-management system | Integrated EMS: per-bank SOC, DVCC-style control, automations (e.g. **Victron Cerbo GX *or equal*** — Sol-Ark/EG4/Schneider/DIY) | 1 | REQ-PWR-15, REQ-PWR-12 | TBD | TBD | TBD | TBD | proposed | **Platform open** |
| House inverter/charger | For house AC + **tether-in** charging (e.g. MultiPlus-II 48 V *or equal*) | 1 | REQ-PWR-13 | TBD | TBD | TBD | TBD | proposed | Bidirectional; runs house off tether w/ dead battery |
| Cow cart | Hand truck, rated for pack weight, securing straps, ramp | 1 | REQ-PWR-9 | TBD | TBD | TBD | TBD | proposed | 100s of lb loaded; Amber/Red move only |
| Cow inverter | For event AC (rated to event loads) | 1 | REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | Greenhouse stays DC-first; inverter is for events |
| Battery mgmt (BMS) | Per pack (reserve + cow) | TBD | REQ-PWR-2 | TBD | TBD | TBD | TBD | proposed | |
| Cow dock connectors | **Keyed, arc-safe high-current DC** (load-break/pre-charge, Anderson SB class) | TBD | REQ-PWR-9, REQ-CTRL-1 | TBD | TBD | TBD | TBD | proposed | Terminal-protected in transit |
| DC distribution + fusing | Bus, fuses/breakers per tier | TBD | REQ-PWR-2..4 | TBD | TBD | TBD | TBD | proposed | **Tier-separated** so shedding T3 can't brown out T1 |
| Load-shed controller | Battery-SOC-based tier shedding | TBD | REQ-PWR-3, REQ-PWR-4 | TBD | TBD | TBD | TBD | proposed | |
| DC disconnect(s) | PV + battery isolators | TBD | Safety | TBD | TBD | TBD | TBD | proposed | |
| Surge protection (SPD) | DC + comms SPD | 1+ | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | TX storm surge |
| Grounding / bonding | Rod, conductors, lugs | 1 set | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | |
| Wiring / connectors | PV wire, MC4, lugs | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | Conduit stub-ups pre-poured ([REQ-SLAB-3](../../design/10-requirements.md#a2-foundation--slab--the-one-way-door)) |
| Combiner box | If multiple strings | TBD | — | TBD | TBD | TBD | TBD | proposed | |
| Battery/electronics enclosure | Ventilated, lockable, weather/hail | 1 | REQ-PWR-6 | TBD | TBD | TBD | TBD | proposed | **Out of child reach**; thermal-managed ([REQ-CTRL-5](../../design/10-requirements.md#k-electronics--controls-architecture)) |
| System monitor / shunt | SOC + production telemetry | 1 | REQ-ELEC-4 | TBD | TBD | TBD | TBD | proposed | Feeds alerts + the data layer |
| Campus tether inlet | Weatherproof emergency power inlet + **hose bib w/ backflow preventer** | 1 | REQ-PWR-7, REQ-WATER-4 | TBD | TBD | TBD | TBD | proposed | **Emergency only**, temporary — not a permanent feed |

**Running subtotal:** TBD

> **Architecture:** see [`60-power-architecture.md`](../../design/60-power-architecture.md) for the three-layer model, the reserve/cow split, and the tether.

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
