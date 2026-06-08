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
   ☀ PV ARRAY ──DC──▶ ┌──────────────────────────┐
                       │  EG4 FlexBOSS21          │◀── CAN ──┐ closed-loop
                       │  hybrid inverter (MPPTs) │          │
                       └────────────┬─────────────┘   ┌──────┴───────────┐
                               AC   │                  │ HOUSE BATTERY     │
                                    │                  │ EG4 48V rack ×N   │
                                    │                  │ (≈35% of total)   │
                                    ▼                  └──────┬───────────┘
 GATEWAY / DISTRIBUTION                           48V DC bus  │
 ┌──────────────────── EG4 GRIDBOSS (MID) ─────────────────┐  │
 │ IN :  GRID ◀── campus tether (emergency AC)              │  │
 │       GEN  ◀── optional generator                        │  │
 │       INV  ◀── FlexBOSS21 AC                              │  │
 │ OUT:  BACKUP ────▶ CRITICAL panel  (Tier 1 + Tier 2)      │  │
 │       SMART 1 ───▶ grow lights      ┐                     │  │
 │       SMART 2 ───▶ hydro pump       │ SOC-based load-shed │  │
 │       SMART 3 ───▶ supplemental fans│  (Tier 2/3)         │  │
 │       SMART 4 ───▶ spare / AC-couple┘                     │  │
 │       NON-BACKUP ▶ least-critical loads                   │  │
 └───────────────────────────────────────────────────────────┘  │
                                                                 │
 ISOLATED COW BRANCH (taps house 48V DC bus — NEVER paralleled)  │
   house 48V DC bus ──▶ ┌──────────────────────────────────────┐ │
                        │ Victron Orion-Tr Smart 48/48 DC-DC    │◀┘
                        │ one-way · current-limited · NO inrush │
                        │ engages only when bus V = house-healthy│
                        └───────────────────┬──────────────────┘
                                 charge only │
                                             ▼
                        ┌──────────────────────────────────────┐
                        │ POWER COW (isolated): EG4 48V rack +   │
                        │ BMS/LVD on cart + portable inverter +  │
                        │ Victron SmartShunt (SOC)               │
                        └───────────────────┬────────────────────┘
                          load out (docked & ≥ LVD only) │
                                             ▼
                        ┌──────────────────────────────────────┐
                        │ COW SUB-PANEL (Tier 3): hydro demo,    │
                        │ data rig, event outlet, supplemental   │
                        └──────────────────────────────────────┘
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
   ☀ PV ARRAY ──DC──▶ ┌─────────────────────────┐◀── CAN ──┐ closed-loop
                       │  EG4 6000XP             │          │
                       │  48V hybrid, dual MPPT  │   ┌───────┴──────────┐
   campus tether ──AC─▶│  AC-in (grid/gen)       │   │ HOUSE BATTERY     │
   (emergency)         └───────────┬─────────────┘   │ EG4 48V rack ×N   │
                              AC-out│                 └───────┬──────────┘
                                    ▼                48V DC bus│
                    ┌───────────────────────────┐             │
                    │ GREENHOUSE LOAD PANEL      │             │
                    │  ├─ Tier 1 critical (always)│            │
                    │  ├─ Tier 2/3 via SOC relay  │ ◀── SmartShunt/BatteryProtect
                    │  │   (contactor sheds)      │     drives the shed
                    │  └─ ...                      │            │
                    └───────────────────────────┘             │
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
> **OPEN QUESTION:** Cow charging rate — the small Orion-Tr 48/48 (~8 A) may be slow; size up or give the cow its own PV+MPPT.
> **OPEN QUESTION:** Validate every port assignment against the current EG4 manuals (products evolve).

*Related: [`../design/60-power-architecture.md`](../design/60-power-architecture.md), [`bom/off-grid-power.md`](bom/off-grid-power.md). Sources: [EG4 GridBOSS wiring diagrams](https://bigbattery.com/wp-content/uploads/2024/11/EG4-GridBOSS-System-Wiring-Diagrams.pdf), [GridBOSS manual](https://signaturesolar.com/content/documents/EG4/EG4%20GridBOSS%20User%20Manual%20v1.1.2%2011-01-24.pdf), [FlexBOSS21 manual](https://eg4electronics.com/wp-content/uploads/2024/08/FlexBOSS-21-Manual.pdf).*
