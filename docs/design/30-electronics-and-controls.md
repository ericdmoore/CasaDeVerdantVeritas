# Electronics & Controls — design principles

*A sub-domain of the [whole-building design principles](00-design-principles.md), focused on the electronics that sense, decide, move, and report: sensors, the controller "core," fans and actuators, the off-grid power chain, alerting, and the data layer. These principles answer a narrower question — **how do we build electronics that a rotating crew of volunteers and students can trust, in a hot, wet, condensing greenhouse, off-grid, for years?***

> Same priority hierarchy as the parent doc (Safety → Education → Resilience → Production → Showcase). When these sub-principles conflict, that order still decides.

---

## 1. Hard to plug into the wrong connector (poka-yoke)

Make wrong connections *physically impossible*, not merely discouraged. Our maintainers are rotating volunteers and students, not a tech who knows the rig — so the hardware has to refuse the mistake.

- **Mechanical keying + distinct connector families** so DC power cannot seat in a data port, and 12 V cannot seat in a 5 V socket.
- **Color-code and label** by function (power / data / sensor / actuator).
- **One job per connector type.** If two cables *can* be swapped, eventually they *will* be.

## 2. Right connector for the context — and keep the wet boundary small

Connector grade follows the **local** environment. The greenhouse floor is wet, hot, and condensing; a sealed equipment box is not.

| Context | Connector | Why |
|---------|-----------|-----|
| Clean, dry run *inside* an enclosure | **RJ45 / PoE++ (802.3bt)** | Commodity, cheap, carries power **and** data on one cable to an edge node. |
| Exposed run across the wet/outdoor environment | **M12 X-coded** (IP67, shielded) | Sealed, vibration- and moisture-tough where it has to survive the real environment. |

> **The reconciliation with Principle 5:** M12 *is* the "rugged hardware" we otherwise avoid. The resolution is **minimize exposed runs** — commodity connectors live inside controlled micro-environments; sealed/industrial connectors appear *only* where a conductor must cross the wet boundary. The design goal is to make that boundary as small as possible.

## 3. Closer to the core, the more data and power are separated

It's a gradient, and the reason is **fault isolation**.

- **At the edge:** converge freely — one PoE++ cable delivering power + data to a sensor node is exactly right.
- **At the core:** separate, so a power fault can't corrupt data and a data fault can't brown out control.
- This is the electronics-layer expression of decisions already in the repo: the safety loop independent of the data layer ([REQ-ELEC-2](10-requirements.md#f-electrical--controls), [REQ-DATA-2](10-requirements.md#j-data--monitoring--the-optional-layer)) and the **Tier 1/2/3 load shedding** ([REQ-PWR-2..4](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)) — keeping Tier 1 power electrically separate is *what lets you shed Tier 3 without browning out the controller.*

## 4. Design around failure — assume it will fail, keep it reachable

Everything fails; plan for the swap, not the miracle.

- **Nothing critical buried, potted, or mounted where you need a ladder and two people.** Optimize for low **MTTR** — a volunteer swaps it in a weekend (ties to the slab [pull-strings + spare conduit](../build/00-slab-prepour-checklist.md), [REQ-SLAB-3](10-requirements.md#a2-foundation--slab--the-one-way-door), and the Op-8 spares shelf).
- **Design around *this* environment's failure modes:** corrosion, condensation ingress, UV embrittlement, rodent chew, connector fretting.
- **Modular + labeled + self-documenting** so the fix doesn't require the person who built it.

## 5. Environmental containers + commodity hardware over "rugged" hardware

Default to cheap, replaceable commodity electronics inside a well-managed sealed enclosure — *not* expensive rugged/industrial gear. Commodity = stocked anywhere = a volunteer can replace it (echoes [Design Principle 5](00-design-principles.md), [REQ-ELEC-3](10-requirements.md#f-electrical--controls)).

**The sharp edge:** the enclosure becomes a single point of failure, and a sealed box in a Dallas greenhouse cooks. The price of admission is disciplined enclosure design:

- **Thermal:** site it in shade / the cool zone, light/reflective color — never sun-bake it. A sealed dark box in full sun runs hotter than the greenhouse.
- **Condensation:** a breather/membrane vent (Gore-type) + desiccant — seal against liquid water but let vapor equalize.
- **Belt-and-suspenders:** conformal-coat the boards anyway.

> Without that discipline, "commodity in a box" fails *faster* than the rugged gear it replaced.

## 6. Low-voltage DC by default in wet / child-accessible zones

SELV (≤ ~48 V) DC is inherently safer around kids and water, and it's where the design already leans (solar-direct DC fans, DC sensors). Pairs with the GFCI requirement ([REQ-ELEC-1](10-requirements.md#f-electrical--controls)). Reserve line-voltage AC for where it's genuinely needed, well away from small hands and standing water.

## 7. Protect the core from surges

Off-grid PV + Texas thunderstorms = real surge exposure. A surge protective device (SPD) and a proper ground to shield the Tier 1 core is cheap relative to losing the brain — and a dead controller on a hot day is a survival problem, not just an inconvenience.

---

## Architecture these imply (sketch)

- **A clear "core" vs. "edge" split.** Core = the controller, the critical-loop power, alerting — separated, protected, serviceable, in a managed enclosure. Edge = sensor/actuator nodes reached over converged PoE++ where the run is clean, M12 where it's exposed.
- **A connector standard** (the table in Principle 2), keyed and color-coded per Principle 1, published so every future addition conforms.
- **Enclosure + micro-environment spec** per Principle 5 (rating, siting, breather, desiccant, thermal).

*These get turned into checkable rows as `REQ-CTRL-*` in [`10-requirements.md`](10-requirements.md#k-electronics--controls-architecture).*

---

## Open questions

> **OPEN QUESTION:** Choice of controller platform / "core" — and whether it's a single brain or a small safety controller (Tier 1) plus a separate program/data controller (Tier 3).
> **OPEN QUESTION:** Published connector standard — finalize the keyed/colored connector families and the RJ45-vs-M12 boundary map for the chosen floor plan.
> **OPEN QUESTION:** Enclosure siting — where is the cool, shaded, reachable home for the core box? (Feeds the floor plan and the slab conduit runs.)
> **OPEN QUESTION:** Grounding/SPD design for an off-grid system — coordinate with the PV/battery installer.

*Parent: [`00-design-principles.md`](00-design-principles.md). Sibling: [`40-network-and-connectivity.md`](40-network-and-connectivity.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-CTRL, REQ-ELEC, REQ-PWR, REQ-DATA).*
