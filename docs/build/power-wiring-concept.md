# Power Wiring — concept (candidate platforms)

*Conceptual block diagrams for the [off-grid power architecture](../design/60-power-architecture.md) — how the pieces connect. **Two candidate platforms** shown for comparison.*

> ⚠️ **Conceptual, not a construction drawing.** The inverter/EMS platform is **not chosen** ([open question](../design/60-power-architecture.md#open-questions)). This is 🔴 **Red licensed work** — validate against the vendors' own wiring manuals and a licensed installer before anything is built. Examples name products "or equal."
>
> Both options share the **isolated charge-only cow** ([REQ-PWR-8..14](../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)): the cow taps the house 48 V DC bus through a **one-way, current-limited DC-DC charger** and **never parallels** the house. EG4 + Victron mixed per "use what fits."

---

## Option A — EG4 GridBOSS + FlexBOSS21 (whole-home scale)

Best if you want **built-in SOC smart-load shedding** and **tether-as-grid** seamless transfer. Likely *oversized* for a greenhouse.

```
 GENERATION / CONVERSION
   ☀ PV ARRAY ──DC──▶  ┌──────────────────────────┐
                       │  EG4 FlexBOSS21          │◀── CAN ──┐ closed-loop
                       │  hybrid inverter (MPPTs) │          │
                       └────────────┬─────────────┘    ┌──────┴───────────┐
                               AC   │                  │ HOUSE BATTERY    │
                                    │                  │ EG4 48V rack ×N  │
                                    │                  │ (≈35% of total)  │
                                    ▼                  └───────────┬──────┘
 GATEWAY / DISTRIBUTION                           48V DC bus       │
 ┌──────────────────── EG4 GRIDBOSS (MID) ───────────────────┐     │
 │ IN :  GRID ◀── campus tether (emergency AC)               │     │
 │       GEN  ◀── optional generator                         │     │
 │       INV  ◀── FlexBOSS21 AC                              │     │
 │ OUT:  BACKUP ────▶ CRITICAL panel  (Tier 1 + Tier 2)      │     │
 │       SMART 1 ───▶ grow lights      ┐                     │     │
 │       SMART 2 ───▶ hydro pump       │ SOC-based load-shed │     │
 │       SMART 3 ───▶ supplemental fans│  (Tier 2/3)         │     │
 │       SMART 4 ───▶ spare / AC-couple┘                     │     │
 │       NON-BACKUP ▶ least-critical loads                   │     │
 └───────────────────────────────────────────────────────────┘     │
                                                                   │
 ISOLATED COW BRANCH (taps house 48V DC bus — NEVER paralleled)    │
   house 48V DC bus ──▶ ┌───────────────────────────────────────┐  │
                        │ Victron Orion-Tr Smart 48/48 DC-DC    │◀ ┘
                        │ one-way · current-limited · NO inrush  │
                        │ engages only when bus V = house-healthy│
                        └────────────────────┬───────────────────┘
                                 charge only │
                                             ▼
                        ┌────────────────────────────────────────┐
                        │ POWER COW (isolated): EG4 48V rack +   │
                        │ BMS/LVD on cart + portable inverter +  │
                        │ Victron SmartShunt (SOC)               │
                        └────────────────────────────────┬───────┘
                          load out (docked & ≥ LVD only) │
                                                         ▼
                        ┌────────────────────────────────────────┐
                        │ COW SUB-PANEL (Tier 3): hydro demo,    │
                        │ data rig, event outlet, supplemental   │
                        └────────────────────────────────────────┘
```

**Key connections**

| From | To | Carries | Notes |
|------|----|---------|-------|
| PV array | FlexBOSS21 PV in | DC | Built-in MPPTs |
| House EG4 batteries | FlexBOSS21 batt + **CAN** | 48 V DC + comms | Closed-loop BMS |
| FlexBOSS21 AC | GridBOSS **INV** | AC | Inverter source |
| **Campus tether** | GridBOSS **GRID** in | AC (emergency) | Off-grid twist: tether = "grid" |
| GridBOSS **BACKUP** | Critical panel | AC | Tier 1 + 2, stays powered |
| GridBOSS **SMART 1–4** | Tier 2/3 loads | AC | **SOC shedding built in** (= REQ-PWR-3/4) |
| House 48 V bus | Victron **Orion-Tr 48/48** | DC | One-way cow charger, gated house-healthy |
| Cow | Cow sub-panel | DC/AC | Live only docked + ≥ LVD |

---

## Option B — EG4 6000XP (greenhouse scale, simpler)

Right-sized for a greenhouse (~6 kW / 8 kW PV). No fancy smart ports — **load-shedding via SOC-triggered relays** on the load panel instead.

```
   ☀ PV ARRAY  ──DC──▶ ┌─────────────────────────┐◀── CAN ───┐ closed-loop
                       │  EG4 6000XP             │           │
                       │  48V hybrid, dual MPPT  │   ┌───────┴───────────┐
   campus tether ──AC─▶│  AC-in (grid/gen)       │   │ HOUSE BATTERY     │
   (emergency)         └────────────┬────────────┘   │ EG4 48V rack ×N   │
                              AC-out│                └─────────┬─────────┘
                                    ▼               48V DC bus │
                    ┌─────────────────────────────┐            │
                    │ GREENHOUSE LOAD PANEL       │            │
                    │  ├─ Tier 1 critical (always)│            │
                    │  ├─ Tier 2/3 via SOC relay  │ ◀── SmartShunt/BatteryProtect
                    │  │   (contactor sheds)      │     drives the shed
                    │  └─ ...                     │            │
                    └─────────────────────────────┘            │
                                                               │
   house 48V DC bus ──▶ Victron Orion-Tr 48/48 DC-DC ──▶ COW ──▶ cow sub-panel
                        (one-way · current-limited)    (isolated, ≥ LVD)
```

Load-shed here = a **SOC relay** (Victron SmartShunt/BMV relay → contactor, or a BatteryProtect) dropping Tier-2/3 branches — simpler and cheaper than GridBOSS, slightly less elegant.

---

## Which to pick

| | **A — GridBOSS + FlexBOSS21** | **B — 6000XP** |
|---|---|---|
| Scale | Whole-home (200 A) — *oversized* | Greenhouse (~6 kW) — *right-sized* |
| Tier 2/3 shedding | **Built-in smart ports** | External SOC relay |
| Tether transfer | Seamless (GRID port) | Via AC-in |
| Cost / complexity | Higher | Lower |
| Best when | You want programmable smart loads + room to grow | You want simple + cheap at greenhouse scale |

**Both** keep the cow isolated/charge-only via the Victron Orion DC-DC, and both are single-bank on the house side (no multi-bank orchestration).

> ✅ **Working direction (2026-06-08): Option B — EG4 6000XP-class**, right-sized for the greenhouse. Option A (GridBOSS) retained for reference; revisit only if programmable smart-load orchestration or big expansion is wanted. The 6000XP all-in-one bundles MPPT + inverter/charger + controller in one box.

## Open questions
> **OPEN QUESTION:** Confirm + size **Option B (EG4 6000XP-class)** with the 🔴 Red designer once the load list exists.
> ✅ **RESOLVED:** Cow charging = Orion baseline + manual routable PV string (see [Cow charging — two tiers](#cow-charging--two-tiers--2026-06-09)).
> **OPEN QUESTION:** Validate every port assignment against the current EG4 manuals (products evolve).

---

## Detailed wiring — EG4 6000XP (✅ working direction)

Terminal-level view of Option B. *(Conceptual; confirm terminal names + the neutral/ground bonding scheme against the [6000XP manual](https://eg4electronics.com/wp-content/uploads/2024/03/EG4_6000XP_Off_Grid_Inverter_User_Manual.pdf) and your installer — off-grid N-G bonding is an easy thing to get wrong.)*

```
  PV STRINGS                                                   MONITORING
  ┌───────┐  DC                                                ┌──────────────┐
  │ str 1 ├─────▶ MPPT 1 ┐                                     │ EG4 WiFi/4G  │
  └───────┘              ├──┐                                  │ dongle → app │
  ┌───────┐  DC          │  │                                  └──────┬───────┘
  │ str 2 ├─────▶ MPPT 2 ┘  │                                         │ RS485/CAN
  └───────┘                 ▼                                          ▼
                    ┌─────────────────────────────────────────────────────────┐
                    │                  EG4 6000XP  (48 V hybrid)              │
   HOUSE BATTERY    │  [PV1] [PV2]   [BAT +/–]  [BMS CAN/RS485]               │
   EG4 48V rack ×N ─┼──────────────▶ BAT ◀─────── CAN (closed-loop) ──────────┤
   (~35% of total)  │                                                         │
   campus tether ──▶│ [AC IN  (Grid/Gen)]              [AC OUT (Load)]        │
   (emergency AC)   └──────────────────────────────────────────┬──────────────┘
                         ▲ auto-transfer + charge              │ 120/240 V
                         │ (runs loads + recharges even        ▼
                         │  with a flat battery — REQ-PWR-13)  ┌───────────────────────┐
                         │                                     │ GREENHOUSE LOAD PANEL │
   ⏚ ground rod / SPD ───┴── bond per manual                   │ main breaker          │
                                                               │  ├─ Tier 1 critical ──── always on (safety loop)
                          SmartShunt ──▶ relay ──▶ contactor  ─┤  ├─ Tier 2/3 branch ──── shed on low SOC
                          (house SOC)        (sheds T2/3)      │  └─ ...               │
                                                               └──────────┬────────────┘
                                                                         │
  ISOLATED COW BRANCH (taps the 48 V BATTERY bus — never the AC, never paralleled)
   48V battery bus ──▶ ┌────────────────────────────────────┐
                       │ Victron Orion-Tr Smart 48/48 DC-DC │  one-way · current-limited ·
                       │ (input-voltage lockout = house-OK) │  NO inrush
                       └──────────────────┬─────────────────┘
                                          │ charge only
                                          ▼
                       ┌─────────────────────────────────────┐
                       │ POWER COW: EG4 48V rack + BMS/LVD,  │
                       │ on cart + portable inverter (events)│
                       │ + Victron SmartShunt (SOC readout)  │
                       └──────────────────┬──────────────────┘
                                          | load out (docked & ≥ LVD)
                                          ▼
                       ┌─────────────────────────────────────┐
                       │ COW SUB-PANEL (Tier 3): hydro demo, │
                       │ data rig, event outlet, supplemental│
                       └─────────────────────────────────────┘
```

**6000XP terminal connections**

| 6000XP terminal | Connects to | Notes |
|-----------------|-------------|-------|
| **PV1 / PV2** | PV strings | Dual MPPT, ≤ ~500 V/string per manual |
| **BAT +/–** | House EG4 48 V rack bus | Plus **BMS CAN/RS485** for closed-loop SOC/charge |
| **AC IN (Grid/Gen)** | **Campus tether** (emergency) | Auto-transfer; charges + powers loads with a flat battery |
| **AC OUT (Load)** | Greenhouse load panel | 120/240 V split-phase |
| **Comms** | EG4 WiFi/4G dongle | Monitoring/alerts app |
| **Ground/SPD** | Ground rod + bond | **N-G bonding per manual** (off-grid gotcha) |
| 48 V battery bus | Victron Orion-Tr 48/48 | One-way cow charger, taps **DC**, not AC |

> **Note:** the cow charger taps the **48 V battery bus** (DC side), *not* the AC output — so the cow is fed at the battery, charges one-way, and never touches the AC distribution or parallels the house.

### Cow charging — two tiers (✅ 2026-06-09)

The cow has **two charge paths, both into the cow battery in parallel** (no fight — each charger regulates to its own setpoint and just adds current):

```
 ① BASELINE (foolproof, automatic)
   house 48V bus ──▶ Victron Orion-Tr 48/48 DC-DC ──▶ COW battery
                     (always-on · ~8A · current-limited · input-V lockout = house-OK)

 ② ENHANCEMENT (manual solar boost)
                     ┌─ PV-rated DC CHANGEOVER (switch no-load) ─┐
   routable string ─┤  HOUSE → 6000XP MPPT-2  (boosts the house) │
   (≤ cow MPPT max) │  COW   → cow's own MPPT (fast refill)      ├─▶ COW battery
                     └────────────────────────────────────────────┘
```

- **Baseline = Orion**: always trickles the cow from the house bus; its **input-voltage lockout** auto-pauses if the house dips → house self-protects.
- **Enhancement = routable string**: flip to **COW** for a fast solar refill when it's come back depleted; otherwise **HOUSE** (the string feeds MPPT-2). **Switch dead**; on undock go **HOUSE first, then unplug**.
- Constraints: string Voc/Isc fits **both** MPPT windows; **Orion + string current ≤ cow BMS charge limit**.

---

*Related: [`../design/60-power-architecture.md`](../design/60-power-architecture.md), [`bom/off-grid-power.md`](bom/off-grid-power.md). Sources: [EG4 6000XP manual](https://eg4electronics.com/wp-content/uploads/2024/03/EG4_6000XP_Off_Grid_Inverter_User_Manual.pdf), [EG4 GridBOSS wiring diagrams](https://bigbattery.com/wp-content/uploads/2024/11/EG4-GridBOSS-System-Wiring-Diagrams.pdf), [FlexBOSS21 manual](https://eg4electronics.com/wp-content/uploads/2024/08/FlexBOSS-21-Manual.pdf).*
