# Resource Cycles — water harvesting & composting

*Closing the loops so the greenhouse produces as little waste as possible — the design embodiment of permaculture's **"produce no waste"** (the one gap the [permaculture review](00-design-principles.md) flagged). Two interlocking cycles — **water** and **nutrient** — that feed each other and the rest of the systems.*

> The design move that matters: stop thinking "rain barrel + compost pile," and design **two closed loops with explicit cross-connections.**

---

## Cycle 1 — Water: harvest by quality, not just quantity

Sources produce **different grades** of water; match grade to use, and store in **four tiers** (three elevated for gravity feed).

| Grade | Source | Stored in | Gravity-feeds |
|-------|--------|-----------|---------------|
| **Pure** | Condensation (distilled-grade) | Small pure tank (elevated) | Evap pads (no scale) · battery top-up · sensitive hydro |
| **White (clean)** | Filtered rainwater **+ campus tether (air-gap)** | **Elevated white tank** | Produce-wash sinks · hand-wash · clean irrigation |
| **Grey (reuse)** | Wash-sink runoff (settled + filtered) | **Elevated grey tank** | Root / non-edible drip only |
| **Bulk** | Raw rainwater (roof + PV gutter) | Cistern (low/ground) | Pumped up → white tank |

**The condensation sleeper:** the greenhouse makes its own humidity that condenses on cool inner surfaces; twin/triple-wall polycarbonate has internal channels you can drain to an eave gutter. Mineral-free → *ideal* for evap pads, battery, and hydro. Capturing it **closes the greenhouse's own humidity loop** (transpire → condense → recapture).

**The wash-sink loop:** rinsing soil off harvested veg makes *light* greywater (just water + dirt). **Settle → screen-filter → grey tank → root irrigation**; the settled soil + the **potting-table soil-catch** both go **back to the beds**. Water *and* soil returned. (Keep reuse off raw-edible parts; plant-safe soap only.)

```
rain → roof + PV → first-flush/screen → CISTERN ──(pump)──┐
condensate ───────────────────────────────▶ PURE tank    │
campus tether ──air-gap──▶ WHITE tank ◀───────────────────┘  ─(gravity)─▶ sinks · clean irrigation
wash sinks → settle → filter → GREY tank ──(gravity)──▶ root/non-edible drip
soil-catch + settled sediment ─────────────────────────▶ back to beds
overflow ───────────────────────────────────────────────▶ swale / compost / recharge
```

Get right: **covered tanks** ([REQ-WATER-2](10-requirements.md#e-irrigation--water)); **gravity head** from elevated tanks ([REQ-PASV-4](10-requirements.md#m-passive-architecture)) on an **engineered tower** (heavy + wind sail — 🔴 Red, foundation pre-pour); **air-gap** tether fill = textbook backflow control ([REQ-WATER-4](10-requirements.md#e-irrigation--water)); white/grey **strictly separate + labeled**; **overflow feeds soil/compost**, not waste.

## Cycle 2 — Nutrient: four composting methods, each with a role

Active composting lives in an **outdoor service zone** — pests, pathogens, and disease pressure don't belong in the controlled growing house. Only the *finished* product comes back in.

| Method | Role | Notes |
|--------|------|-------|
| **Vermicompost (worms)** | Continuous, education, **worm tea** liquid feed | Low odor, small footprint, near year-round. The kid favorite. |
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
