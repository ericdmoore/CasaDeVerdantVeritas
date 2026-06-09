# Resource Cycles — water harvesting & composting

*Closing the loops so the greenhouse produces as little waste as possible — the design embodiment of permaculture's **"produce no waste"** (the one gap the [permaculture review](00-design-principles.md) flagged). Two interlocking cycles — **water** and **nutrient** — that feed each other and the rest of the systems.*

> The design move that matters: stop thinking "rain barrel + compost pile," and design **two closed loops with explicit cross-connections.**

---

## Cycle 1 — Water: harvest by quality, not just quantity

Sources produce **different grades** of water; match grade to use, and store across **three elevations** so everything flows by gravity.

| Grade | Source | Stored at | Gravity-feeds |
|-------|--------|-----------|---------------|
| **Pure** | Condensation (distilled-grade) | **HIGH** (tower) | Evap pads (no scale) · battery top-up · sensitive hydro · fogger basin |
| **White (clean)** | Filtered rainwater **+ campus tether (air-gap)** | **HIGH** (tower) | Produce-wash sinks · hand-wash · clean irrigation |
| **Grey (reuse buffer)** | Wash-sink + fogger returns (settled + filtered) | **MEDIUM** | Root / non-edible drip — see *managed spill* ↓ |
| **Bulk** | Raw rainwater (roof + PV gutter) | **LOW** (cistern) | Pumped up → white tank |

> **Why three elevations:** the fresh tanks (white/pure) sit **HIGH** for head to the sinks; the **returns** (sink drains, fogger overflow) originate at bench height and can only be reused *pump-free* if the grey buffer sits **MEDIUM** — low enough to gravity-collect them, high enough to gravity-feed the (lower) beds.

**The condensation sleeper:** the greenhouse makes its own humidity that condenses on cool inner surfaces; twin/triple-wall polycarbonate has internal channels you can drain to an eave gutter. Mineral-free → *ideal* for evap pads, battery, hydro, and the fogger. Closes its own humidity loop (transpire → condense → recapture).

### Two water-handling principles

