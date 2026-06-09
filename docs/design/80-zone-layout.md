# Zone Layout — the floor plan

*Where everything goes. This is the synthesis doc — it lands every system (growing, passive, power, water, controls) in physical space, and it's the **keystone that unblocks the BOMs and the slab.** Finalizing it satisfies [REQ-SLAB-1](../build/00-slab-prepour-checklist.md) (floor plan before pour) and sets the irrigation-zone and device counts the [controls](../build/bom/controls.md) and [irrigation](../build/bom/irrigation.md) BOMs need — which in turn yield the Tier 1/2/3 load list the [power BOM](../build/bom/off-grid-power.md) waits on.*

> **Status:** 🟡 Schematic v1. Arrangement is *relative to orientation*; absolute positions firm up once [site & orientation](20-site-and-orientation.md) and exact dimensions are set. **Decided:** balanced **soil beds + a hydroponic demo**; gathering **both** — a **full-length covered south ramada** (primary) + a small indoor nook. **Decided:** the south shade is a **deciduous-vine ramada** = the Covered Outdoor Instruction Area ([passive §2](50-passive-architecture.md#2-shade--the-cheapest-cooling-is-heat-never-admitted)); solar chimney sits at the **west end** of the ridge.

---

## The layout logic (what drives the arrangement)

Working assumption: **~20 × 40 ft, E–W long axis**, broad south face ([site rec](20-site-and-orientation.md)). The plan follows five rules:

1. **Light gradient** — full-sun crops on the **south** side; shade-tolerant + work zones to the **north** ([REQ-EDU-1](10-requirements.md#i-education--layout)).
2. **One-glance supervision** — a **central circulation spine** so one adult sees the whole interior ([REQ-EDU-3](10-requirements.md#i-education--layout)); ADA-width (≥ 48").
3. **Passive airflow** — **south roll-up sides = breeze intake**; **north wall = insulated/reflective + thermal-mass water drums**; **ridge vent + solar chimney = exhaust** ([REQ-COOL](10-requirements.md#b-cooling--ventilation--the-headline-system), [REQ-PASV](10-requirements.md#m-passive-architecture)).
4. **Teach outside, grow inside** — a **full-length Covered Outdoor Instruction Area** (a Spanish-style ramada along the south face) is the primary gathering space, keeping a class *out* of the interior to preserve the light-touch **Group U** classification ([regulatory](../build/10-regulatory-governance.md#-the-decision-that-governs-everything-occupancy-classification)). It pulls **double duty as the south shade device** — see [passive §2](50-passive-architecture.md#2-shade--the-cheapest-cooling-is-heat-never-admitted).
5. **Infra cool, shaded, out of reach** — controls enclosure and power gear sited in the coolest/shaded corner ([REQ-CTRL-5](10-requirements.md#k-electronics--controls-architecture)), never at child height.

## Schematic plan

```
                  N — insulated/reflective wall + ▓ thermal-mass water drums ▓
  ┌──────────────────────────────────────────────────────────────────┬─────────┐
  │ ▓▓▓▓▓▓▓▓▓▓▓▓▓ thermal-mass water drums (north wall) ▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │ CONTROLS│
  │ [worm    [work +   [potting +   [repotting  [seedling /            │ ENCL.   │
  │  window]  tool wall] soil-catch]  station]   propagation IZ5]      │ (high,  │
  │ ·········· tall-crop trellis ARCH over spine (walk-under) ········· │  shaded)│
  │ ════════ central ADA circulation spine (≥48", one-glance) ════════ ├─────────┤
  │ [BED K][BED 1][BED 2][BED 3][BED 4][BED 5: ADA ht + root window]    │ DATA /  │
  │  └──── 6 grade SIP beds — grey-buffer waterfall fill ────┘ [hydro   │ research│
  │                                                            IZ6 demo]├─────────┤
  │ ~~~~~~~~~~~~ south roll-up sides (breeze intake) ~~~~~~~~~~~~~~~~~~~ │ ENTRY / │
  └──────────────────────────────────────────────────────────────────┤ AIRLOCK │
  ╔══════════════════ COVERED OUTDOOR INSTRUCTION AREA ════════════════╧══(ADA)══╝
  ║ full-length Spanish ramada · open sides · latilla top · deciduous grapevine  ║
  ║ (dappled summer shade, bare for winter light) · IZ8 planters · class gather  ║
  ╚══════════════════════════════════════════════════════════════════════════════╝
                  S — sun + prevailing breeze (ramada pre-shades the intake air)

  Ridge vent runs the full E–W length; SOLAR CHIMNEY at the WEST end of the ridge.
  Service end (E): header + pure-tank tower (HIGH) · grey buffer (MED, by beds) ·
  cistern (LOW, outside) · power / cow dock.   Indoor calm/sensory nook: SW corner.
```

*Schematic only — proportions not to scale. Mirror E↔W to suit the real entry approach from campus.*

### Section — why the south ramada cools without stealing winter light

The dappled-light tension lives in the *vertical* geometry (Dallas 32.8 °N: summer noon ≈ 80°, winter noon ≈ 34°):

```
   SECTION — looking west          N ◄──────────────────────► S
                                                  ☀ SUMMER ≈80°  ✗ caught by canopy
            ┌──── ridge vent ────┐                       │
   N WALL   │  (solar chimney at  │                       ▼
   ▓drums▓  │   the WEST end ↙)   │                ☀ WINTER ≈34°  ╲
   ┌─────┐  └─────── interior ────┘   ┌──────┐              ╲      ╲ slips under →
   │ N   │      ⌒ trellis arch ⌒      │ SOUTH│  roll-up      ╔══════╲═══════════════╗
   │beds/│        ADA spine           │ beds │   S wall  →   ║ ░ deciduous vine ░    ║
   │bench│                            │K–5SIP│  (membrane)   ║ ░ COVERED OUTDOOR ░   ║
   └─────┘                            └──────┘               ║   INSTRUCTION AREA    ║
   ══════════ slab + water = thermal mass ══════════════════╩══ open-sided on-grade ═╝
        breeze ↗ enters low — already SHADED & pre-cooled by the canopy ──► up & out ↑
```

- **Summer (leafed-out):** the vine canopy catches the near-overhead sun → shades both the pad *and* the glazing, and the air pulled into the low intakes is **pre-cooled, shaded air** (the same free-synergy logic as the earth-tube intake).
- **Winter (bare):** low southern sun rakes *under* the bare canopy and through the roll-up wall to the south beds — the deciduous habit is the self-regulating valve, not a setting anyone adjusts.
- **Always:** open sides keep the breeze path to the intakes and keep it reading as a shade structure (light-touch **Group U**); the roll-up south wall is the operable membrane between interior and the covered classroom.

## Zones

> **Bed model (decided):** the primary growing is **6 elevated 4×8 SIP beds — one per grade (K–5)**, free-standing islands (4-ft width needs both-side access), ~360 sq ft footprint. See the [bed & device schedule](90-bed-and-device-schedule.md). The IZ table below is the *earlier* zone framing; grade beds are the authoritative bed count.

### Growing zones → irrigation zones (this sets the valve count)

| ID | Zone | Location / why | Irrigation |
|----|------|----------------|-----------|
| **IZ1** | South in-ground soil beds | Best light; hands-in-dirt | Drip, latching valve |
| **IZ2** | South raised soil beds | Light + back-friendly | Drip, latching valve |
| **IZ3** | North raised beds | Shade-tolerant crops | Drip, latching valve |
| **IZ4** | ADA wheelchair-height bed | Accessible participation ([REQ-ACC-2](10-requirements.md#h-accessibility--inclusion)) | Drip, latching valve |
| **IZ5** | Germination / propagation bench | Work height; optional grow light | Fine/low-flow line |
| **IZ6** | Hydroponic demo | Research/contrast; EC/pH | **Recirculating** (own loop, off the drip manifold) |
| **IZ7** | Wicking beds | Multi-day untended buffer | **Sub-irrigated** (separate fill) |
| **IZ8** | Outdoor ramada planters | Edge growing; demo (under the Instruction Area) | Drip / hose-bib |

→ **~6 drip latching-valve zones (IZ1–5, IZ8) + 1 recirculating (IZ6) + 1 wicking fill (IZ7).** This is the count the [irrigation BOM](../build/bom/irrigation.md) needs.

### Functional & infrastructure zones

| Zone | Where | Notes |
|------|-------|-------|
| Entry / airlock | One end (campus-facing) | ADA entry; door never locks occupants in ([REQ-SAFE-1](10-requirements.md#g-safety--egress)) |
| Central circulation spine | Length of interior | ADA + sightline ([REQ-EDU-3](10-requirements.md#i-education--layout)) |
| Indoor flexible nook / calm-sensory | South corner | Bad-weather gathering + [REQ-ACC-3](10-requirements.md#h-accessibility--inclusion) calm zone |
| **Covered Outdoor Instruction Area** (full-length S ramada) | Attached along the south face, open-sided | **Primary** instruction (Group U preserving); doubles as the south shade device + pre-cools the breeze intake. Deciduous-vine ramada ([passive §2](50-passive-architecture.md#2-shade--the-cheapest-cooling-is-heat-never-admitted)); posts anchor to the slab ([slab §5](../build/00-slab-prepour-checklist.md)) |
| Data / research corner | Interior, near power | Sensors hub, dashboards ([REQ-DATA](10-requirements.md#j-data--monitoring--the-optional-layer)) |
| Work / potting | North, mid | Child + one ADA height ([REQ-EDU-2](10-requirements.md#i-education--layout)) |
| **Tool / storage wall** | By work zone + entry | Shadow-board/French-cleat wall + class-set caddies + lockable cabinet ([REQ-STR-7](10-requirements.md#a-structure--envelope)); kid-height + ADA |
| Controls enclosure | Cool/shaded corner, high | [REQ-CTRL-5](10-requirements.md#k-electronics--controls-architecture); out of reach |
| Water infra | Service end | **HIGH** white+pure tanks (tower); **MEDIUM** grey reuse buffer (catches returns, feeds beds — *managed spill*); **LOW** cistern outside. Narrow head band: catch ~36" → beds ~24" |
| Power / cow dock | Near entry | Cow rolls out for events; fixed reserve stays ([REQ-PWR-8](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)) |
| Thermal mass | North wall | Water drums ([REQ-PASV-6](10-requirements.md#m-passive-architecture)) |
| Solar chimney + ridge vent | **Chimney at the W end** of the E–W ridge; ridge vent runs full length | Passive exhaust ([REQ-PASV-2](10-requirements.md#m-passive-architecture), [passive §1](50-passive-architecture.md#1-air-turnover--cooling--the-dominant-need)) |

### Built-in educational features — *construction-locked*

From the science/garden teacher ([growing program](../operate/30-growing-program.md)). Each is designed *into* a bed/structure now — **one-way door** ([REQ-EDU-5](10-requirements.md#i-education--layout)):

| Feature | What / where | Build note |
|---------|--------------|-----------|
| **Root window** | Below-grade viewing glazing into a raised bed — taproot vs. fibrous, potatoes | Built into the bed wall; drainage + viewing pane |
| **Worm window** | Cutaway view into the vermicompost bin (*the anchor compost method*) | Viewing pane; site **cool/stable** — north wall by thermal mass, shaded, low (worms die >85–90 °F) |
| **Hydroponic demo** | Small-scale, **visible reservoir** (IZ6) | Clear reservoir; own loop |
| **Data station** | Sensors + dashboard made visible (data corner) | Power/data drops ([REQ-SLAB-3](#a2-foundation--slab--the-one-way-door)) |
| **Tall-crop trellis** | Walk-under climbing-crop arch over the spine | Anchored to structure/slab |
| **Seedling station** | Germination bench + grow lights (IZ5); **humidity domes + a DC ultrasonic fogger** in a **float-valve constant-level basin** (pure-tank-fed, covered, overflow→irrigation) | Power + water + drainage; fogger is Tier-3/HA-controllable |
| **Repotting station** | Work bench, child + ADA height | Water + drainage nearby |
| **Soil-catch potting table** | Table with an integrated **hole + catchment** to scrape soil into → returned to beds | Drain to soil-catch; closes the soil loop |
| **Aquaponics rough-in** | *Future* — stub plumbing + space/structural allowance near a future fish-tank spot | Roughed-in now, built later (like spare conduit) |

## What this unblocks
- **Slab** ([REQ-SLAB-1](../build/00-slab-prepour-checklist.md)) — drains, conduit, plumbing stub-ups, anchors **and the built-in features above** all place off this plan.
- **Irrigation BOM** — ~8 zones → valve/line counts.
- **Controls BOM** — sensors/actuators per zone → device counts → **Tier 1/2/3 load list** → unblocks the **power BOM** sizing.

## Open questions
> **OPEN QUESTION:** Final site orientation + exact dimensions → absolute positions, mirror direction, door location.
> **OPEN QUESTION:** Bed count/size within each zone → exact IZ valve count and growing area.
> **OPEN QUESTION:** Is the cistern inside the footprint or external? (Affects slab + the 800 sq ft budget.)
> **OPEN QUESTION:** Header-tank support structure + height for adequate gravity head.

*Parent: [`00-design-principles.md`](00-design-principles.md). Synthesizes: [`20-site`](20-site-and-orientation.md), [`50-passive`](50-passive-architecture.md), [`60-power`](60-power-architecture.md), [`70-cycles`](70-resource-cycles.md). Feeds: [`../build/00-slab-prepour-checklist.md`](../build/00-slab-prepour-checklist.md), [`../build/bom/`](../build/bom/).*
