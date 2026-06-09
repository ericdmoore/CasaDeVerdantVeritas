# Network & Connectivity — design

*A sub-domain of [electronics & controls](30-electronics-and-controls.md): how the sensors, actuators, controller core, and the outside world talk to each other. The greenhouse runs an internal network of devices orchestrated by **Home Assistant (HA)**, with an external uplink for alerts and remote access, and a visitor-friendly way to see local data on a phone.*

> Same priority hierarchy as the [parent principles](00-design-principles.md): Safety → Education → Resilience → Production → Showcase.

---

## 0. The rule that governs everything: HA is *not* the safety system

The most important constraint before any topology. The safety loop is independent of the data layer ([REQ-ELEC-2](10-requirements.md#f-electrical--controls), [REQ-DATA-2](10-requirements.md#j-data--monitoring--the-optional-layer)) and HA-class orchestration is **Tier 3, sheddable** ([REQ-PWR-4](10-requirements.md#f2-off-grid-energy--solar--battery-no-utility)). Networking must honor that:

- **Overtemp→vent, irrigation, and the high-temp alarm run with HA crashed, the LAN down, and the internet out.** That logic lives on-device (e.g. ESPHome local automations) or on a dedicated tiny safety controller — *never* only in an HA automation.
- HA does what it's good at: dashboards, scheduling, history, remote access, alerting — **convenience and observability, not survival.**

> If you take one thing from this doc: *the network dying must never be able to cook the greenhouse.*

## 1. External uplink — size it to the alert, not the dashboard

Local-first means the greenhouse fully works offline. The *one* external function that truly matters is **getting an alert to a phone**. So size the critical uplink to that, and let the heavy remote-dashboard traffic be sheddable.

| Option | Verdict |
|--------|---------|
| **Own cellular (LTE)** | **Recommended primary.** Independent, matches the off-grid ethos, cheap IoT/M2M data for telemetry, works anywhere with coverage. Costs a few watts continuous — a load line on the power BOM. |
| **School WiFi** | Secondary *only if* DISD IT formally allows it (IoT/guest VLAN). Expect friction: security policy, content filtering, captive portals, weak coverage at the campus edge, and you inherit their outages. Don't design around it. |
| **Neighbor WiFi (piggyback)** | Dropped. Unauthorized is off the table; even with permission it's fragile and not ours. |
| **Satellite (Starlink)** | Last resort only. ~50–75 W continuous **fights the off-grid battery** on a cloudy stretch. Unnecessary given Dallas cellular coverage. |

**Critical-alert resilience:** the safety controller should have a **minimal, low-power alert channel** (even SMS) that survives independently of the full HA + AP stack — so the failure mode *"the network powered down to save the battery, so no one got warned"* can't happen.

## 2. Segment the network — kids, the public, and a QR invite

This network is exposed to children, a public showcase, and phones we *invite* to join. Segment accordingly:

- **IoT / control segment** — sensors and actuators; no internet except what HA brokers.
- **Guest segment** — the QR network; **read-only**, client-isolated, can *see* dashboards but **never reach an actuator**.
- **Core** — HA, critical-loop power, alerting.

**Never port-forward HA to the internet.** Remote access via an outbound tunnel only (HA Nabu Casa — which also funds the project — or self-hosted Tailscale/WireGuard). Change every default credential.

## 3. Network gear is a continuous off-grid load — split it by tier

Router + AP + cellular modem + HA host run 24/7 (~15–25 W continuous — real over a cloudy stretch). So:

- **Tier 1/2 (survives):** the low-power critical-alert path.
- **Tier 3 (sheds gracefully):** full HA, the access point, the dashboards, remote access.

Each of these is a line item on the [off-grid power BOM](../build/bom/off-grid-power.md).

## 4. Design the network to fail and recover itself

Echoes [electronics Principle 4](30-electronics-and-controls.md#4-design-around-failure--assume-it-will-fail-keep-it-reachable):

- **Watchdog / scheduled power-cycle** for HA and the modem — they hang.
- **Real-time clock (RTC).** Off-grid + maybe no internet = NTP may be absent, and irrigation/vent schedules need reliable time. Clock drift is a silent killer.
- **SSD, not an SD card, for HA.** SD-card corruption is *the* classic HA death — straight violation of design-around-failure.
- **Monitor the monitors:** HA alerts when a sensor node drops offline, so silent failures surface (this is what the weekly "trust but verify" SOP checks by hand — automate it).

## 5. Transport: as few as the physics needs — band-diverse, each earning its keep

Not one radio, and not five. The [tiered operating model](../operate/10-roles-and-tiers.md) changes the old "keep it to one radio" rule: 🟢 **Green never sees the radios**, 🟠 **Amber can run several**, and the [heartbeat/reachability diagnostic](10-requirements.md#l-network--connectivity) makes the transport under a node nearly irrelevant to fault-finding. So the constraint moves from *simplicity* to *physics + cost*.

> ✅ **Locked transport stack (2026-06-08):** wired **PoE/Ethernet** backbone · **Zigbee** 2.4 GHz mesh (Thread-capable 802.15.4 hardware) · **LoRa/sub-GHz** for far + canopy nodes · **WiFi** for powered aggregators + camera.

- **Wired PoE/Ethernet backbone** (the [M12/RJ45 connector standard](30-electronics-and-controls.md#2-right-connector-for-the-context--and-keep-the-wet-boundary-small)) for the reliable, powered core and key actuators. **Wired-first** — radio only where wiring can't reach.
- **One 2.4 GHz mesh** (**Zigbee** now; Thread/Matter later on the same 802.15.4 hardware) for distributed in-greenhouse sensors near mains routers.
- **Sub-GHz / LoRa** for **far or canopy-buried outdoor nodes** — rain cistern, weather station, outdoor beds — where 2.4 GHz can't penetrate wet foliage or reach the distance. (Sub-GHz penetration is real: **water absorbs 2.4 GHz**.)
- **WiFi (ESP32/ESPHome)** reserved for powered, bandwidth-y nodes — aggregators, the camera.

> **Band diversity is a resilience feature, not sprawl:** a single 2.4 GHz insult (interference, a dead coordinator) can't take the sub-GHz nodes down with it — **no single RF point of failure** ([design-around-failure](30-electronics-and-controls.md#4-design-around-failure--assume-it-will-fail-keep-it-reachable) applied to spectrum).

**Guardrails so it stays disciplined, not sprawling:**
- **One transport per niche** — don't run two radios doing the same near-field 2.4 GHz mesh job.
- **Each gateway is a budgeted power line** on the [power BOM](../build/bom/off-grid-power.md) (always-on = Wh/day).
- **Each transport needs spares + ≥ 2 Amber people** who know it (continuity over a thin Amber pool — the *residual* form of the old cognitive-load worry).
- **Standardize the integration pattern** — every transport lands in HA through a documented bridge and one diagnostic view, even if the radios differ.

Overall stack: **ESPHome + HA** fits our ethos — open, local-first, cheap, huge community.

## 6. The QR / dashboard experience (education + showcase)

- **Two QR codes:** one **WiFi-join** (standard `WIFI:` payload phones read natively) onto the *guest* segment; one a **URL to the local dashboard** (`greenhouse.local` via mDNS for a friendly name).
- **Range reality:** local WiFi won't cover the whole campus. For range-free access, a **public read-only dashboard** over the uplink doubles as the **community/showcase** feature — anyone can pull up live greenhouse data.
- **`REQ-DATA-4` is a networking requirement in disguise:** classrooms setting up experiments and watching from the room means the data has to *reach the school building* — favors a path that bridges to the school LAN or a cloud dashboard.
- **Camera + kids = privacy.** Any webcam points at **plants, not students**, leans local-first, and gets a line on data governance so a showcase feature doesn't become a privacy problem.
- **Cooling-mode page (teaching surface).** A dashboard page shows the **current vent mode** (stack vs. wind-venturi), *why* it chose it (interior temp + windspeed/direction), and a **countdown to the next mode re-evaluation** (the ~15-min dwell, [REQ-COOL-10](../design/10-requirements.md#b-cooling--ventilation--the-headline-system)) — plus an **"override-tripped"** flag when a temp-spike forces an early switch, so a sudden change doesn't look like a glitch. Great live-physics lesson.

---

## Architecture sketch

```
        ┌─────────────── Tier 3 (sheddable) ───────────────┐
 Phones │  Guest WiFi (read-only, isolated) ── Access Point │
 (QR) ──┼──                                                 │
        │  HA core (SSD, RTC, watchdog) ── Dashboards/History│
        └───────────────────────┬───────────────────────────┘
                                 │  brokers
        ┌──── IoT / control segment (no direct internet) ────┐
        │  PoE/Ethernet backbone ── key actuators            │
        │  Zigbee (Thread-capable HW) ── in-house sensors    │
        │  LoRa / sub-GHz ── far + canopy-buried nodes        │
        └────────────────────────────────────────────────────┘

   ╔══════════════ Tier 1/2 (survives) ══════════════╗
   ║  Safety controller ── overtemp→vent, irrigation,  ║
   ║  alarm  ── low-power cellular/SMS alert channel   ║   ← independent of HA & LAN
   ╚═══════════════════════════════════════════════════╝

   Uplink: LTE (primary) · [school WiFi if IT allows] · outbound tunnel only
```

*Turned into checkable rows as `REQ-NET-*` in [`10-requirements.md`](10-requirements.md#l-network--connectivity).*

---

## Open questions

> **OPEN QUESTION (recommendation: cellular-primary):** External uplink — own LTE vs. pursuing school IT approval vs. both. Leaning **own LTE** for independence; school WiFi only as a blessed secondary.
> ✅ **RESOLVED (2026-06-08):** Sensor transports = **Zigbee** (in-greenhouse 2.4 GHz mesh, Thread-capable HW for a later Matter evolution) **+ LoRa/sub-GHz** (far/canopy nodes) **+ WiFi** (powered aggregators/camera) over the **wired PoE backbone**. Z-Wave dropped — LoRa covers the sub-GHz role. Band diversity buys RF resilience.
> **OPEN QUESTION:** Sensor *topology* — how many scattered battery sensors (→ Zigbee carries more) vs. powered aggregators (→ WiFi carries more). Shifts the load between locked transports; doesn't change the stack.
> **OPEN QUESTION:** The actual far/canopy node list that justifies standing up LoRa on day one vs. later (rain cistern, weather station, outdoor beds).
> **OPEN QUESTION:** HA host platform + whether the safety controller is the same brain or a separate Tier 1 device (ties to the [electronics open question](30-electronics-and-controls.md#open-questions)).
> **OPEN QUESTION:** Does the critical-alert path use cellular data, SMS, or both? Determines the modem/plan on the power BOM.
> **OPEN QUESTION:** Data governance + camera privacy policy for student-facing data.

*Parent: [`30-electronics-and-controls.md`](30-electronics-and-controls.md). Feeds: [`10-requirements.md`](10-requirements.md) (REQ-NET), [`docs/build/bom/off-grid-power.md`](../build/bom/off-grid-power.md) (network gear as loads).*
