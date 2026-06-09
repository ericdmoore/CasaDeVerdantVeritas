# Bed & Device Schedule

*The keystone quantity artifact. The [zone layout](80-zone-layout.md) says **where**; this says **how many** — beds, sensors, actuators, and their power tier. Populating it cascades into every BOM: the **Tier 1/2/3 load list** ([off-grid power](../build/bom/off-grid-power.md) sizing), **valve counts** ([irrigation](../build/bom/irrigation.md)), **device counts** ([controls](../build/bom/controls.md)), and **tool-set counts** ([structure](../build/bom/structure.md)).*

> **Status:** 🟡 Firming up. **Beds = decided** (6 grade SIP beds, §1). **Device wattages = grounded in real products** (§2–3, sourced) — no longer estimates. Still open: final device *selection* + *counts* and the days-of-autonomy target (→ battery size), confirmed with the 🔴 Red designer.

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

## 2. Device schedule — grounded in real products

*Power figures are real product specs / measured draws, not estimates (sources ↓). "Or equal" — these anchor the wattage, not the brand.*

| Device | Real product (or equal) | Tier | Power (real) |
|--------|--------------------------|------|--------------|
| Safety controller + sensor nodes | **ESP32 / ESPHome**, always-on | **T1** | **~0.5–1 W each** (active WiFi ~80–160 mA @5 V; deep-sleep µA but ours stay on) |
| Sensors: temp/RH, soil-moisture, tank level, overtemp | I²C/analog on the ESP nodes | T1/T3 | ~mW (powered by the node) |
| Hydro EC/pH, light/PAR | sensor modules | T3 | ~mW–1 W |
| Zigbee coordinator | **HA Connect ZBT-1** (USB) | T1 | **<1 W** |
| Cellular uplink **+ WiFi AP (combo)** | **USR-G806w**-class LTE + WiFi 6 | T1 alert / T3 rest | **~1.8 W standby, ~3.1 W full** |
| (alt ultra-low uplink) | Milesight UR41 / LINOVISION IOT-R41 | T1 | **<1 W idle** (~2.7 W typ.) |
| PoE switch (small 8-port) | managed | T3 | **~5–10 W idle** |
| HA host | **Raspberry Pi 5** + SSD (*not* an N100) | T3 | **~3–4 W idle** (N100 ~8–9 W) |
| RTC / watchdog / load-shed relays | modules | T1 | ~1 W |
| **Exhaust fans (DC, solar-direct)** | **Backwoods 16" 12/24 V** (1627 CFM); 80 W→3000 CFM class | **T2** | **~36–80 W each** (~×2 for ~6k CFM) |
| Evap-cooling pump | submersible cooler pump | T2 | **~33 W** (tiny DC fountain ~4–5 W) |
| **Transfer / lift pump** | **HYSKY DC60G-24120S-1**, 24 V submersible brushless, ~16.7 GPM, 12 m head *or equal* | **T2** | **~120 W** (solar-direct; intermittent tank refills; dry-run protected) |
| Vent linear actuators | 12/24 V, brief runs | T2 | ~20–50 W for seconds → ~0 daily; **wax-piston = 0 W** |
| Latching solenoid valves | per zone | T1 | **~0 W holding**; ms pulse → negligible/day |
| Grow light (seedling) | **SHOPLED 4 ft, 40 W** (true draw) | T3 | **~40 W** (run 12–16 h for starts) |
| **Small ultrasonic fogger** | **single-disc 24 V** (e.g. RM-1236, 24 V/0.65 A) | T3 | **~12–15 W** — *not* a 12-head 300–400 W pond unit |

> **Consolidation wins:** a **combo LTE + WiFi router** is *both* the uplink and the AP in one ~2–3 W box; the **Pi-5 host beats an N100 by ~5 W continuous (~120 Wh/day)** — real money off-grid.

## 3. Load-tier rollup → power sizing (grounded)

| Tier | Real items | Continuous | Wh/day |
|------|-----------|------------|--------|
| **Tier 1** (survives) | ESP32 safety + nodes (~2–3 W) + ZBT-1 (~1 W) + cellular alert (~1–2 W) + valve pulses | **~5–8 W** | **~120–190** |
| **Tier 2** (solar-correlated) | 2× DC fans (~72–160 W) + evap pump (~33 W) + transfer/lift pump (~120 W, intermittent) — **solar-direct, minimal battery** | ~100–280 W when running | sized to PV |
| **Tier 3** (sheds first) | Pi 5 (~3–4 W) + PoE sw + combo router (~8–13 W) + fogger (~12–15 W) + grow light (~40 W on) + structural LED (dimmable, ~5–15 W/m) + anti-condensation heater (~10–50 W, thermostatic) | ~15–25 W base | ~300–700 |

→ **Battery floor = Tier 1:** e.g. **~150 Wh/day × 3 days ÷ 0.85 DoD ≈ ~530 Wh usable** — a *small* LiFePO₄ carries the safety loop through 3 cloudy days. The PV + cow/house bulk carry Tier 2/3. This is the real load list the [power BOM](../build/bom/off-grid-power.md#sizing-basis--do-this-before-buying-anything) sizes against.

**Sources:** [ESP32 power](https://lastminuteengineers.com/esp32-sleep-modes-power-consumption/) · [Pi 5 vs N100 idle](https://the-diy-life.com/raspberry-pi-5-vs-intel-n100-pc-which-is-right-for-you/) · [USR-G806w / IoT router power](https://www.pusr.com/blog/In-Depth-Analysis-of-Power-Consumption-for-IoT-Routers) · [Backwoods 12/24 V DC fan](http://blog.backwoodssolar.com/2014/07/16-in-large-dc-fan-12v-24v/) · [evap/fountain pump W](https://www.amazon.com/Mavel-Star-Submersible-Fountain-Upgraded/dp/B0713T9PRP) · [SHOPLED 40 W grow light](https://www.amazon.com/SHOPLED-Fixture-Spectrum-Equivalent-Reflector/dp/B088CXZ5YG) · [single-disc fogger 24 V/15 W](https://www.alibaba.com/product-detail/2021-humidifier-24v-single-disc-ultrasonic_1600262586894.html) · [PoE switch idle](https://blog.it-planet.com/en/network-switch-reduce-power-consumption-and-save-costs/)

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
