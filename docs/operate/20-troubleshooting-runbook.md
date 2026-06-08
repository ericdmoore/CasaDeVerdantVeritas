# Troubleshooting Runbook (Amber)

*For 🟠 **Amber** (infra) volunteers, picking up a 🟢 Green SOS ([SOP-04](sops/SOP-04-something-isnt-working.md)). The goal: localize a fault fast using telemetry the system already collects, fix what's in the low-voltage domain, and hand the rest to 🔴 Red. **Stop at the red line** — power system, mains, and anything in the sealed design are licensed work ([roles & tiers](10-roles-and-tiers.md)).*

> Before touching anything physical: it's a greenhouse — vent it if it's warm, and remember the [tier boundary](10-roles-and-tiers.md#the-boundary-is-the-point).

---

## The mental model: the path

Every behavior is a **chain**, and the fault is *one link*:

```
physical condition → sensor → transport (radio/wire) → controller core → logic → actuator → physical effect
        ↑ (e.g. heat)                                                              ↓ (e.g. vent opens)
```

A missing behavior ("fans didn't run") could be a dead sensor, a quiet radio node, a hung controller, a tripped automation, or a stuck actuator. **Don't guess — let the telemetry point first.**

## Step 1 — Triage from telemetry (before walking out)

The system tracks **per-node last-seen / heartbeat age** and offers a **reachability scan** ([REQ-NET-7](../design/10-requirements.md#l-network--connectivity)). Read it first:

| Pattern | Likely zone |
|---------|-------------|
| **One node** quiet, neighbors fine | That node: its power, connector, or radio/sensor. |
| **A whole segment / area** quiet | A shared router, a radio coordinator, or that area's power. |
| **Everything** quiet at once | The **core** (controller/host) or its power — or the data layer only (check: are plants/actuators actually fine? Safety loop is independent). |
| Node **present but values stuck/implausible** | The sensor itself (drift, condensation, corrosion), not the link. |
| Behavior missing but **all nodes report fine** | The **automation/logic** or the **actuator**, not sensing. |

> Reminder: if the **data layer** is down but the **safety loop** is doing its job (venting, irrigating), plants are fine — this is by design ([REQ-NET-1](../design/10-requirements.md#l-network--connectivity)). Triage urgency accordingly.

## Step 2 — Localize on site

Walk to the zone the telemetry implicated and work the chain link by link:

- **Power** — is the node powered? Check the keyed connector is seated (Green may have already tried). Check the node's power source / tier — was it **shed on low battery** ([REQ-PWR-4](../design/10-requirements.md#f2-off-grid-energy--solar--battery-no-utility))? A Tier-3 node going dark in a cloudy stretch is *expected behavior*, not a fault.
- **Connector / wiring** — corrosion, moisture ingress, a chewed or fretted cable (the greenhouse failure modes from [electronics Principle 4](../design/30-electronics-and-controls.md#4-design-around-failure--assume-it-will-fail-keep-it-reachable)).
- **Radio** — for a lone quiet node: is its nearest mains router up? Interference? Re-pair if needed. For a whole segment: the coordinator (swap to the spare stick; restore the saved network config).
- **Controller / host** — hung? Watchdog should have cycled it; if not, restart. SD-card death is *the* classic host failure — confirm it booted from SSD ([REQ-NET-6](../design/10-requirements.md#l-network--connectivity)).
- **Logic** — did the automation actually fire? Check the trigger/conditions and the controller log.
- **Actuator** — getting the command but not moving? Stuck vent, seized fan, clogged valve, blown fuse on that circuit.

## Common failure points (greenhouse-specific)

- **Condensation / corrosion** at a connector or board — the #1 environmental killer. Reseat, clean, check the enclosure breather/desiccant.
- **Low-battery load shed** mistaken for a fault — always check SOC + tier first.
- **2.4 GHz interference** dropping radio nodes — esp. if WiFi/camera load changed, or the coordinator stick got moved near USB-3 noise.
- **Host storage / hang** — SSD healthy? watchdog working?
- **Stuck actuator** — mechanical, not electronic; often the real answer when sensing looks fine.

## Fix, or escalate to 🔴 Red

**Amber may** reseat/clean low-voltage connectors, swap a sensor/radio node or coordinator, restart the host, re-pair devices, replace a low-voltage fuse, free a stuck low-voltage actuator.

**Stop and escalate to 🔴 Red for:** anything on the **PV array, charge controller, or battery bank**; any **mains/AC**; structural; or anything inside the **sealed design**. *The fact that you could doesn't mean you may* — arc-flash/fire risk and code ([REQ-REG-2](../build/10-regulatory-governance.md)).

## After the fix

- [ ] **Verify** the original behavior returns (watch the actuator actually act).
- [ ] **Log it** in the maintenance log: symptom → root cause → fix.
- [ ] **Feed design-around-failure:** if this fault is likely to recur (a connector that keeps corroding, a node that keeps dropping), note it — the fix might be a **design change** or a **spares-shelf** item, not just a repair. Recurring faults are signal.

---

## Open questions
> **OPEN QUESTION:** Where does the per-node heartbeat / reachability diagnostic surface for Amber — a dedicated dashboard view? (Design hook: [REQ-NET-7](../design/10-requirements.md#l-network--connectivity).)
> **OPEN QUESTION:** Sensor/actuation **path map** for the final device list — a per-zone diagram Amber can follow. (Produce once hardware is specced.)

*Related: [`10-roles-and-tiers.md`](10-roles-and-tiers.md), [`sops/SOP-04-something-isnt-working.md`](sops/SOP-04-something-isnt-working.md), [`../design/30-electronics-and-controls.md`](../design/30-electronics-and-controls.md), [`../design/40-network-and-connectivity.md`](../design/40-network-and-connectivity.md).*
