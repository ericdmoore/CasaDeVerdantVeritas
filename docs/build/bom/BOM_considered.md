# BOM · Products Considered (controls, irrigation drivers, hydro, charge control)

*A decision log for the electronics and charge-control choices — every product or approach we looked at, whether it survived, and **why**. The per-subsystem BOMs ([controls](controls.md), [irrigation](irrigation.md), [off-grid power](off-grid-power.md)) carry only what's **Selected**; this file keeps the reasoning so the next volunteer doesn't re-litigate a closed question or re-buy a rejected part.*

> **Status:** 🟡 Living. Entries dated 2026-09-01 unless noted. Add a row when you evaluate something; never delete a `Disregarded` row — the rationale is the point.

---

## Legend

| Status | Meaning |
|--------|---------|
| **Selected** | Recommended working direction. Feeds a row in the subsystem BOM, where it stays `proposed` until the 🔴 Red designer approves. |
| **Pending** | Viable; decision blocked on a named dependency (sizing, availability, a sibling decision). |
| **Disregarded** | Ruled out for *this* build. The rationale says why — often it's a fine product that's wrong for our architecture. |

**Open?** — 🟢 open hardware (design files published under an open license) · 🟡 closed hardware, open/documented protocol or open firmware · 🔴 closed. Per [Design Principle 5](../../design/00-design-principles.md), open + commodity is preferred but **listed/stamped** wins wherever the fire-marshal or sealed-design path touches the part.

