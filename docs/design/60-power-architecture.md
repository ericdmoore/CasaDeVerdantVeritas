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

### The battery is split: fixed reserve + mobile bulk

This is the architectural heart, and it makes the "power cow" *safe by design*:

| Part | Stays/Moves | Job |
|------|-------------|-----|
| **Fixed Tier-1 reserve** | Never leaves | Keeps the safety loop + alerting alive at all times — including while the cow is away. Small. |
| **Mobile bulk pack ("power cow")** | Rolls out | The main storage (Tier 2/3). Rack batteries + inverter on a hand truck; dual-use as event power. |

> Because the reserve stays, **"the battery left the building" is a non-event** — the greenhouse runs its safety loop on the reserve and falls back to passive cooling, exactly what the design already survives. The cow's absence costs comfort, not safety.

## The "power cow" 🐄 — mobile dual-use storage

Usually docked in the greenhouse (charging from PV, discharging to loads); wheels out to power school events — the **community/showcase mission helping fund the build**.

- **Form:** rack-mount LiFePO₄ batteries strapped to a hand truck, with an inverter for AC at events. ([REQ-CTRL-6](10-requirements.md#k-electronics--controls-architecture) keeps the *greenhouse* DC-first; the cow's inverter is for event AC.)
- **Docking:** keyed, **arc-safe high-current DC connectors** (load-break / pre-charge; Anderson SB / Powerpole class), terminal-protected in transit ([REQ-PWR-9](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)).
- **SOC discipline:** an event must not strand the greenhouse — charge from PV when docked, and the cow can be topped from the campus tether *before* an event. Never draw the fixed reserve into the cow.
- **Handling = Amber/Red only.** Rack batteries are 40–100+ lb each; a loaded truck is hundreds of pounds. Securing, ramps (the flush ADA slab threshold helps), tip-risk, lithium transport. **Never Green/students.**
- **Event code/risk:** a mobile lithium + inverter station at a school event likely needs district risk-management / fire sign-off; UL-listed components make that easy. Coordinate via [regulatory governance](../build/10-regulatory-governance.md).

## Layer 3 — the campus tether (emergency only)

A **temporary** extension cord + garden hose from campus, for extreme weather ([REQ-PWR-7](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility), [REQ-WATER-5](10-requirements.md#e-irrigation--water)).

- **Emergency-only, explicitly not a dependency.** The design never assumes it's there.
- **Keep it temporary.** A *permanent* feed becomes licensed installed work (🔴 Red), changes the building's "serviced" status, and can drag in code/occupancy questions — so we deliberately don't.
- **Hose = cross-connection** → backflow preventer required ([REQ-WATER-4](10-requirements.md#e-irrigation--water)).
- Deploy steps live in the [summer-survival SOP](../operate/sops/SOP-03-summer-survival.md).

---

## Open questions

> **OPEN QUESTION:** Fixed Tier-1 reserve size — how many days of autonomy for the safety/alert loop alone (ties [REQ-PWR-1](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility); recommend 2–3).
> **OPEN QUESTION:** Cow capacity + inverter rating — driven by both greenhouse bulk storage *and* the event loads it's meant to support.
> **OPEN QUESTION:** Docking connector standard + charge topology (does the cow charge through the same MPPT, or its own?).
> **OPEN QUESTION:** Event use policy + district risk-management/fire sign-off for the mobile lithium station.

*Parent: [`00-design-principles.md`](00-design-principles.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-PWR), [`../build/bom/off-grid-power.md`](../build/bom/off-grid-power.md). Related: [`50-passive-architecture.md`](50-passive-architecture.md) (layer 1).*
