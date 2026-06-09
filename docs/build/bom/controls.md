# BOM · Controls (compute, sensing, actuation, comms)

*The electronics that sense, decide, move, and report. Implements [`30-electronics-and-controls.md`](../../design/30-electronics-and-controls.md), [`40-network-and-connectivity.md`](../../design/40-network-and-connectivity.md), and the safety/data requirements. Valves and pumps live in the [irrigation BOM](irrigation.md); this BOM owns their **control signal**, not the plumbing.*

> **Status:** 🟡 Scaffolding. Quantities **TBD** pending the final sensor/actuator list + zone layout (which also produces the Tier 1/2/3 load list the [power BOM](off-grid-power.md) needs).

---

## Architecture recap (what this BOM builds)

Per the design docs, **two compute roles** — never merged:

- 🔴 **Safety controller (Tier 1)** — runs the life-or-death loop (overtemp→vent, irrigation, alarm) **on-device**, surviving with HA/LAN/internet down ([REQ-NET-1](../../design/10-requirements.md#l-network--connectivity)). Tiny, battery-protected, its own alert channel.
- 🟠 **Program/data host (Tier 3)** — Home Assistant: dashboards, scheduling, history, remote access. Sheddable.

Edge nodes reach the core over **band-diverse transports** ([locked stack](../../design/40-network-and-connectivity.md#5-transport-as-few-as-the-physics-needs--band-diverse-each-earning-its-keep)): wired PoE + Zigbee + LoRa + WiFi.

> **DC-direct, 48 V distributed, step down at the point of load.** PoE runs at ~48 V = our battery voltage, so the **PoE switch is DC-fed from the rail**. The governing topology is a **"snowflake": keep 48 V as long as possible and convert *at the load* (point-of-load).** Distributing 48 V means a spoke carries **¼ the current of 24 V / a tenth of 5 V** → **thin, cheap wire + negligible voltage drop** over greenhouse distances (5/12 V across tens of feet would sag badly). So **48 V spokes radiate to each zone, and a small buck steps down *there*** — 48→24 V at an actuation cluster, 48→5 V at a sensor node, etc. The **cascade (24→12→5)** lives only *within* a co-located cluster (e.g., the core's Pi + router + logic — cheap, common parts, negligible loss at tiny loads). **Tier 1 (ESP32 safety + alert) keeps its own 48→5 V feed.** 48-input stages span the **full ~46–58 V** swing; 48 V DC is **below the ~60 V SELV hazard line** (safe to distribute; still keep out of standing water/reach). The inverter is *only* for the cow's event AC ([REQ-CTRL-6](../../design/10-requirements.md#k-electronics--controls-architecture)) — efficient (no AC round-trip) *and* survives inverter-off.

---

## A. Compute & core

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Safety controller | Low-power MCU/PLC running critical loop on-device (e.g. ESPHome on ESP32, or industrial micro-PLC) | 1 | REQ-NET-1, REQ-ELEC-2 | TBD | TBD | TBD | TBD | proposed | Independent of HA; **fail-open** defaults |
| HA / NVR host | **Mini PC (N100-class)** + SSD — **justified by the ~20-camera NVR** compute (a Pi 5 can't) | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | ~8–30 W under NVR load; T3. *The camera count is what stepped this up off the Pi* |
| UPS (host) | Small UPS / battery-backed DC for the mini PC | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | **Graceful shutdown** on a rail dropout (avoid corruption). The 48 V battery is system-wide ride-through; this protects the host |
| Real-time clock | Battery-backed RTC module | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | Off-grid timekeeping w/o NTP |
| Watchdog | HW watchdog / scheduled power-cycle relay | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | Auto-recover a hung host/modem |
| DC-DC converters (**point-of-load**) | **48 V distributed to each zone**, stepped down **locally**: 48→24 V at actuation clusters; 48→5 V at sensor nodes; cascade 24→12→5 V only *within* a co-located cluster (cheap common parts) | TBD | REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | Thin wire + no voltage drop; size the 24 V buck to **peak concurrent load**; **Pi (T3) rides the core cascade** |
| Tier-1 power feed | **Separate small 48→5 V** (independent of the workhorse/cascade) | 1 | REQ-CTRL-6, REQ-NET-1 | TBD | TBD | TBD | TBD | proposed | ESP32 safety + critical alert — a workhorse/cascade failure must **not** reach Tier 1 |

## B. Sensing

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Air temp / humidity | **SHT31** (DFRobot SEN0385 outdoor / FS200-SHT31 probe) *or equal*; I²C | TBD | REQ-COOL-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | <10 mA (on the node); feeds safety loop **and** data layer |
| **Overtemp safety sensor** | Independent of the data sensors | 1+ | REQ-SAFE-5, REQ-NET-1 | TBD | TBD | TBD | TBD | proposed | Drives the alarm + vent on the safety controller |
| Soil / media moisture | **Capacitive** (DFRobot SEN0193 *or equal*) — no corrosion | TBD | REQ-WATER-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | mW on the node; drives irrigation logic |
| Light (PAR/lux) | 1–2 | REQ-DATA-1 | REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Shade/lesson data |
| **Wind sensor (speed + direction)** | **Ultrasonic, no moving parts** — Calypso ULP (~0.005–0.12 W) / Niubol RS485 Modbus (~0.4 W) *or equal* | 1 | REQ-COOL-10 | TBD | TBD | TBD | TBD | proposed | T1; selects chimney vs. ridge-venturi mode; **direction** guards the due-west wind-shadow case |
| Tank level | Cistern + header + pure tank | TBD | REQ-CYCLE-3, REQ-ELEC-4 | TBD | TBD | TBD | TBD | proposed | Low-water alert |
| Hydroponic EC / pH | If hydro zone | TBD | REQ-EDU-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Research zone |
| Battery SOC / shunt | (see [power BOM](off-grid-power.md)) | — | REQ-ELEC-4 | TBD | — | — | — | cross-ref | Feeds load-shed + alerts |

## C. Actuation (control side)

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Powered vent / louver actuators | **DC linear actuator**, greenhouse window-opener class (RollerTrol / PowerJack *or equal*) — ~1.5–2 A @12 V (≈18–24 W moving, **0 idle**), 20–60 lb force; **fail-open** | TBD | REQ-COOL-7 | TBD | TBD | TBD | TBD | proposed | Backed by passive wax-piston openers (passive BOM) |
| **Sliding shade-panel drive** | **Self-locking geared DC motor** + continuous-cable drum + pulleys + **mechanical limit switches**; UV-stable cable (s/s or Dyneema) | TBD | REQ-PASV-3 | TBD | TBD | TBD | TBD | proposed | Long bidirectional travel (CW/CCW); **holds at 0 power** (worm gear) + resists wind; limit switches = foolproof end-stops + stall timeout. **Stepper avoided** (holding current = off-grid penalty). ~20–50 W moving, 0 idle (T2); adjustable layer *atop* the fixed-overhang baseline |
| **Chimney baffle actuator** | Window-opener-class linear actuator (~2 A @12 V moving, 0 idle); **mode valve + winter damper** | 1 | REQ-COOL-9, REQ-COOL-10 | TBD | TBD | TBD | TBD | proposed | Open = stack mode; closed = wind mode / winter. **Wax-piston backstop** = fail open-when-hot |
| **Ridge-venturi vent actuator** | Same window-opener-class actuator | TBD | REQ-COOL-9, REQ-COOL-10 | TBD | TBD | TBD | TBD | proposed | **Interlocked** with the chimney baffle — never both open (short-circuit) |
| Exhaust / circulation fans | **Backwoods 16" 12/24 V** (36 W → 1627 CFM) / 80 W→3000 CFM class *or equal*; **solar-direct** | ~2 | REQ-COOL-5 | TBD | TBD | TBD | TBD | proposed | Run hardest when sun = heat is max |
| Evap-cooling pump driver | Relay/driver (pump in irrigation BOM) | TBD | REQ-COOL-6 | TBD | TBD | TBD | TBD | proposed | |
| Irrigation valve drivers | Drivers for **latching solenoids** (irrigation BOM) | TBD | REQ-WATER-1 | TBD | TBD | TBD | TBD | proposed | Latching = ~zero holding current (off-grid) |
| **Structural / work lighting** | **Dimmable DC LED strip** (12/24 V) + PWM dimmer, HA-controllable | TBD | REQ-LIGHT-2, REQ-EDU-4 | TBD | TBD | TBD | TBD | proposed | **T3**; ambient/work/event/showcase light (*not* a grow light); ~5–15 W per run-meter, dimmed |
| High-temp alarm | Audible/visible, on safety controller | 1 | REQ-SAFE-5 | TBD | TBD | TBD | TBD | proposed | Fires before danger |
| Load-shed relays | SOC-tiered switching (T2/T3) | TBD | REQ-PWR-3, REQ-PWR-4 | TBD | TBD | TBD | TBD | proposed | |
| **Per-circuit indicator lamps** | **6 mm metal IP66 panel lamp** after each fuse/breaker, in the **matching voltage per rail** (DC **5 V / 12 V / 24 V / 48 V** variants — don't cross-use); **color-coded by rail/tier**; + **blown-fuse LED**; optional **controller-driven status LED** (green on / amber shed / red fault) off ESP32 GPIO | TBD | REQ-NET-7, REQ-EDU-4, REQ-CTRL-1 | TBD | TBD | TBD | TBD | proposed | "Is it live?" at a glance — Amber diagnostic + teaching display; mW. **Not Shelly** (WiFi sprawl/power, DC-range, network-dependent). Tier-1 indication stays **passive** |
| Per-circuit DC sense *(optional)* | **INA219/INA226** (DC V + I) on the ESPHome node | TBD | REQ-NET-7, REQ-ELEC-4 | TBD | TBD | TBD | TBD | proposed | Per-circuit power/on-off into HA — **DC-native, local**; covers the Shelly "monitoring" use-case without WiFi-per-device |

## D. Network & comms (the locked transports)

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| PoE++ switches (**DC-input**) | **2× 8-port** managed, VLAN-capable; **48 V DC input** (wide ~48–57 V, *or* a DC-DC holding ~53–54 V) — fed from the **battery rail, no inverter** | 2 | REQ-NET-3, REQ-NET-8, REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | ~20 cams + nodes + APs exceed one switch; **48 V feed must source the full PoE budget**; DC-feed skips AC round-trip + survives inverter-off |
| Zigbee coordinator | USB stick, **Thread-capable** 802.15.4 | 1 | REQ-NET-8 | TBD | TBD | TBD | TBD | proposed | On a USB extension (2.4 GHz noise) |
| LoRa / **Meshtastic node** | **High on the weather station** (ESP32 + LoRa, solar-standalone) | 1 | REQ-NET-8, REQ-NET-2 | TBD | TBD | TBD | TBD | proposed | Far/canopy telemetry **+ resilient off-grid mesh alert path** (independent of cellular); sub-watt; height = range |
| WiFi access point | Guest + powered-node SSIDs, client isolation | 1 | REQ-NET-3, REQ-NET-9 | TBD | TBD | TBD | TBD | proposed | |
| Cellular uplink | LTE router + IoT SIM | 1 | REQ-NET-5 | TBD | TBD | TBD | TBD | proposed | Primary uplink |
| Critical-alert channel | Independent cellular/SMS from safety controller | 1 | REQ-NET-2 | TBD | TBD | TBD | TBD | proposed | Survives HA/AP loss |
| **PoE cameras — external (security)** | Fixed PoE IP cam, local RTSP/ONVIF | **8** | REQ-NET-3, REQ-NET-10 | TBD | TBD | TBD | TBD | proposed | ~5–15 W ea; **motion-triggered recording** to cut load; camera VLAN, local-first, **no internet-expose**; signage + retention; T2 |
| **PoE cameras — internal (growth)** | Fixed PoE cam, timelapse | **~12 (2/bed × 6)** | REQ-DATA-4, REQ-NET-10 | TBD | TBD | TBD | TBD | proposed | **Duty-cycle / snapshot — timelapse ≠ 24/7 streaming** (order-of-magnitude power saver); plants not students; **T3** |
| Comms SPD | Surge protection on data/antenna lines | TBD | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | TX storms |

## E. Connectors & wiring

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Keyed DC power connectors | **Anderson Powerpole** (color-coded, polarity-safe) | TBD | REQ-CTRL-1, REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | The one connector 🟢 Green may plug |
| Sealed field connectors | **M12 X-coded (IP67)** for wet/exposed runs | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | Minimize exposed runs |
| Indoor data connectors | RJ45 (inside enclosures) | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | |
| Cabling | **Cat6/6A for PoE++ (802.3bt)**, low-voltage DC, conduit | TBD | REQ-ELEC-1, REQ-CTRL-3 | TBD | TBD | TBD | TBD | proposed | Conduit stub-ups pre-poured (REQ-SLAB-3) |
| Cable glands | **IP-rated** entries into every enclosure | TBD | REQ-CTRL-2, REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | Keep water out at penetrations |
| Wire-to-wire splices | **Wago Lever-Nuts (221-series or equal)** — tool-free, reusable, transparent | TBD | REQ-CTRL-1, REQ-CTRL-8 | TBD | TBD | TBD | TBD | proposed | **Splices only** (non-terminations); low-voltage control — *not* the high-current bus (lugs/Anderson there) |

## F. Enclosure & support

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Core enclosure / wiring case | Sealed, **shaded/cool sited**, breather + desiccant | 1 | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | Commodity-in-a-box; thermal-managed |
| DIN rail + terminal blocks | Standard rail for breakers/relays/PSUs/terminals | TBD | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | Tidy, serviceable panel |
| **DC circuit breakers** | **DC-rated** (polarity-correct), per low-voltage circuit | TBD | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | Per-circuit protection — **not** AC breakers |
| Network switch enclosure | Case for the PoE switch + patch | 1 | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | |
| Desiccant + breather vent | Enclosure moisture control | TBD | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | Recharge/replace; pairs w/ breather membrane |
| **Anti-condensation heater** | Thermostatic, mild (~10–50 W) | 1 | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | **T3**; keeps electronics above dew point on cold/humid nights |
| GFCI / protection | On any AC; conduit, out of reach | TBD | REQ-ELEC-1 | TBD | TBD | TBD | TBD | proposed | |
| Spares shelf | Coordinator stick, sensor/node samples, fuses, fittings | 1 set | REQ-CTRL-4 | TBD | TBD | TBD | TBD | proposed | Amber repair stock; ≥2 of failure-prone parts |

**Running subtotal:** TBD

---

## Notes
- **Poka-yoke everything pluggable** ([REQ-CTRL-1](../../design/10-requirements.md#k-electronics--controls-architecture)) — keyed + color-coded so 🟢 Green can only plug power, and can't plug it wrong.
- **Polarity convention** ([REQ-CTRL-8](../../design/10-requirements.md#k-electronics--controls-architecture)): on any low-voltage DC pair, the **marked conductor = positive (+)**. One rule, everywhere — so Amber never guesses.
- **Splices vs. terminations:** **Wago Lever-Nuts** for wire-to-wire splices; device terminals use their proper lugs/connectors; the high-current battery bus uses lugs / Anderson, never Wagos.
- **DC-first** ([REQ-CTRL-6](../../design/10-requirements.md#k-electronics--controls-architecture)) — minimize AC/inverter inside the greenhouse.
- The safety loop **must demo working with HA powered off** before sign-off.

## Open questions
> **OPEN QUESTION:** Final sensor + actuator list per zone (zones now defined in [`80-zone-layout.md`](../../design/80-zone-layout.md): IZ1–8 + functional zones) → sets quantities here *and* the power load tiers.
> **OPEN QUESTION:** Safety controller platform — ESPHome/ESP32 vs. a hardened micro-PLC (Tier-1 reliability vs. ecosystem).
> **OPEN QUESTION:** LoRa gateway day-1 or deferred (depends on the far-node list).

*Upstream: [`30-electronics-and-controls.md`](../../design/30-electronics-and-controls.md), [`40-network-and-connectivity.md`](../../design/40-network-and-connectivity.md). Format: [`README.md`](README.md). Related: [`off-grid-power.md`](off-grid-power.md), [`irrigation.md`](irrigation.md).*
