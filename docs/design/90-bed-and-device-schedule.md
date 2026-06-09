# Bed & Device Schedule

*The keystone quantity artifact. The [zone layout](80-zone-layout.md) says **where**; this says **how many** — beds, sensors, actuators, and their power tier. Populating it cascades into every BOM: the **Tier 1/2/3 load list** ([off-grid power](../build/bom/off-grid-power.md) sizing), **valve counts** ([irrigation](../build/bom/irrigation.md)), **device counts** ([controls](../build/bom/controls.md)), and **tool-set counts** ([structure](../build/bom/structure.md)).*

> **Status:** 🟡 **Proposed v1** for an ~800 sq ft (20×40) house. Numbers are *defensible starting points*, **not confirmed** — the science/garden teacher sets the beds, the 🔴 Red designer sets device specs/wattages. Replace `~` values as they firm up; the rollups recompute from there.

---

## 1. Bed schedule

| Zone | Beds | Size (each) | Method | Irrigation |
|------|------|-------------|--------|-----------|
| **Grade beds (1 per grade, K–5)** | **6** | **4×8 ft elevated** (32 sq ft ea → **192 sq ft growing**) | **SIP / wicking**, free-standing islands | Grey-buffer fed; **waterfall-chainable** ([REQ-CYCLE-14](10-requirements.md#o-resource-cycles)) |
| **Seedling bench** (IZ5) | 1 | ~2×8 ft | Trays + grow light + fogger | Fine/low-flow + fogger |
| **Hydroponic demo** (IZ6) | 1 | ~2×8 ft | Kratky/NFT | Recirculating (own loop) |
| **Outdoor pad** (IZ8) | ~4 containers | — | Soil / TX-native | Drip / hose-bib |
| Root-window bed | 1 *(= one grade bed w/ a pane)* | 4×8 | SIP + viewing pane | Buffer-fed |

**Footprint check:** 6 grade beds at **6×10 ft effective** (the 4×8 bed + 2-ft access on *both* long sides — a 4-ft bed needs both-side reach, so islands) = **~360 sq ft**. In ~800 sq ft that leaves ~440 for spine + stations + infra → **fits.**

**Notes:** classes within a grade share their grade's bed. Make ≥1 grade bed **ADA height + knee clearance** to satisfy [REQ-ACC-2](10-requirements.md#h-accessibility--inclusion) (no separate ADA bed needed). All grade beds are **SIP**, so they tie into the grey-buffer **managed waterfall**.

→ **6 grade SIP beds + seedling + hydro (recirc) + outdoor.** SIP beds fill from the buffer (chained/valved, not 6 separate drip zones) → simplifies the [irrigation](../build/bom/irrigation.md) valve count.

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

- **Irrigation:** the **6 grade SIP beds fill from the grey buffer as chained waterfall run(s)** (standpipes + couplers per [REQ-CYCLE-14](10-requirements.md#o-resource-cycles)) — so ~2–3 fill valves, *not* 6 drip zones; + 1 hydro recirc + seedling/fogger lines. Fewer valves than the old all-drip model.
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
