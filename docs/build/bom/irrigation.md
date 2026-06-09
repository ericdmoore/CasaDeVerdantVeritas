# BOM · Irrigation & Water

*The plumbing from harvest → storage → distribution, plus fertigation and freeze protection. Implements [REQ-WATER-*](../../design/10-requirements.md#e-irrigation--water), [REQ-CYCLE-*](../../design/10-requirements.md#o-resource-cycles), and the gravity/wicking parts of [REQ-PASV](../../design/10-requirements.md#m-passive-architecture). Valves are driven by the [controls BOM](controls.md); this BOM owns the plumbing.*

> **Status:** 🟡 Scaffolding. Quantities **TBD** pending floor plan / zone layout and tank sizing ([REQ-WATER-5](../../design/10-requirements.md#e-irrigation--water)).

---

## Two off-grid design choices that drive this BOM

1. **Latching solenoid valves** — pulse to open/close, **~zero holding current.** On a battery, ordinary always-energized solenoids are a non-starter; latching is the off-grid default.
2. **Gravity-fed, low-pressure distribution** — the elevated header tank ([REQ-PASV-4](../../design/10-requirements.md#m-passive-architecture)) feeds drip by gravity, so emitters must be **pressure-compensating / low-head rated.** Waters with a dead battery — the foolproof path.

The water is **quality-tiered** ([resource cycles](../../design/70-resource-cycles.md)): bulk rain → cistern → general irrigation; distilled-grade condensate → pure tank → evap pads / battery / sensitive hydro.

---

## A. Harvesting & inflow

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Roof gutters + downspouts | Sized for Dallas downpours | TBD | REQ-WATER-3, REQ-CYCLE-1 | TBD | TBD | TBD | TBD | proposed | Primary catchment |
| PV array gutter | Low-edge collection | TBD | REQ-CYCLE-1 | TBD | TBD | TBD | TBD | proposed | Clean runoff |
| First-flush diverters | Per catchment | TBD | REQ-CYCLE-1 | TBD | TBD | TBD | TBD | proposed | Dump dirty initial flow |
| Inlet screens / leaf filters | Mesh + debris | TBD | REQ-CYCLE-1 | TBD | TBD | TBD | TBD | proposed | Mosquito + debris |
| Interior condensate gutters | Twin-wall channel / eave collection | TBD | REQ-CYCLE-2 | TBD | TBD | TBD | TBD | proposed | Distilled-grade → pure tank; **construction-locked** |

## B. Storage

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Bulk cistern | Sized per autonomy calc; low/ground | TBD | REQ-WATER-5 | TBD | TBD | TBD | TBD | proposed | Raw rainwater; **covered** (REQ-WATER-2) |
| **Elevated WHITE tank** | Clean water, gravity head | 1 | REQ-PASV-4, REQ-CYCLE-3 | TBD | TBD | TBD | TBD | proposed | Filtered rain + tether; feeds sinks/clean irrigation |
| **Elevated GREY tank** | Wash-reuse, gravity head | 1 | REQ-CYCLE-3 | TBD | TBD | TBD | TBD | proposed | Settled+filtered wash water → root drip |
| **Elevated PURE tank** | Condensate store | 1 | REQ-CYCLE-2 | TBD | TBD | TBD | TBD | proposed | Evap/battery/hydro feed |
| **Tank tower / stand** | Engineered for dead + wind load | 1 | REQ-STR-1, REQ-CYCLE-3 | TBD | TBD | TBD | TBD | proposed | ~1,700 lb full + wind sail; **foundation pre-pour** (🔴 Red) |
| Tank covers / screens | All open surfaces | TBD | REQ-WATER-2 | TBD | TBD | TBD | TBD | proposed | Mosquito + child safety |
| Tank level sensors | (driven by [controls](controls.md)) | — | REQ-CYCLE-3 | TBD | — | — | — | cross-ref | Low-water alerts |
| Overflow routing | White→cistern; grey→beds/swale | TBD | REQ-CYCLE-4 | TBD | TBD | TBD | TBD | proposed | No wasted water |

## C. Pumps & pressure

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Transfer pump | DC, cistern → white tank (**solar-direct** if possible) | 1 | REQ-WATER-1, REQ-PWR-3 | TBD | TBD | TBD | TBD | proposed | Lifts to the elevated tank |
| **Coarse pre-filter (~500 µm)** | Flushable spin-down, **before the pump** | 1 | REQ-CYCLE-11 | TBD | TBD | TBD | TBD | proposed | Protects the pump from grit |
| **Fine filters (~100 µm → ~50 µm)** | Staged spin-down, **after the pump** before the tank | 2 | REQ-CYCLE-11 | TBD | TBD | TBD | TBD | proposed | Coarse-first = each stage lasts longer; flushable |
| Pressure regulation | Low-pressure reg for gravity drip | TBD | REQ-PASV-4 | TBD | TBD | TBD | TBD | proposed | Match emitter spec |

## D. Distribution

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| **Latching solenoid valves** | Per zone; ~zero holding current | TBD | REQ-WATER-1, REQ-PWR-2 | TBD | TBD | TBD | TBD | proposed | Off-grid default; driver in [controls](controls.md) |
| Manifold / mainline | Sized to zones | TBD | REQ-WATER-1 | TBD | TBD | TBD | TBD | proposed | |
| Drip lines + emitters | **Pressure-compensating, low-head** | TBD | REQ-PASV-4 | TBD | TBD | TBD | TBD | proposed | Must work at gravity pressure |
| Wicking-bed kits | Reservoir liner, fill/overflow, wick media | TBD | REQ-PASV-5 | TBD | TBD | TBD | TBD | proposed | Multi-day untended buffer |
| Ollas | Buried porous pots (demo beds) | TBD | REQ-PASV-5 | TBD | TBD | TBD | TBD | proposed | Optional/education |
| Humidity domes | Clear covers for seed/cutting trays | TBD | REQ-CYCLE-12 | TBD | TBD | TBD | TBD | proposed | **Passive** propagation humidity — zero power/pressure |
| **DC ultrasonic fogger** | Low-voltage piezo fogger, enclosed propagation chamber | 1 | REQ-CYCLE-12 | TBD | TBD | TBD | TBD | proposed | **Pure-tank-fed** (mineral-free); no pressure needed; **Tier-3, HA-controllable**; showcase. *Not* a pressure/gravity mister (head insufficient) |
| Manual override valves | Hand valves per zone | TBD | REQ-PASV-7 | TBD | TBD | TBD | TBD | proposed | Tool-free fallback |

## E. Fertigation

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Fertigation injector | Venturi / dosing for **compost / worm tea** | 1 | REQ-CYCLE-7 | TBD | TBD | TBD | TBD | proposed | Nutrient cycle → distribution |
| Tea filter / strainer | Pre-emitter | 1 | REQ-CYCLE-7 | TBD | TBD | TBD | TBD | proposed | Stops clogging |

## F. Wash station & greywater reuse

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Wash sinks | Row; kid-height + one ADA | TBD | REQ-CYCLE-10 | TBD | TBD | TBD | TBD | proposed | Fed from WHITE tank |
| Soil-catch potting table | Bench w/ integrated hole + catchment | 1 | REQ-CYCLE-10 | TBD | TBD | TBD | TBD | proposed | Soil → back to beds |
| Settling tank / sediment trap | Before the grey filter | 1 | REQ-CYCLE-10 | TBD | TBD | TBD | TBD | proposed | Sediment → beds/compost; clean periodically |
| Greywater filter | Screen/disc, pre-grey-tank | 1 | REQ-CYCLE-10 | TBD | TBD | TBD | TBD | proposed | So reuse won't clog drip |
| Reclaimed plumbing | **Labeled (purple), no cross-connection** | TBD | REQ-WATER-4, REQ-CYCLE-10 | TBD | TBD | TBD | TBD | proposed | Grey → root/non-edible only |

## G. Backup & protection

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|------|--------|-------|
| Campus hose inlet | **Air-gap discharge into the top of the WHITE tank** | 1 | REQ-WATER-4, REQ-WATER-5, REQ-PWR-7 | TBD | TBD | TBD | TBD | proposed | Air gap = textbook backflow control; emergency only |
| Freeze protection | Heat tape / drain-down / insulation; elevated tanks more exposed | TBD | REQ-HEAT-1 | TBD | TBD | TBD | TBD | proposed | Survive hard-freeze nights |

**Running subtotal:** TBD

---

## Notes
- **Latching valves + gravity feed** are the two choices that make irrigation survive a dead battery — keep them central.
- Every open water surface **covered** (mosquito + the child-safety rule, REQ-WATER-2).
- Condensate is distilled-grade → keep it for evap pads / battery / sensitive hydro, not mixed into the bulk cistern.
- **Edible-use caution:** if condensate/greywater ever irrigates food, add pathogen treatment (open Q in [resource cycles](../../design/70-resource-cycles.md)).

## Open questions

- **RESOLVED:** Zones defined in [`80-zone-layout.md`](../../design/80-zone-layout.md) — ~6 drip latching-valve zones (IZ1–5, IZ8) + IZ6 recirculating hydro + IZ7 wicking fill. Bed counts within zones still TBD.
- **OPEN QUESTION:** Cistern + pure-tank + header sizing (ties autonomy calc, REQ-WATER-5).
- **OPEN QUESTION:** Header-tank elevation + structural support (construction-locked).

*Upstream: [`70-resource-cycles.md`](../../design/70-resource-cycles.md), [`50-passive-architecture.md`](../../design/50-passive-architecture.md). Format: [`README.md`](README.md). Related: [`controls.md`](controls.md) (valve drivers), [`off-grid-power.md`](off-grid-power.md).*
