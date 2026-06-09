# Bed & Device Schedule

*The keystone quantity artifact. The [zone layout](80-zone-layout.md) says **where**; this says **how many** — beds, sensors, actuators, and their power tier. Populating it cascades into every BOM: the **Tier 1/2/3 load list** ([off-grid power](../build/bom/off-grid-power.md) sizing), **valve counts** ([irrigation](../build/bom/irrigation.md)), **device counts** ([controls](../build/bom/controls.md)), and **tool-set counts** ([structure](../build/bom/structure.md)).*

> **Status:** 🟡 **Proposed v1** for an ~800 sq ft (20×40) house. Numbers are *defensible starting points*, **not confirmed** — the science/garden teacher sets the beds, the 🔴 Red designer sets device specs/wattages. Replace `~` values as they firm up; the rollups recompute from there.

---

## 1. Bed schedule

| Zone | Beds | Size (each) | Method | Irrigation |
|------|------|-------------|--------|-----------|
| **IZ1** south in-ground | ~3 | ~3×8 ft | Soil (full sun) | Drip zone |
| **IZ2** south raised | ~3 | ~3×6 ft | Soil, raised | Drip zone |
| **IZ3** north raised | ~3 | ~3×6 ft | Soil, shade-tolerant | Drip zone |
| **IZ4** ADA bed | 1 | ~3×6 ft @ ~30" | Soil, knee clearance | Drip zone |
| **IZ5** seedling bench | 1 | ~2×8 ft | Trays + grow light + fogger | Fine/low-flow + fogger |
| **IZ6** hydroponic demo | 1 | ~2×8 ft | Kratky/NFT | Recirculating (own loop) |
| **IZ7** wicking/SIP run | ~3 (chained) | ~3×6 ft | Sub-irrigated, **waterfall-chained** ([REQ-CYCLE-14](10-requirements.md#o-resource-cycles)) | Buffer → bed→bed spill |
| **IZ8** outdoor pad | ~4 containers | — | Soil/native | Drip / hose-bib |
| Root-window bed | 1 *(within IZ1/IZ2)* | ~3×4 ft | Soil + viewing pane | Drip |

→ **~18 beds / ~6 drip valve zones + 1 recirc (IZ6) + 1 wicking-run fill (IZ7).** Confirms the [irrigation](../build/bom/irrigation.md) valve count.

## 2. Device schedule

| Device | Zone(s) | Qty | Tier | ~W (run) | Drives |
|--------|---------|-----|------|----------|--------|
| **Overtemp safety sensor** | ridge/core | 1–2 | **T1** | ~0.5 | controls (safety loop) |
| Air temp/humidity | 2–3 zones | ~3 | T1/data | ~1 | controls, data |
| Soil-moisture | per bed group | ~6 | T1/T3 | ~0.5 | irrigation logic |
| Light / PAR | interior | 1–2 | T3 | ~0.5 | data |
| Tank levels | cistern/white/grey/pure + basin | ~5 | T1 | ~0.5 | low-water alerts |
| Hydro EC / pH | IZ6 | ~2 | T3 | ~1 | research |
| **Exhaust / circ fans (DC)** | ridge/walls | ~2–3 | **T2 (solar-direct)** | ~100–400 ea | power (peak), cooling |
| Vent actuators | ridge/sides | ~2–4 | T2 | ~10 (pulse) | + passive wax-piston backup |
| Evap pump | pad wall | 1 | T2 | ~50–150 | cooling assist |
| **Latching irrigation valves** | per zone | ~8 | T1 (pulse) | ~0 hold | irrigation |
| Grow light | IZ5 | 1–2 | T3 | ~50–200 | seedlings |
| DC ultrasonic fogger | IZ5 | 1 | T3 | ~20–50 | propagation/showcase |
| Safety controller | core | 1 | **T1** | ~2 | the brain |
| HA host (SSD) | core | 1 | T3 | ~5–15 | orchestration |
| Network (PoE sw, Zigbee, LoRa, WiFi AP, cellular) | core | set | T1 alert / T3 rest | ~15–25 | network |
| Load-shed relay, watchdog, RTC | core | set | T1 | ~1 | resilience |

## 3. Load-tier rollup → power sizing

*Fill the watts above, then sum. Proposed v1 ballparks:*

| Tier | What | ~Continuous | ~Wh/day | Notes |
|------|------|-------------|---------|-------|
| **Tier 1** (survives) | Safety controller + sensing + alert + Zigbee + night-irrigation pulses | **~6–10 W** | **~150–240** | This × autonomy days ÷ DoD = the **battery floor** |
| **Tier 2** (solar-correlated) | Fans + evap pump + vent actuators | ~150–600 W *when running* | *(sun-direct — minimal battery)* | Sized to PV, runs on sun |
| **Tier 3** (sheds first) | HA + AP + LoRa + grow light + fogger + data | ~30–60 W | ~400–900 | Drops on low SOC |

→ This is the **load list the [power BOM](../build/bom/off-grid-power.md#sizing-basis--do-this-before-buying-anything) waits on.** Tier 1 sets the battery; PV sized to recharge + carry daytime Tier 2/3.

## 4. Derived counts (what this unblocks)

- **Irrigation:** ~8 latching valves · ~6 drip zones · 1 recirc · 1 wicking run · standpipes/couplers per IZ7 chain.
- **Controls:** ~18 sensors + ~10 actuators + the core/network set → device count + conduit/stub-ups.
- **Tools (structure):** class of ~25 → **~30 trowels + sets** of forks/cultivators; ~6 table-group caddies; glove sets kid+adult.
- **Power:** the Tier rollup → battery + array sizing.

---

## Open questions (the real inputs)
> **OPEN QUESTION:** Teacher confirms **bed count/size/method** per zone (drives everything in §1).
> **OPEN QUESTION:** 🔴 Red designer confirms **device specs + actual wattages** (drives §2–3 → power sizing).
> **OPEN QUESTION:** Final **site dimensions** — if not ~20×40, bed counts scale.
> **OPEN QUESTION:** Days-of-autonomy target for Tier 1 (recommend 2–3) → battery size.

*Bridges [`80-zone-layout.md`](80-zone-layout.md) → the [BOMs](../build/bom/). Feeds [`off-grid-power.md`](../build/bom/off-grid-power.md), [`irrigation.md`](../build/bom/irrigation.md), [`controls.md`](../build/bom/controls.md), [`structure.md`](../build/bom/structure.md).*
