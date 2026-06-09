# Passive Architecture — foolproof resilience by physics

*The architectural features that keep the greenhouse alive with **zero electricity, zero human attention** — the survival layer beneath the solar+battery system. A sub-domain of the [design principles](00-design-principles.md), and the physical embodiment of [Principle 3 (passive cooling is primary)](00-design-principles.md#3-designed-for-dallas-not-for-a-catalog-photo) and [Principle 4 (resilient when no one is watching)](00-design-principles.md#4-resilient-when-no-one-is-watching).*

---

## The test every feature must pass

> **The best passive features self-regulate by physics and scale *with* the stressor.** The solar chimney pulls harder the hotter it gets. Deciduous shade arrives exactly in summer. They need no power, no human, and no decision — the worse conditions get, the harder they work.

A second filter: **most must be built *into* the structure/slab**, not bolted on later — same one-way-door logic as the [slab](../build/00-slab-prepour-checklist.md). This is a *decide-during-construction* list.

These sit at the base of the resilience stack: **passive (always) → solar+battery (normal) → [campus tether](00-design-principles.md#project-constraints-decided) (emergency).**

---

## 1. Air turnover & cooling — the dominant need

- **Solar chimney (thermal stack).** A tall, dark/glazed absorber stack; sun heats it, buoyancy drives exhaust, fresh air pulled through low intakes. **Scales with the heat load** — the hotter the day, the stronger the draw. The flagship feature. *Cost: height = wind load + structure.*
- **Earth-tube / ground-coupled intake.** Intake air drawn through buried pipe (or an under-slab plenum) is pre-cooled by stable ~68–72 °F TX subsoil. **Killer synergy:** let the solar chimney's draw pull air *through* the earth tubes → a fully passive cool-air loop, no fan. ⚠️ **Caveat (open decision):** in humid Dallas, earth tubes risk condensation/mold (and radon) — they need slope-to-drain, smooth antimicrobial pipe, and cleanouts, *or skip them.* See open questions.
- **Wax-piston auto-vents** (ridge/gable) — non-electric openers that crack on rising temperature ([REQ-COOL-4](10-requirements.md#b-cooling--ventilation--the-headline-system)); the chimney's foolproof valving.
- **Stack-effect geometry** — tall ridge, low intakes; design the building *section* for buoyancy-driven flow. Height is the lever.
- **High-albedo / reflective roof surfaces** — reject solar gain before it enters.

### Two exhausts, one driver at a time — the mode-switch ([REQ-COOL-9/10](10-requirements.md#b-cooling--ventilation--the-headline-system))

Buoyancy and wind both want to create a low-pressure zone up top, but they peak at **opposite times** and, if you let both top openings exhaust at once, they fight: they share one internal pressure node, the weaker one reverses, and the two high openings short-circuit air *between themselves* — bypassing the canopy. So run **two purpose-built high exhausts and only ever one at a time:**

| | **Solar chimney (tall)** | **Wind-capped ridge vent (lower, long)** |
|---|---|---|
| Driver | Buoyancy | Wind / venturi |
| Why this height | Stack ΔP scales with height → give the **weak** driver max height | Long distributed area along the ridge |
| Regime | **High-pressure, low-volume** | **High-volume, lower-pressure** |
| Wins when | **Still + hot** (no wind to drive anything else) | **Breezy** (wind suction ~10 Pa ≫ buoyancy ~1–5 Pa) |

They're not redundant — they're tuned for different flow regimes, and **low intakes stay open in both modes** so the canopy is flushed vertically either way; only the driver and the outlet change. Why this beats one venturi-capped chimney: buoyancy is pressure-limited (needs the tall flue, moves modest volume); wind has pressure to spare but you want *volume* — the long ridge delivers it.

**The five rules that keep it honest:**
1. **The inactive exhaust is positively closed.** The chimney baffle *is* the mode valve (and doubles as the winter heat-retention damper). Leave it cracked in wind mode and you reintroduce the short-circuit.
2. **Fail to the passive thermal default, not a fixed position.** Heat is the lethal failure here (Principle 3); a stuck-open vent in a mild Dallas freeze is the minor one — so the bias is *when in doubt, dump heat.* But "fail all-open" bleeds heat on a winter night, so the de-energized layer is **wax-piston auto-openers** (↑): open-when-hot / closed-when-cold, zero power, no decision. The powered mode-switch is an **optimization layer on top**, never what keeps the plants alive.
3. **Temperature gates venting; wind only selects the path.** Interior temp decides *whether* to vent; windspeed decides *which* exhaust. (Earlier worry — "don't gate cooling on windspeed" — resolved: windspeed never closes the system, it just picks chimney vs. ridge.)
4. **Switch on a dwell timer (~15 min) with an emergency-override.** Matches the structure's thermal lag and spares the actuators; but if interior temp blows past a hard ceiling mid-dwell, recompute *now* — don't let the timer trap a failing mode during a spike.
5. **Omnidirectional cap + wind *direction*, not just speed.** A directional cap only suctions from its prevailing quarter, so windspeed alone can read "windy" while the venturi is dead. Sense direction too and use an omnidirectional cowl.

**Site geometry (favorable, and it closes rule 5):** Dallas sun is south → the large glazed roof face is **south**, the **ridge runs E–W**, and the chimney sits at the **west end** of the ridge. Prevailing **S/N** winds cross the ridge crest *perpendicular* — the ideal ridge-venturi angle (an N–S ridge would barely venturi) — and put the west-end chimney *beside*, not upwind of, the ridge flow, so no wind-shadow. The one angle that would shadow the cap is a due-**west** wind down the ridge line; that's exactly where the wind-direction input earns its keep — on west winds the controller falls back to stack mode. Bonus: the west chimney soaks the brutal low **afternoon** sun → peak buoyancy right when the afternoon heat peaks.

> **Build-locked vs. tunable:** chimney position, ridge orientation, and intake locations are **construction-locked**; the windspeed crossover, dwell time, and which exhaust is the fail-default are **commissioning-tunable** software knobs — don't mistake the knobs for one-way doors. Commission with the wax-piston thermal default, watch which exhaust actually carries the load, and reassign from data.

## 2. Shade — the cheapest cooling is heat never admitted

- **Sliding solar louvers** — adjustable external shading that can track season/sun.
- **Fixed, geometry-tuned overhangs / awnings / light shelves** — sized to Dallas's **32.8 °N** sun angles to block high summer sun yet admit low winter sun. **The most foolproof shade device: nothing moves, nothing fails.** Pair with the louvers — fixed awning/overhang as the can't-fail baseline, louvers to fine-tune.
- **Deciduous living shade** — vines on a west/south trellis or a tree: leafs out for summer, drops for winter, self-regulating *and* a teaching feature. West side especially (brutal low afternoon sun).
- **Seasonal shade cloth / whitewash** ([REQ-LIGHT-1](10-requirements.md#c-shading--light)).

> **Decided — the south face is a deciduous-vine ramada (the [Covered Outdoor Instruction Area](80-zone-layout.md#schematic-plan)).** A full-length, open-sided Spanish-style ramada runs along the south wall: timber/steel posts, a **latilla (open-slat) top, and a deciduous vine** trained over it. One structure, three jobs — the **primary "teach-outside" gathering space** ([Group U](../build/10-regulatory-governance.md#-the-decision-that-governs-everything-occupancy-classification)-preserving), the **south shade device**, and it **pre-cools the breeze intake** (the low intakes draw shaded air, not sun-baked air).
>
> **The latillas and the vine do different jobs — keep them honest:** fixed latillas shade *year-round* (they don't know it's January), so on their own a dense slat roof would over-shade the south beds exactly when we want the low 34° winter sun. **The deciduous vine is the part that self-regulates** — bare in winter, low sun rakes through the open slats; leafed-out in summer, full dapple. Keep the latilla spacing open-ish and let the vine be the seasonal valve. **Open sides are non-negotiable** — a solid-walled lean-to would dam the S/SSE breeze the cooling design depends on (and risk pushing past Group U). The **roll-up south wall stays the operable membrane** between interior and the covered classroom.
>
> **Vine shortlist (Dallas 8a/8b, kids underneath — deciduous, tough, safe/teachable):**
> - **Grape** (*Vitis* — Pierce's-disease-tolerant: muscadine, 'Black Spanish/Lenoir', 'Blanc du Bois') — **the pick.** Classic ramada vine, dense summer shade, **edible** (food + teaching missions), non-toxic, on-theme. *PD is endemic in the South — choose PD-tolerant stock.*
> - **Passionflower / Maypop** (*Passiflora incarnata*) — TX native, edible fruit, spectacular flowers, **host plant for Gulf Fritillary butterflies** (caterpillar-to-butterfly lesson). Herbaceous — dies back fully (maximal winter light) and rebuilds each spring, so pair with a woody backbone.
> - **American wisteria** (*Wisteria frutescens*) — native and well-behaved (*not* the structure-crushing invasive Asian wisterias), lovely blooms. ⚠️ seeds/pods **toxic if eaten** — only if pods can stay above grabbing height.
> - **Virginia creeper** (*Parthenocissus quinquefolia*) — native, bulletproof, brilliant red fall color. ⚠️ berries **toxic** (oxalates) — same site-it-high caveat.
>
> **Recommendation:** **grape** as the primary woody canopy (safe, edible, on-theme), optionally **interplant passionflower at one bay** for the butterfly/pollinator lesson — food, shade, and a living curriculum from one structure. *Build note: the posts are a slab one-way-door — footings/anchors in the [slab pre-pour checklist §5](../build/00-slab-prepour-checklist.md).*

## 3. Water — passive irrigation survives a dead battery

- **Gravity-fed irrigation from an elevated header tank.** A raised rainwater tank drip-feeds by gravity, **no pump** — plants water even with the battery flat. The strongest water-side fool-proofing; pairs with the off-grid ethos. *(Elevation must be designed in now.)*
- **Wicking beds / sub-irrigated planters.** A reservoir below the root zone wicks on demand — buffers *days* untended. Arguably the best bed-level answer to the [summer-survival](../operate/sops/SOP-03-summer-survival.md) problem. ⚠️ Caveat: needs drainage design or it goes anaerobic; watch salt buildup.
- **Ollas** (buried porous clay pots) — ancient, passive, seep-on-demand; great for demo beds.

## 4. Freeze — the mild Dallas need

- **Black water drums along an insulated north wall** — classic passive-solar heat battery: soak sun by day, radiate through freeze nights. *Same water mass that buffers summer heat and stores irrigation water — one feature, three jobs.*
- **Insulated/reflective north wall + earth-berming** — cut winter loss, bounce light south (the passive-solar greenhouse archetype).

## 5. Thermal mass — the multi-season buffer

The **slab** ([REQ-SLAB-6](10-requirements.md#a2-foundation--slab--the-one-way-door)) plus **water containers** absorb daytime heat and release it at night, flattening every swing — summer comfort *and* freeze protection. The water mass triple-counts as irrigation buffer. *Open: how much mass to build in (drives slab/structure loading).*

> **Considered & rejected — solar Trombe wall.** A Trombe wall is a *heating* device, wrong for a **cooling-dominant** greenhouse: it adds heat we spend the season removing, and it wants the **south face** — which is our glazed, light-admitting wall for the *plants* (a masonry Trombe wall there steals their light). Our minimal freeze-night need is already met by the **internal water-barrel thermal mass** (buffers, doesn't net-add heat; doesn't block south light). *(A fan-driven vented Trombe could summer-vent to outside, but the south-light conflict still sinks it here.)*

## 6. Structural fail-safes

- **Gravity/counterweight-default vents** — fail *open* mechanically when an actuator dies (the physical form of the [fail-open rule](10-requirements.md#b-cooling--ventilation--the-headline-system)).
- **Manual override on every powered system** — hand crank for vents, manual valve for irrigation. The tool-free last resort.

---

## Requirements

Turned into checkable rows as `REQ-PASV-*` in [`10-requirements.md`](10-requirements.md#m-passive-architecture).

## Which are construction-locked (feed the slab/build)

Earth tubes (under-slab), thermal-mass loading, the solar chimney, header-tank elevation, and overhang geometry must all be designed **before construction** — they touch the structure and the [slab pre-pour checklist](../build/00-slab-prepour-checklist.md).

## Open questions

> **OPEN QUESTION:** **Earth tubes — in or out?** The humid-Dallas mold/condensation/radon risk is real; only include if engineered out (slope, antimicrobial pipe, cleanouts). Lean: *start without; revisit if passive cooling proves insufficient.*
> **OPEN QUESTION:** **Thermal-mass quantity** — how much slab + water mass to build in, traded against structural loading and cost.
> **OPEN QUESTION:** Solar-chimney dimensions/placement vs. the final floor plan, orientation, and wind loads.
> **OPEN QUESTION:** Header-tank elevation + location for gravity irrigation (structure + the rainwater system).

*Parent: [`00-design-principles.md`](00-design-principles.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-PASV, REQ-COOL, REQ-WATER), [`../build/00-slab-prepour-checklist.md`](../build/00-slab-prepour-checklist.md).*