**Recurring decisions this log honors** (already made upstream — don't reopen here):
- **DC-latching irrigation valves** on a 48 V DC rail, stepped down at point of load ([irrigation BOM](irrigation.md), [controls BOM](controls.md)).
- **Tier 1 safety loop runs on-device**, HA is sheddable Tier 3 ([REQ-NET-1](../../design/10-requirements.md#l-network--connectivity), [REQ-ELEC-2](../../design/10-requirements.md#f-electrical--controls)).
- **Both battery banks are 48 V LiFePO₄**, never paralleled; EG4 6000XP-class all-in-one is the house working direction ([power architecture](../../design/60-power-architecture.md)).

---

## 1. Irrigation valve control — brain

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **Olimex ESP32-POE-ISO** *or equal* | Irrigation / actuation node MCU | 🟢 OSHWA-certified, KiCad published | **Selected** | ESP32 + galvanically isolated PoE Ethernet lands exactly on the 48 V / PoE++ point-of-load topology; ESPHome supports it natively; commodity price. | [controls §A](controls.md#a-compute--core) safety controller |
| **Controllino MAXI** | Tier-1 safety controller (micro-PLC form) | 🟢 open-source Arduino PLC | **Pending** | Answers the "hardened micro-PLC vs ESP32" open question the *other* way: DIN rail, native 24 V DC industrial I/O, relay + high-side outputs. Choose if Tier 1 must look like a PLC to the stamping engineer. Blocked on: Red designer's view of ESPHome as a life-safety controller. | [controls §A](controls.md#a-compute--core) |
| **OpenSprinkler (AC, triac outputs)** | Turnkey sprinkler controller | 🟢 firmware GPL; hardware files published | **Disregarded** | Drives 24 VAC always-energized solenoids via triacs — cannot pulse a DC-latching valve. Brings its own scheduler, duplicating the Tier-1/Tier-3 split. **Keep as the reference design** for valve current-sensing and the HA integration pattern (`hass-opensprinkler`). | — |
| **OpenSprinkler DC / Latch variant** | Turnkey latching-valve controller | 🟢 | **Pending** | If a current latching-solenoid variant is shipping, it's a shortcut for the H-bridge + cap bank. Still duplicates the scheduler. Blocked on: verify availability + latching support before designing around it. | — |
| **KinCony KC868-A8 / A16** | ESP32 DIN-rail relay board | 🟡 schematics published, ESPHome configs | **Disregarded** *(for valves)* | Relays are the wrong actuator for latching solenoids (need polarity reversal). May resurface for **load-shed relays** — evaluate separately. | — |
| **Sequent Microsystems relay HATs** | Raspberry-Pi stackable relays | 🟡 drivers + docs on GitHub | **Disregarded** | Ties valve actuation to a Pi — and the Pi/mini-PC is the *sheddable* Tier-3 host. Violates REQ-NET-1. Relays also wrong actuator (above). | — |
| **Sonoff 4CH / generic SPST relay boards** | Valve switching | 🟡 | **Disregarded** | An SPST contact cannot generate the reversed-polarity pulse a latching solenoid needs. Would work only if we abandoned latching valves — which we won't (off-grid holding current). | — |

## 2. Irrigation valve control — drivers

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **DRV8871 H-bridge, one per zone** *or equal* | Latching-solenoid pulse driver | 🟡 commodity IC, reference boards open | **Selected** | 6.5–45 V, 3.6 A, two GPIO for direction — fires the ~30–50 ms ±pulse at 12–24 V. Per-zone chips = a failure kills *one* zone and the swap is one module ([design principle 4](../../design/30-electronics-and-controls.md)). ~6 drip zones + IZ7 fill keeps count sane. | [controls §C](controls.md#c-actuation-control-side) "Irrigation valve drivers" |
| Shared cap bank, ~4700 µF @ 24 V | Pulse energy store | — | **Selected** | One bank feeds all zones; **firmware enforces one valve per pulse**. Sized so a single pulse doesn't collapse it (also what makes the ΔV sensing method work — §3). | same row |
| Shared H-bridge + per-zone select relays | Commercial 2-wire pattern | — | **Disregarded** | Fewer parts, but a stuck select relay opens the *wrong* valve, and the fault is invisible until the bed floods. Per-zone bridges fail safer. | — |
| **L298N** | Classic H-bridge | 🟡 | **Disregarded** | Functionally fine for 50 ms pulses; ~2 V dropout and dated. DRV8871 is cleaner at the same price. | — |
| TB6612FNG / DRV8833 | Dual H-bridge | 🟡 | **Disregarded** | Voltage ceiling too low for a 24 V pulse. | — |

## 3. Irrigation — software layer

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **ESPHome `sprinkler` component** | On-device zone sequencing + run timing | 🟢 | **Selected** | Zones, per-zone durations, sequencing, repeat, multiplier — all run on the ESP32. If Wi-Fi/HA/LAN dies mid-run the valve still closes. **This is REQ-NET-1 in firmware.** Wrinkle to document: it drives `switch` entities, so each zone is a **template switch that fires the H-bridge pulse** rather than holding a coil. | Tier 1 |
| **HA `irrigation_unlimited` (HACS)** | Program layer: start time + zone sequence + run times, rain delay, seasonal adjust | 🟢 | **Selected** | Models exactly the "schedule = start time + relay sequence + run times" structure. Lives on the sheddable Tier-3 host; loses nothing critical when shed. | Tier 3 |
| OpenSprinkler firmware scheduler | Turnkey scheduler | 🟢 | **Disregarded** | See §1 — duplicates the split. | — |

## 4. Irrigation — "did the valve fire / did water move?"

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **Cap-bank ΔV across the pulse** | Solenoid-integrity check | — (method) | **Selected** | `Q = C·ΔV`. Open coil / cut wire → almost no droop; shorted coil → deep fast collapse; healthy → a repeatable per-zone signature, baselined once, alarmed on drift. **Zero added parts** — one ADC channel already on the node. | [controls §C](controls.md#c-actuation-control-side) |
| **INA226 on the valve common return** | Pulse current in engineering units | 🟡 commodity IC | **Selected** *(optional add)* | Conversion time 140–588 µs with averaging off gives tens of samples inside a 50 ms pulse. One valve fires at a time → one chip covers every zone. **Already in the BOM** ([controls §C](controls.md#c-actuation-control-side) metering row) → rides the spares shelf. | same |
| Shunt → op-amp → diode/cap peak-hold → slow ADC | Analog pulse capture | — | **Pending** | Most robust and the easiest for a volunteer to scope, but more analog parts. Fallback if ΔV proves too noisy on the real cap bank. | — |
| **ACS712 / ACS724 Hall sensor** | Current sense | 🟡 | **Disregarded** | 185 mV/A is too coarse for a ~300 mA, 50 ms pulse; offset drift swamps the signal. | — |
| ZMCT103C CT, ATM90E32 / CircuitSetup, PZEM-004T | AC current / energy metering | 🟢/🟡 | **Disregarded** | AC instruments. Our valve side is DC-pulsed. (PZEM also needs ≥ 80 VAC.) | — |
| **Tank-level Δ over a run** | Flow proxy — "did water leave?" | — (method) | **Selected** | Level drop × tank cross-section = gallons delivered, at **zero pressure**, using the **tank level sensors already in the BOM**. Independent of coil current → two instruments, one added part. | [irrigation §B](irrigation.md#b-storage) level sensors |
| **YF-S201-class hall paddle flow meter** | Per-zone flow | 🟡 | **Disregarded** | Needs more pressure than a gravity header (~0.43 psi/ft; a 10 ft tower ≈ 4.3 psi) provides. Reads zero when water is actually flowing. | — |
| Low-flow pulse meter (positive-displacement or low-head turbine) | Per-zone flow | 🟡 | **Pending** | Only if per-zone gallons are wanted beyond the tank-Δ method. Blocked on: header elevation (sets available head) — a construction-locked open question. | — |

## 5. Hydroponics (IZ6) — pump control & sensing

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **Low-side logic-level MOSFET switch** + flyback diode + RC snubber *or equal* | DC pump on/off | 🟡 commodity | **Selected** | DC has no zero-crossing to quench an arc; a contact rated 10 A/250 VAC is often ≤ 30 VDC and derates hard at 24 V. Contacts **weld closed** — a hydro pump welded *on* is a flood. MOSFET has no contact to weld. | [controls §C](controls.md#c-actuation-control-side) "Evap-cooling pump driver" pattern → add hydro pump row |
| **Mechanical relay in front of the pump** | DC pump on/off | — | **Disregarded** | Above. The one the question started with; the reason it's wrong is worth keeping in the log. | — |
| DC-rated SSR | DC pump on/off | 🟡 | **Pending** | Acceptable, costlier; choose if volunteers prefer a DIN-rail module over a bare MOSFET board. | — |
| **Brushless pump with PWM/analog speed input** | Speed control, not just on/off | — | **Pending** | Blocked on the pump selection in the irrigation BOM. Buys flow tuning + soft start. | [irrigation §C](irrigation.md#c-pumps--pressure) |
| **INA226 on the pump feed** | Dry-run / clog / airlock / bearing-drift / Wh telemetry | 🟡 | **Selected** | Steady-state DC — the *good* case for current sensing. Current drop = dry run or airlock; spike toward stall = clog; months-long drift = bearings. Wh/cycle feeds the off-grid budget ([REQ-ELEC-4](../../design/10-requirements.md#f-electrical--controls)). Same part as §4. | [controls §C](controls.md#c-actuation-control-side) metering |
| **Low-level float switch wired in series with pump power** | Stuck-*off* / dry-run hardware interlock | — | **Selected** | Works with the controller dead. Pair with a reservoir sized so static solution buys a **day**, not an hour, in a Dallas greenhouse. | controls + irrigation |
| **Overflow standpipe back to reservoir**, sized > pump output | Stuck-*on* failsafe | — (plumbing) | **Selected** | Same "water line set by the standpipe, not by fill volume" pattern as the wicking beds ([REQ-CYCLE-14](../../design/10-requirements.md#o-resource-cycles)). One vocabulary across the building. | [irrigation §D](irrigation.md#d-distribution) |
| **DFRobot Gravity EC + pH probes on ADS1115** *or equal* | Hydro water chemistry | 🟡 commodity, well-documented | **Selected** *(start here)* | Fits "commodity a volunteer can replace" ([REQ-ELEC-3](../../design/10-requirements.md#f-electrical--controls)). Costs stability + calibration discipline. | [controls §B](controls.md#b-sensing) "Hydroponic EC / pH" |
| **Atlas Scientific EZO** | Hydro water chemistry | 🟡 documented I²C/UART | **Pending** | The better *instrument*; the worse *fit* for a rotating crew. Upgrade path if Gravity proves too noisy to teach from ([REQ-EDU-1](../../design/10-requirements.md)). | same |

## 6. Solar charge control (MPPT), BMS, chemistry

| Product / approach | Role | Open? | Status | Rationale | Feeds |
|--------------------|------|-------|--------|-----------|-------|
| **EG4 6000XP-class all-in-one** *or equal* | House bank MPPT + inverter/charger | 🔴 (closed-loop BMS comms, Pylontech protocol) | **Selected** *(existing working direction)* | Already decided in [power architecture](../../design/60-power-architecture.md). Charge behavior configured **via the battery's BMS** over CAN, not by hand in the charger. Two built-in MPPTs = "stackable at a granularity of two"; units parallel as the coarser step. | [power BOM](off-grid-power.md) |
| **Victron SmartSolar MPPT** *or equal* | **Cow MPPT** (open line item) | 🟡 VE.Direct documented; **Venus OS is GPL** | **Selected** | Expert mode: user-defined absorption/float V, absorption time + tail current, equalize on/off/V/interval, temp-comp coefficient, low-temp cutoff, re-bulk offset, saved presets. DVCC lets a CAN BMS drive it. Cow already carries a Victron Orion → one app, one VE.Direct → ESPHome telemetry path. UL-listed models exist for the fire sign-off. | [power BOM](off-grid-power.md) "Cow MPPT" |
| Victron Venus OS on a Raspberry Pi (GX role) → MQTT → HA | Telemetry / DVCC coordinator | 🟢 GPL software on commodity hardware | **Pending** | Only needed if the cow grows to multiple Victron devices needing DVCC. Otherwise ESPHome's `victron` external component reading VE.Direct is simpler. | — |
| **Libre Solar MPPT 2420 HC** | **Teaching-bench** MPPT (multi-chemistry demo) | 🟢 CERN-OHL hardware (KiCad), Zephyr firmware, ThingSet over CAN/serial | **Selected** *(bench only)* | The one serious open-hardware MPPT. Firmware carries `FLOODED / AGM / GEL / LFP / NMC / NMC_HV` types with set points exposed over ThingSet — the configurable-behavior ask, in the open. **80 V PV in, 20 A, 24 V-class (~500 W)** → not a 48 V bank charger. | new **Education bench** rows, [controls](controls.md) / [REQ-EDU](../../design/10-requirements.md) |
| Libre Solar MPPT 1210 HUS | Smaller bench MPPT (12 V / 10 A, USB out) | 🟢 | **Pending** | Cheaper bench alternative if the demo battery is 12 V-only. | — |
| **Libre Solar BMS C1** | Open 16S BMS (48 V LFP), CAN | 🟢 | **Pending** | Open place for "configurable charge behavior" at 48 V — the BMS publishes CVL/CCL and a closed charger obeys. **Teaching artifact, not the listed bank's safety device** (school lithium bank stays on a listed rack battery + its own BMS). | bench |
| **diyBMS v4** | Open 16S BMS, ESP32, MQTT → HA, Pylontech-CAN emulation | 🟢 | **Pending** | Same role as BMS C1 with a larger install base and direct HA MQTT. Same listing caveat. | bench |
| DIY ESP32 MPPT (TechBuilder / ASCAS v3 class) | Demo MPPT | 🟢 GitHub | **Disregarded** | Great classroom demo of the MPPT sweep; hobby-grade (no isolation, no listing, protection is firmware). Libre Solar covers the demo role with real engineering. | — |
| **EPEver Tracer AN/BN** | MPPT | 🟡 Modbus RTU, "User" battery type fully writable | **Disregarded** | Cheap and HA-friendly via RS485, but a quality tier below Victron and buys nothing the cow's Victron ecosystem doesn't already give. | — |
| Renogy Rover | MPPT | 🔴 BT-centric | **Disregarded** | Closed, weaker protocol, no advantage. | — |
| **NMC chemistry (any pack)** | Battery | — | **Disregarded** *(for the building)* | Thermal-runaway threshold far below LFP; reclaimed EV modules on a school campus is a fire-marshal conversation. LFP-only stands ([REQ-PWR-8](../../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility), [REQ-PWR-6](../../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)). Bench only, small cells, BMS with temp cutoff. | — |
| **Keyed Anderson Powerpole per chemistry** (housing color + stack arrangement), profile bound to the key | Bench poka-yoke | — | **Selected** *(bench)* | A Gel profile physically cannot reach an NMC pack; an FLA equalize cannot reach a Gel pack. [REQ-CTRL-1](../../design/10-requirements.md#k-electronics--controls-architecture) applied to electrochemistry. | bench |

### 6a. What an MPPT configures — and what it doesn't

The charger sets the **ceiling**: bulk current limit, absorption voltage + duration/tail current, float voltage, equalization (lead only), re-bulk offset, temperature compensation (lead), low-temp charge inhibit (lithium). The **floor** ("low-voltage allowance") is a *discharge*-side setting: on a 48 V system the loads don't pass through the MPPT, so the floor lives in the **BMS** (lithium) or a separate **LVD** (lead — the BatteryProtect already in the power BOM). Our tiered load shedding *is* the graduated floor; for LFP set the system LVD well above the BMS's ~2.5–2.8 V/cell (~51–52 V at the pack) so the BMS trip is the backstop, not the daily event.

Typical 48 V-nominal windows (the pack datasheet always wins):

| Chemistry | Absorb / charge | Float | Equalize | Temp comp | Special |
|-----------|-----------------|-------|----------|-----------|---------|
| FLA (24 cells) | ~57.6–59.2 V | ~54–55 V | ~62 V+, periodic | −3 to −5 mV/°C/cell | gassing → ventilation |
| Gel (24 cells) | ~56.4–57.6 V | ~54.4–55 V | **never** | required | equalize kills gel |
| LFP 16S | 55.2–57.6 V (3.45–3.6/cell) | ~53.6–54.4 or none | never | none | inhibit < 0–5 °C; derate > 45 °C |
| NMC 13S | 54.6 V max (4.2/cell) | none | never | none | 14S = 58.8 V — same "48 V" label, 4 V different ceiling |

---

## 7. Modular ("stackable") MPPT — design notes

*Can a 20 A module grow to 40 A, 60 A… by adding a panel and a module? Yes — two shapes, and the choice is architectural.*

| Shape | How it stacks | Wins | Costs |
|-------|---------------|------|-------|
| **A — one module per PV string, outputs paralleled on the battery** | Each module is a complete MPPT (tracker + 20 A buck + own output fuse + CAN node). Add a panel ⇒ add a string **and** a module. | Independent MPP tracking per string (a shaded string doesn't drag the array — the **tank tower / solar chimney / tree shadow** case); modules fail independently (lose 20 A, not the array); hot-add. This is Victron VE.Smart/DVCC and Libre Solar's CAN/ThingSet thesis. | Set-point coherence + CCL sharing need a coordinator (below). |
| **B — one controller, N interleaved power-stage phases** | One MPPT algorithm, one PV input, N identical half-bridge + inductor phase cards at 360°/N. | Ripple cancellation (shared output cap doesn't grow with N); active per-phase current sharing. How server VRMs / big chargers are built. | **One input ⇒ one string** — growth is series (hits V_in max) or parallel (string wire + fuse grow). No shading immunity. Hot-plug story is hard. |

**Status: Shape A — Selected** for this project (shading + independent failure). Shape B — **Disregarded** (single-string constraint).

### The aggregate limits, in the order you'll hit them

| # | Limit | Why it binds |
|---|-------|--------------|
| 1 | **Battery charge-current limit (C-rate / BMS CCL)** | LFP ~0.5 C recommended: a 100 Ah pack takes ~50 A ⇒ 2½ modules. FLA ~0.1–0.2 C. **Usually the first wall — the battery, not the roof, sets N.** |
| 2 | **Set-point coherence** | Each module senses battery voltage at *its* terminals; cable drop at 20 A makes it read high and terminate absorption early. Fix: remote (Kelvin) sense to the battery post, or a shared shunt broadcasting the true voltage. |
| 3 | **System-wide CCL sharing** | 3 × 20 A = 60 A into a 50 A BMS limit. BMS publishes CCL; coordinator hands each module CCL ÷ N_online. Stage transitions decided from the **aggregate** shunt current, not each module's own tail current. |
| 4 | **Common bus bar + battery cable + main fuse** | Each module lead carries 20 A; the bus carries the sum. Rough 75 °C copper: 10 AWG ≈ 35 A · 8 ≈ 50 A · 6 ≈ 65 A · 4 ≈ 85 A. At 48 V, 60 A ≈ 3 kW. Designer stamps the final sizing. |
| 5 | **Enclosure heat** | ~3 % loss × 20 A × 48 V ≈ 30 W per module; N in a sealed Dallas box is ventilation math ([REQ-CTRL-5](../../design/10-requirements.md#k-electronics--controls-architecture)). |
| 6 | **Night back-feed** | Paralleled synchronous bucks can conduct battery → PV after dark. **Each** module needs its own reverse blocking. |
| 7 | CAN bus | Termination + node count — a non-issue below ~10 modules. |

**Hard rule:** never parallel two MPPT *inputs* on one string — two trackers perturbing one array fight, and reverse current between input stages is a fire path. One string, one module.

### The module spec (Shape A)

- **Module** = 1 PV string + 1 MPPT (20 A) + own output fuse (~25–30 A) + CAN node, DIN-rail mounted. **Keyed MC4 in, keyed Powerpole out** — a volunteer adds one without opening anything else ([REQ-CTRL-1](../../design/10-requirements.md#k-electronics--controls-architecture)).
- **Pre-provision the bus for the final count on day one** — bus bar, enclosure width, main cable, N+1 fuse positions. Same logic as the slab's pull-strings and spare conduit ([REQ-SLAB-3](../../design/10-requirements.md#a2-foundation--slab--the-one-way-door)): growth must not reopen the box.
- **Coordination over CAN:** BMS → CVL/CCL → modules; shared stage transitions from the aggregate shunt.
- **Remote voltage sense** or a SmartShunt-class monitor as the single source of truth.
- **Sized to the battery's CCL**, not the roof.

**Where it lands:** at 24 V the Libre Solar 2420 HC has the CAN/ThingSet plumbing for a genuinely open stackable **bench** (verify multi-unit current-limit sharing in the shipping firmware). At 48 V, Victron SmartSolar + GX/DVCC does it natively for the **cow**; the **house** 6000XP is already stackable at a granularity of two.

---

## Open questions this log resolves / raises

> ✅ **Proposes to resolve** ([controls](controls.md) open Q): safety-controller platform → **ESPHome on Olimex ESP32-POE-ISO**, with Controllino MAXI as the Pending alternate if the stamping engineer wants a PLC form factor.
> ✅ **Proposes to resolve** ([power BOM](off-grid-power.md) "Cow MPPT" row): → **Victron SmartSolar**, sized to the routable string.
> **OPEN QUESTION:** OpenSprinkler DC/Latch variant — is one shipping, and does it pulse DC-latching solenoids? (Shortcut for §2 if yes.)
> **OPEN QUESTION:** Header-tank elevation → available head → whether any per-zone flow meter is viable (§4).
> **OPEN QUESTION:** Does the education program want a **multi-chemistry bench** at all? If yes, it becomes its own BOM section (Libre Solar 2420 HC + small panel + keyed 12/24 V batteries).
> **OPEN QUESTION:** Libre Solar firmware — multi-unit CCL sharing over CAN in the shipping release (§7).

*Upstream: [`30-electronics-and-controls.md`](../../design/30-electronics-and-controls.md), [`60-power-architecture.md`](../../design/60-power-architecture.md), [`70-resource-cycles.md`](../../design/70-resource-cycles.md). Feeds: [`controls.md`](controls.md), [`irrigation.md`](irrigation.md), [`off-grid-power.md`](off-grid-power.md). Format: [`README.md`](README.md).*
