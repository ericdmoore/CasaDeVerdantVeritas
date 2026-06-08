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

| Part | Size | Stays/Moves | Job |
|------|------|-------------|-----|
| **House pack (Tier-1 reserve)** | **~35%** of total | Never leaves | Keeps the safety loop + alerting alive at all times — including while the cow is away. Sized to cover **Tier-1 autonomy on its own.** |
| **Mobile bulk pack ("power cow")** | **~65%** of total | Rolls out | The main storage (Tier 2/3) + event power. Rack 48 V LiFePO₄ on a hand truck. |

> Because the house pack stays, **"the battery left the building" is a non-event** — the greenhouse runs its safety loop on the house pack and falls back to passive cooling, exactly what the design already survives. The cow's absence costs comfort, not safety.
>
> **Constraint on the 35/65 split:** the house 35% must still meet the Tier-1 autonomy target on its own ([REQ-PWR-11](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)). Since Tier 1 is a tiny load, 35% is normally ample — *verify once the load list exists.*

## Battery coupling & SOC management

The hard part of a removable pack: **never hard-parallel two banks at mismatched SOC** (inrush, arcing, and uncontrolled draining of the reserve). Two things make it safe:

- **Physics on our side:** LiFePO₄'s **flat voltage curve** means two packs at mid-range SOC sit at nearly the same voltage → tame equalizing current. The danger is only a **deeply depleted** cow (steep low end).
- **A managed coupler, not a dumb busbar.** Default: a **pre-charge contactor** gated by the controller (soft-connect, then parallel) — fine for moderate gaps; a deeply depleted cow charges through the controlled path *first*. Upgrade: a **bidirectional DC-DC** (banks never hard-paralleled — max isolation/control, at efficiency + cost). *(Sub-decision, see open questions.)*
- **Plus a manual battery selector/isolator** (marine 1/2/BOTH/OFF style) as the **Amber override + maintenance/emergency layer** beneath the automation — governing **only the bulk pool**:
  - 🔴 **The Tier-1 safety feed is hardwired to the house pack, never behind the selector** — it can't be switched off.
  - **`BOTH` = combined capacity, engaged only when banks are SOC-matched** (or via pre-charge) — `BOTH` with a depleted cow is the inrush case.
  - Prefer a **dual on/off** type over make-before-break 1/2/BOTH, so House↔Cow never transits a paralleled state involuntarily.
  - Positions: **House** (run off the reserve), **Cow** (run off the cow), **BOTH** (full array, matched only), **OFF** (isolation).

### The SOC policy (the control rules)
1. **House reserve floor is sacred** — never discharged below it for anything but Tier 1.
2. **A depleted cow recharges from the SUN first** — solar surplus (after Tier 1 + live loads) tops the cow.
3. **House → cow transfer only when the house is high** (e.g., > 75–80%), and **rate-limited.**
4. **Combined-pool discharge** for Tier 2/3 down to the house floor; below it, shed cow + Tier 3.
5. **Pre-event top-up** from solar or the tether — **never** from the reserve.
6. **Block sub-freezing charging** — a cow back cold from a winter event warms before the BMS allows charge.

### Implementation — integrated energy-management system (EMS)

What we *need* is an integrated, well-documented, **locally-controllable** EMS that provides: per-bank SOC monitoring, coordinated charge control, an inverter/charger (for house AC + tether-in), and programmable automations for the SOC policy.

> **Platform NOT yet chosen.** **Victron is the common commodity exemplar** (and the easiest to illustrate with), but it's a candidate, not a decision — alternatives include **Sol-Ark, EG4, Schneider Conext, Outback**, or a **DIY BMS + controller** route. Pick during detailed design with the 🔴 Red system designer; validate the exact topology with a dealer (high-energy licensed work).

Mapping the roles to the Victron line purely as a *concrete illustration* ("or equal"):

| Role | Victron example (or equal) |
|------|----------------------------|
| System brain (Venus OS, **DVCC**, automations) | Cerbo GX (MK2) + GX Touch / VRM |
| Per-bank SOC monitor (×2) | SmartShunt |
| Solar charge control | SmartSolar MPPT |
| Inverter/charger — house AC + **tether-in** | MultiPlus-II (48 V) |
| Cow coupling | Orion XS DC-DC *or* BMS pre-charge contactor |

## The "power cow" 🐄 — mobile dual-use storage

Usually docked in the greenhouse (charging from PV, discharging to loads); wheels out to power school events — the **community/showcase mission helping fund the build**.

- **Form:** rack-mount 48 V LiFePO₄ on a hand truck, with a **portable inverter** for AC at events (travels with the cow; the greenhouse keeps its own MultiPlus-II). ([REQ-CTRL-6](10-requirements.md#k-electronics--controls-architecture) keeps the *greenhouse* DC-first.)
- **Docking:** keyed, **arc-safe high-current DC connectors** (load-break / pre-charge; Anderson SB / Powerpole class), terminal-protected in transit ([REQ-PWR-9](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)).
- **SOC discipline:** governed by the policy above — never strand the greenhouse; never drain the reserve into the cow.
- **Handling = Amber/Red only.** Rack batteries are 40–100+ lb each; a loaded truck is hundreds of pounds. Securing, ramps (the flush ADA slab threshold helps), tip-risk, lithium transport. **Never Green/students.**
- **Event code/risk:** a mobile lithium + inverter station at a school event likely needs district risk-management / fire sign-off; UL-listed components make that easy. Coordinate via [regulatory governance](../build/10-regulatory-governance.md).

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
- **It can run the house with a dead battery.** The tether is AC; an **inverter/charger** (e.g. a MultiPlus-II *or equal*) turns it into bus power — so plugging in **powers the greenhouse loads *and* recharges the pack** even if the house battery is flat ([REQ-PWR-13](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)). This is the bottom of the resilience stack working as intended.
- **Keep it temporary.** A *permanent* feed becomes licensed installed work (🔴 Red), changes the building's "serviced" status, and can drag in code/occupancy questions — so we deliberately don't.
- **Hose = cross-connection** → backflow preventer required ([REQ-WATER-4](10-requirements.md#e-irrigation--water)).
- Deploy steps live in the [summer-survival SOP](../operate/sops/SOP-03-summer-survival.md).

---

## Open questions

> **OPEN QUESTION:** **EMS platform — not chosen.** Victron vs. Sol-Ark / EG4 / Schneider / DIY BMS+controller. Decide with the 🔴 Red designer.
> **OPEN QUESTION:** **Coupler type** — pre-charge contactor (default, cheaper) vs. bidirectional DC-DC (max isolation).
> **OPEN QUESTION:** **Automated coupling vs. all-manual selector** — keep the automated EMS with the selector as override (recommended), or go selector + Amber discipline only (simpler/cheaper, less foolproof).
> **OPEN QUESTION:** Fixed house-pack autonomy — confirm 35% covers Tier-1 for the autonomy window once the load list exists.
> **OPEN QUESTION:** Event use policy + district risk-management/fire sign-off for the mobile lithium station.

*Parent: [`00-design-principles.md`](00-design-principles.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-PWR), [`../build/bom/off-grid-power.md`](../build/bom/off-grid-power.md). Related: [`50-passive-architecture.md`](50-passive-architecture.md) (layer 1).*
