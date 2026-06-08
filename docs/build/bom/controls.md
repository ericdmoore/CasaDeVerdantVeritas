# BOM · Controls (compute, sensing, actuation, comms)

*The electronics that sense, decide, move, and report. Implements [`30-electronics-and-controls.md`](../../design/30-electronics-and-controls.md), [`40-network-and-connectivity.md`](../../design/40-network-and-connectivity.md), and the safety/data requirements. Valves and pumps live in the [irrigation BOM](irrigation.md); this BOM owns their **control signal**, not the plumbing.*

> **Status:** 🟡 Scaffolding. Quantities **TBD** pending the final sensor/actuator list + zone layout (which also produces the Tier 1/2/3 load list the [power BOM](off-grid-power.md) needs).

---

## Architecture recap (what this BOM builds)

Per the design docs, **two compute roles** — never merged:

- 🔴 **Safety controller (Tier 1)** — runs the life-or-death loop (overtemp→vent, irrigation, alarm) **on-device**, surviving with HA/LAN/internet down ([REQ-NET-1](../../design/10-requirements.md#l-network--connectivity)). Tiny, battery-protected, its own alert channel.
- 🟠 **Program/data host (Tier 3)** — Home Assistant: dashboards, scheduling, history, remote access. Sheddable.

Edge nodes reach the core over **band-diverse transports** ([locked stack](../../design/40-network-and-connectivity.md#5-transport-as-few-as-the-physics-needs--band-diverse-each-earning-its-keep)): wired PoE + Zigbee + LoRa + WiFi.

---

## A. Compute & core

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Safety controller | Low-power MCU/PLC running critical loop on-device (e.g. ESPHome on ESP32, or industrial micro-PLC) | 1 | REQ-NET-1, REQ-ELEC-2 | TBD | TBD | TBD | TBD | proposed | Independent of HA; **fail-open** defaults |
| HA host | Mini PC / SBC, **SSD boot** (not SD card) | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | Tier 3; sheddable |
| Real-time clock | Battery-backed RTC module | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | Off-grid timekeeping w/o NTP |
| Watchdog | HW watchdog / scheduled power-cycle relay | 1 | REQ-NET-6 | TBD | TBD | TBD | TBD | proposed | Auto-recover a hung host/modem |

## B. Sensing

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Air temp / humidity | Greenhouse-rated, multiple zones | TBD | REQ-COOL-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Feeds safety loop **and** data layer |
| **Overtemp safety sensor** | Independent of the data sensors | 1+ | REQ-SAFE-5, REQ-NET-1 | TBD | TBD | TBD | TBD | proposed | Drives the alarm + vent on the safety controller |
| Soil / media moisture | Per bed/zone | TBD | REQ-WATER-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Drives irrigation logic |
| Light (PAR/lux) | 1–2 | REQ-DATA-1 | REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Shade/lesson data |
| Tank level | Cistern + header + pure tank | TBD | REQ-CYCLE-3, REQ-ELEC-4 | TBD | TBD | TBD | TBD | proposed | Low-water alert |
| Hydroponic EC / pH | If hydro zone | TBD | REQ-EDU-1, REQ-DATA-1 | TBD | TBD | TBD | TBD | proposed | Research zone |
| Battery SOC / shunt | (see [power BOM](off-grid-power.md)) | — | REQ-ELEC-4 | TBD | — | — | — | cross-ref | Feeds load-shed + alerts |

## C. Actuation (control side)

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Powered vent / louver actuators | DC linear actuators; **fail-open** | TBD | REQ-COOL-7 | TBD | TBD | TBD | TBD | proposed | Backed by passive wax-piston openers (passive BOM) |
| Exhaust / circulation fans | **Solar-direct DC** preferred | TBD | REQ-COOL-5 | TBD | TBD | TBD | TBD | proposed | Run hardest when sun = heat is max |
| Evap-cooling pump driver | Relay/driver (pump in irrigation BOM) | TBD | REQ-COOL-6 | TBD | TBD | TBD | TBD | proposed | |
| Irrigation valve drivers | Drivers for **latching solenoids** (irrigation BOM) | TBD | REQ-WATER-1 | TBD | TBD | TBD | TBD | proposed | Latching = ~zero holding current (off-grid) |
| High-temp alarm | Audible/visible, on safety controller | 1 | REQ-SAFE-5 | TBD | TBD | TBD | TBD | proposed | Fires before danger |
| Load-shed relays | SOC-tiered switching (T2/T3) | TBD | REQ-PWR-3, REQ-PWR-4 | TBD | TBD | TBD | TBD | proposed | |

## D. Network & comms (the locked transports)

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| PoE switch | Managed, VLAN-capable | 1 | REQ-NET-3, REQ-NET-8 | TBD | TBD | TBD | TBD | proposed | IoT / guest segmentation |
| Zigbee coordinator | USB stick, **Thread-capable** 802.15.4 | 1 | REQ-NET-8 | TBD | TBD | TBD | TBD | proposed | On a USB extension (2.4 GHz noise) |
| LoRa gateway | For far/canopy nodes | 1 | REQ-NET-8 | TBD | TBD | TBD | TBD | proposed | Day-1 vs later — open Q |
| WiFi access point | Guest + powered-node SSIDs, client isolation | 1 | REQ-NET-3, REQ-NET-9 | TBD | TBD | TBD | TBD | proposed | |
| Cellular uplink | LTE router + IoT SIM | 1 | REQ-NET-5 | TBD | TBD | TBD | TBD | proposed | Primary uplink |
| Critical-alert channel | Independent cellular/SMS from safety controller | 1 | REQ-NET-2 | TBD | TBD | TBD | TBD | proposed | Survives HA/AP loss |
| Comms SPD | Surge protection on data/antenna lines | TBD | REQ-CTRL-7 | TBD | TBD | TBD | TBD | proposed | TX storms |

## E. Connectors & wiring

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Keyed DC power connectors | **Anderson Powerpole** (color-coded, polarity-safe) | TBD | REQ-CTRL-1, REQ-CTRL-6 | TBD | TBD | TBD | TBD | proposed | The one connector 🟢 Green may plug |
| Sealed field connectors | **M12 X-coded (IP67)** for wet/exposed runs | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | Minimize exposed runs |
| Indoor data connectors | RJ45 (inside enclosures) | TBD | REQ-CTRL-2 | TBD | TBD | TBD | TBD | proposed | |
| Cabling | PoE/Cat6, low-voltage DC, conduit | TBD | REQ-ELEC-1, REQ-CTRL-3 | TBD | TBD | TBD | TBD | proposed | Conduit stub-ups pre-poured (REQ-SLAB-3) |
| Wire-to-wire splices | **Wago Lever-Nuts (221-series or equal)** — tool-free, reusable, transparent | TBD | REQ-CTRL-1, REQ-CTRL-8 | TBD | TBD | TBD | TBD | proposed | **Splices only** (non-terminations); low-voltage control — *not* the high-current bus (lugs/Anderson there) |

## F. Enclosure & support

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Core enclosure | Sealed, **shaded/cool sited**, breather + desiccant | 1 | REQ-CTRL-5 | TBD | TBD | TBD | TBD | proposed | Commodity-in-a-box; thermal-managed |
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
