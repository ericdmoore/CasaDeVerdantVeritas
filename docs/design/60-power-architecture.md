# Power Architecture — off-grid system

*How the greenhouse makes, stores, and rations electricity — the design narrative behind [REQ-PWR-*](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility) and the [off-grid power BOM](../build/bom/off-grid-power.md). Sub-domain of the [design principles](00-design-principles.md); tightly coupled to [electronics](30-electronics-and-controls.md), [network](40-network-and-connectivity.md), and [passive architecture](50-passive-architecture.md).*

---

## The three-layer resilience model

Power resilience is layered, and **each layer degrades gracefully into the next**:

```
1. PASSIVE  (always, zero electricity) ── solar chimney, shade, thermal mass, gravity irrigation
2. SOLAR + BATTERY (normal operation) ── PV array → battery → tiered loads
3. CAMPUS TETHER (emergency only) ─────── temporary extension cord + garden hose, extreme weather
```

The golden property: **the greenhouse survives the total loss of layers 2 and 3 on layer 1 alone** ([REQ-COOL-2](10-requirements.md#b-cooling--ventilation--the-headline-system), [REQ-PASV-1](10-requirements.md#m-passive-architecture)). Power is an assist, never the survival path.

## Layer 2 — solar + battery

- **PV array** sized to recharge the battery *and* carry daytime Tier 2/3 on a normal day (see [BOM sizing basis](../build/bom/off-grid-power.md#sizing-basis--do-this-before-buying-anything); orientation/tilt per [site](20-site-and-orientation.md)).
- **Tiered loads + load shedding** ([REQ-PWR-2..4](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)): **Tier 1** (control, sensing, critical alert, night irrigation) shed last; **Tier 2** (cooling assist, solar-direct preferred) rides the sun; **Tier 3** (HA, dashboards, lights) shed first on low state-of-charge.

### Two independent banks — house (critical) + isolated cow

The "power cow" is **safe by design because it's never electrically merged with the house.** Two separate banks, two separate jobs:

| Bank | Powers | Presence |
|------|--------|----------|
| **House bank** (~35% of total) | **Critical loads** — Tier 1 (safety / control / alert / night irrigation) + Tier 2 (cooling assist) | Always present |
| **Power cow** (~65% of total) | Its **own dedicated sub-panel** of Tier-3 circuits (hydro demo, grow lights, data rig, supplemental fans, event outlet) + event power | Docked or rolled out |

> The cow leaving is a **non-event**: its sub-panel simply de-energizes (those loads are Tier-3 by choice), the house bank carries all critical loads, and passive covers cooling. *Capacity isn't wasted — the cow's energy is allocated to loads that tolerate its absence.*
>
> Sizing: the **house bank must carry its critical loads for the autonomy window on its own** ([REQ-PWR-11](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)); the cow is independent. Verify the ~35/65 split against the load list.

## Cow integration — charge-only, isolated, own sub-panel

The cow is **never paralleled with the house bus.** Separate, one-directional paths — which is what makes it foolproof (no inrush, no back-feed, ever).

### Charging the cow — two tiers (decided 2026-06-09)

Both feed the **cow battery in parallel** (a standard "multiple chargers, one battery" setup — they don't fight; each regulates to its own setpoint and just adds current):

- **① Foolproof baseline — Orion DC-DC charger.** A one-way 48→48 V DC-DC charger (Victron Orion-Tr *or equal*, ~8 A / ~380 W) from the house bus → cow. **Automatic, current-limited (no inrush at any SOC), always running** whenever the house is healthy. Its **input-voltage lockout** is the gate: divert solar elsewhere and let the house dip, and the Orion **auto-pauses pulling from the house** — the house protects itself. Slow but bulletproof, zero human input.
- **② Manual enhancement — routable PV string.** One PV string (sized to the **cow MPPT's max**) on a **PV-rated DC changeover switch**: **HOUSE** position → the 6000XP's **MPPT-2** (boosts the house); **COW** position → the **cow's own MPPT** (fast solar refill). Operator-chosen, for when the cow comes back depleted.
  - **Switch no-load** (MPPTs off / at night) — PV DC arcs; use a PV-rated changeover, not a marine selector.
  - **On undock:** switch to **HOUSE first** (cow PV connector dead), *then* unplug. Default to **HOUSE** whenever the cow's away.
  - String Voc/Isc must fit **both** MPPT windows; **combined charge current (Orion + string) ≤ the cow BMS limit.**

- **Cow → sub-panel: discharge only.** The cow feeds a **dedicated cow-circuits sub-panel**, live **only when docked and above the cow's LVD** (its BMS). Two automatic protections: the **LVD** cuts the sub-panel when the cow runs low, and **physically unplugging** the cow de-energizes it.
- **No coupling device, no selector across the batteries, no combiner.** Charge-in and load-out are different terminals on different one-way paths; the two **batteries** never see each other. (The changeover switches the PV *source*, never the batteries.)
- **Block sub-freezing charging** — a cow back cold from a winter event warms before its BMS allows charge.

### EMS — now a single-bank choice
Because the house EMS only ever sees **one** bank (the cow is independent), there's **no multi-bank orchestration problem.** The house side needs an inverter/charger (house AC + tether-in), an MPPT, a battery monitor, and a controller — all of which an **all-in-one hybrid inverter bundles in one box.** **Working direction: an EG4 6000XP-class all-in-one** (greenhouse-scale; see [wiring concept Option B](../build/power-wiring-concept.md#option-b--eg4-6000xp-greenhouse-scale-simpler)). Confirm + size with the 🔴 Red designer.

## The "power cow" 🐄 — mobile dual-use storage

Docked, it charges from the house and runs its sub-panel; rolled out, it powers school events — the **community/showcase mission helping fund the build**.

- **Form:** rack-mount 48 V LiFePO₄ on a hand truck, with a **portable inverter** for event AC (travels with the cow; the greenhouse keeps its own inverter/charger). [REQ-CTRL-6](10-requirements.md#k-electronics--controls-architecture) keeps the *greenhouse* DC-first.
- **Connectors:** keyed, **arc-safe** charge-in and load-out connectors (Anderson SB / Powerpole class), terminal-protected in transit ([REQ-PWR-9](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)).
- **Handling = Amber/Red only.** 40–100+ lb per rack battery; a loaded truck is hundreds of pounds — securing, ramps (the flush ADA threshold helps), tip-risk, lithium transport. **Never Green/students.**
- **Event code/risk:** a mobile lithium + inverter station at a school event likely needs district risk-management / fire sign-off; UL-listed components make that easy. Coordinate via [regulatory governance](../build/10-regulatory-governance.md).

## Layer 3 — the campus tether (emergency only)

A **temporary** extension cord + garden hose from campus, for extreme weather ([REQ-PWR-7](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility), [REQ-WATER-5](10-requirements.md#e-irrigation--water)).

- **Emergency-only, explicitly not a dependency.** The design never assumes it's there.
- **It can run the house with a dead battery.** The tether is AC; an **inverter/charger** (e.g. a MultiPlus-II *or equal*) turns it into bus power — so plugging in **powers the greenhouse loads *and* recharges the pack** even if the house battery is flat ([REQ-PWR-13](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)). This is the bottom of the resilience stack working as intended.
- **Keep it temporary.** A *permanent* feed becomes licensed installed work (🔴 Red), changes the building's "serviced" status, and can drag in code/occupancy questions — so we deliberately don't.
- **Hose = cross-connection** → backflow preventer required ([REQ-WATER-4](10-requirements.md#e-irrigation--water)).
- Deploy steps live in the [summer-survival SOP](../operate/sops/SOP-03-summer-survival.md).

---

## Open questions

> **OPEN QUESTION:** Confirm + size **EG4 6000XP-class all-in-one** (working direction) with the 🔴 Red designer once the load list exists.
> ✅ **RESOLVED (2026-06-09):** Cow charging = **two tiers** — foolproof Orion DC-DC baseline (always-on, ~8 A) + a **manual routable PV string** (PV-rated changeover → 6000XP MPPT-2 *or* the cow MPPT). Both feed the cow battery in parallel; no fight. *(Final string sizing/changeover rating with the Red designer.)*
> **OPEN QUESTION:** House-bank autonomy — confirm the ~35% covers Tier 1 + needed Tier 2 for the autonomy window once the load list exists.
> **OPEN QUESTION:** Cow **sub-panel circuit list** + sizing (which Tier-3 loads live on it).
> **OPEN QUESTION:** Event use policy + district risk-management/fire sign-off for the mobile lithium station.

*Parent: [`00-design-principles.md`](00-design-principles.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-PWR), [`../build/bom/off-grid-power.md`](../build/bom/off-grid-power.md). Related: [`50-passive-architecture.md`](50-passive-architecture.md) (layer 1).*
