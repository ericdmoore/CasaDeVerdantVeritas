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

## 2. Shade — the cheapest cooling is heat never admitted

- **Sliding solar louvers** — adjustable external shading that can track season/sun.
- **Fixed, geometry-tuned overhangs / awnings / light shelves** — sized to Dallas's **32.8 °N** sun angles to block high summer sun yet admit low winter sun. **The most foolproof shade device: nothing moves, nothing fails.** Pair with the louvers — fixed awning/overhang as the can't-fail baseline, louvers to fine-tune.
- **Deciduous living shade** — vines on a west/south trellis or a tree: leafs out for summer, drops for winter, self-regulating *and* a teaching feature. West side especially (brutal low afternoon sun).
- **Seasonal shade cloth / whitewash** ([REQ-LIGHT-1](10-requirements.md#c-shading--light)).

## 3. Water — passive irrigation survives a dead battery

- **Gravity-fed irrigation from an elevated header tank.** A raised rainwater tank drip-feeds by gravity, **no pump** — plants water even with the battery flat. The strongest water-side fool-proofing; pairs with the off-grid ethos. *(Elevation must be designed in now.)*
- **Wicking beds / sub-irrigated planters.** A reservoir below the root zone wicks on demand — buffers *days* untended. Arguably the best bed-level answer to the [summer-survival](../operate/sops/SOP-03-summer-survival.md) problem. ⚠️ Caveat: needs drainage design or it goes anaerobic; watch salt buildup.
- **Ollas** (buried porous clay pots) — ancient, passive, seep-on-demand; great for demo beds.

## 4. Freeze — the mild Dallas need

- **Black water drums along an insulated north wall** — classic passive-solar heat battery: soak sun by day, radiate through freeze nights. *Same water mass that buffers summer heat and stores irrigation water — one feature, three jobs.*
- **Insulated/reflective north wall + earth-berming** — cut winter loss, bounce light south (the passive-solar greenhouse archetype).

## 5. Thermal mass — the multi-season buffer

The **slab** ([REQ-SLAB-6](10-requirements.md#a2-foundation--slab--the-one-way-door)) plus **water containers** absorb daytime heat and release it at night, flattening every swing — summer comfort *and* freeze protection. The water mass triple-counts as irrigation buffer. *Open: how much mass to build in (drives slab/structure loading).*

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