1. **Catch high, preserve head.** Capture returns (sink drains, fogger overflow) **at their source height** and gravity-cascade down — never drop water to the floor and then need to lift it. There's only a narrow vertical band between catch height (~36") and bed height (~24"), so every inch of head counts.
2. **Managed waterfall spill.** The medium grey **buffer** gives *optionality* (outlet valves actively send water to chosen beds/compost), and a **passive priority waterfall** handles the rest with zero controls: each stage fills, then *spills* to the next only when full. **Buffer → bed → bed → … → drain-line emitters → high-volume bypass to daylight.** Nothing wasted, nothing floods, no pump.

   **The bed-scale rule that makes it work — dedicated inlet + outlet, never one dual-purpose port.** A single fill/overflow port can't fill and define an overflow level at the same time, and it can't chain. Split them:
   - **Inlet** feeds the reservoir. **Outlet = an overflow standpipe set at the top of the reservoir** — *this* is the guarantee a bed can never overfill its top: the water line is set by the standpipe height, not by how much you pour in. Excess just leaves.
   - **Chain them: outlet(N) → inlet(N+1).** Each bed's overflow becomes the next bed's supply — a one-way waterfall, **never a bottom-to-bottom manifold** (that makes the reservoirs communicating vessels: levels equalize, per-bed overflow control is lost, back-siphon path opens).
   - **Head is the budget, not the pipe.** Bed N's overflow lip must sit above bed N+1's water line, so **stair-step the beds or step the standpipe heights down** bed-to-bed. With only ~12" between catch (~36") and bed (~24") height (↑ principle 1), the step-per-bed caps how many beds chain in one run before a fresh run must start from the buffer.
   - **Two failsafe tiers below the last bed:** its overflow feeds a **sloped drain line with emitters** (even the "waste" waters perimeter/swale plants); only if those emitters are maxed (everything soaked) does water back up to a **tee/standpipe higher on that line → a high-volume bypass to daylight** (swale / recharge). The bypass goes to daylight, *not* back to the grey buffer — when this tier fires the buffer is full too, so recirculating just chases its tail; route through the buffer only if the buffer itself has a daylight overflow.

```
returns (caught high) ─drop line─▶ GREY BUFFER (MEDIUM) ── valves: direct to beds/compost
rain → roof+PV → CISTERN(LOW) ──pump──▶ WHITE(HIGH) ──gravity──▶ sinks · clean irrigation
condensate ─▶ PURE(HIGH) ─▶ fogger · evap · battery · hydro          │ when full ▼
campus tether ─air-gap─▶ WHITE(HIGH)                       MANAGED WATERFALL SPILL
soil-catch + sediment ─────────────────────────▶ back to beds        ▼
                              bed1 IN→[overflow]→bed2 IN→[overflow]→…→bedN
                                                                     │ overflow
                                                          sloped drain line + emitters → perimeter/swale plants
                                                                     │ emitters maxed (all soaked) ▼
                                                          tee/standpipe → HIGH-VOLUME BYPASS → daylight: swale / recharge
```

Get right: **covered tanks** ([REQ-WATER-2](10-requirements.md#e-irrigation--water)); **engineered tower** for the HIGH tanks (heavy + wind sail — 🔴 Red, foundation pre-pour); **air-gap** tether fill = textbook backflow control ([REQ-WATER-4](10-requirements.md#e-irrigation--water)); white/grey **strictly separate + labeled**; **size the grey buffer for turnover** (modest — no stagnant greywater); managed spill **feeds soil**, not waste.

## Cycle 2 — Nutrient: four composting methods, each with a role

Active composting lives in an **outdoor service zone** — pests, pathogens, and disease pressure don't belong in the controlled growing house. Only the *finished* product comes back in.

| Method | Role | Notes |
|--------|------|-------|
| **Vermicompost (worms)** — *the anchor* | Continuous, education, **worm tea** liquid feed | **The low-maintenance backbone** — a big established bin runs itself for years with near-zero attention (keep the mass high, don't over-pull). Its **neglect-tolerance matches the summer-coverage gap**, so it's the primary method. ⚠️ **Site it COOL/stable** (north wall by thermal mass, shaded, low) — worms die above ~85–90 °F, so a sun-baked spot kills the very hardiness we want. |
| **Bokashi** | **Cafeteria-scrap pre-treatment** (incl. meat/dairy) | Sealed anaerobic ferment — fast, pest-free; output then feeds the hot pile / hügel beds. |
| **Hot compost** | Bulk plant waste + pre-treated scraps | Outdoor pile, 130–160 °F (optional minor winter warmth); needs turning + space. |
| **Hügelkultur beds** | **Water-storing beds that compost in place** | Buried wood core = water sponge; build-time decision. *Merges both cycles.* |

### The cafeteria loop (designed in)

Cafeteria scraps → **bokashi** (ferments tricky waste safely, no open pile) → **hot compost or buried in hügel/beds** → soil → food → **take-home** ("backpack Thursday"). Scraps come *in* for compost; produce goes *home* with students, **not back to the cafeteria** (see [growing program](../operate/30-growing-program.md) — avoids the district food-service hurdle).
⚠️ Cafeteria scraps likely need **health-dept / district sign-off** ([regulatory governance](../build/10-regulatory-governance.md)) and **sealed, rodent-proof handling**. Bokashi's sealed buckets are part of *why* this is manageable.

## How the cycles integrate — the loop closures

This is the whole point — the cross-connections, not the parts:

- **Compost / worm tea → fertigation** through the drip system (nutrient cycle feeds the water cycle's distribution).
- **Hügelkultur wood core → water storage** — one structure serving *both* cycles → fewer waterings → helps [summer survival](../operate/sops/SOP-03-summer-survival.md).
- **Condensate → distilled top-up** for batteries + evap pads (water cycle feeds the power + cooling systems).
- **Overflow → compost beds / swale** (no wasted water).
- **Cafeteria scraps → bokashi → soil → food → cafeteria** (civic loop).
- **Hot-compost heat** — optional passive winter warmth assist.

## And the hardware half of "produce no waste"

Our [design-around-failure + repairable/commodity ethos](30-electronics-and-controls.md#5-environmental-containers--commodity-hardware-over-rugged-hardware) already minimizes hardware waste. The honest end-of-life item: a **LiFePO₄ recycling plan** for the battery/cow at end of life — name the recycler now.

**Solar desiccant regeneration (reuse loop).** Enclosure desiccant (silica gel) is **reused, not discarded** — regenerated by heating to ~120 °C in a **box solar oven** (off-grid, free) in the outdoor service zone, then put back. A small produce-no-waste loop *and* a solar-thermal teaching demo (also handy for drying seeds/herbs). ⚠️ **Box oven, not a parabolic mirror** — concentrated solar is a burn/fire/eye hazard around kids; a box oven reaches regen temp without a focal point.

## Construction-locked elements (feed the slab/site/build)

Must be designed **before construction** — they touch structure, glazing, and the slab:
- **Header-tank elevation** (gravity head) and **cistern siting + overflow routing**.
- **Interior condensate gutter** (integrates with glazing detail + [slab drainage](../build/00-slab-prepour-checklist.md)).
- **PV array gutter** at the low edge.
- **Hügelkultur bed locations** + the outdoor compost service zone in the [site plan](20-site-and-orientation.md).

## Requirements

Turned into `REQ-CYCLE-*` in [`10-requirements.md`](10-requirements.md#o-resource-cycles).

## Open questions

> **OPEN QUESTION:** Health-dept / district sign-off path for the cafeteria-scrap loop.
> **OPEN QUESTION:** Edible-use water treatment — if condensate/greywater ever irrigates food, what pathogen control? (Keep condensate→non-edible or treat.)
> **OPEN QUESTION:** Sizing — cistern + pure-water tank volumes (ties [REQ-WATER-5](10-requirements.md#e-irrigation--water) autonomy), and compost throughput vs. the school's waste volume.
> **OPEN QUESTION:** LiFePO₄ recycler / end-of-life partner.

*Parent: [`00-design-principles.md`](00-design-principles.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-CYCLE), future `bom/water-harvesting.md` + compost-care SOPs. Related: [`50-passive-architecture.md`](50-passive-architecture.md) (gravity/wicking), [`60-power-architecture.md`](60-power-architecture.md) (condensate top-up).*
