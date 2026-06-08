# Roles & Tiers

*Who does what — and, just as importantly, **who is allowed to touch what.** The greenhouse is run by two tiers of volunteers plus contracted professionals. The tier is a **safety and competence boundary**, not just a skill label. Expands [Operating Principle 9](00-operating-principles.md#9-build-the-operating-group-as-deliberately-as-the-building).*

---

## The three tiers

| Tier | Who | Concern | May touch |
|------|-----|---------|-----------|
| 🟢 **Green** | Teachers, students, general volunteers | **Plants & operations** | Growing, watering, harvest, observation, logging. The *only* hardware act: **plugging in keyed power** (Anderson Powerpole / M12) — which is designed so it can't be done wrong. |
| 🟠 **Amber** | Electronics / infra volunteers | **Low-voltage infrastructure** | Sensors, radios, networking, the controller core, diagnostics, the data layer. May also do some planting, but their job is the infra. |
| 🔴 **Red** | **Paid / licensed professionals** (not volunteers) | **Licensed & high-energy work** | The off-grid **PV + battery power system**, mains/AC, structural, and anything inside the **sealed architect/engineer design**. Contracted, not part of the volunteer rota. |

## The boundary is the point

The reason to draw these lines is **safety and legality**, not bureaucracy:

- 🟢 **Green never needs to understand the electronics.** Their whole interface to the infra is: *notice that an expected behavior isn't happening → send the SOS* (see [SOP-04](sops/SOP-04-something-isnt-working.md)). They don't diagnose; the system and the Amber runbook do. This is *why the radio/HW choice never leaks to them* — keyed power ([REQ-CTRL-1](../design/10-requirements.md#k-electronics--controls-architecture)) is the only hardware they meet, and it's poka-yoke'd so it can't be mis-plugged.
- 🟠 **Amber owns the low-voltage world** — and stops at the red line. They troubleshoot via the [runbook](20-troubleshooting-runbook.md), fix what's fixable, and escalate the rest to Red.
- 🔴 **Red is a hard line, not a preference.** The **PV/LiFePO₄ DC bus carries real arc-flash and fire risk**, and mains + the sealed design are **legally licensed work** ([REQ-REG-2](../build/10-regulatory-governance.md)). A willing, capable Amber volunteer still must **not** cross it. This protects people *and* keeps the build code-compliant on school land.

> **Rule of thumb:** if it's a plant or a plug → Green. If it's a sensor, a packet, or a controller → Amber. If it's power, mains, structure, or anything stamped → Red.

## How escalation flows across tiers

```
🟢 Green notices behavior missing ──SOS──▶ 🟠 Amber
                                            │
                            runbook + heartbeat/reachability diagnostic
                                            │
                              fix it ◀──────┴──────▶ escalate ──▶ 🔴 Red (power/mains/sealed)
```

Each tier hands *up* only what it isn't allowed or able to resolve. Green never skips to Red; Amber is the triage layer.

## Naming the people (fill in)

Per Operating Principle 9, roles need *names*, not just tiers:

> **OPEN QUESTION:** Named **Amber lead** (electronics/infra continuity across school years).
> **OPEN QUESTION:** Standing **Red relationships** — a licensed electrician / solar installer and the project architect/engineer on call for escalations.
> **OPEN QUESTION:** How Amber volunteers are recruited and onboarded (the skill pool is smaller than Green).

*Related: [`00-operating-principles.md`](00-operating-principles.md), [`sops/SOP-04-something-isnt-working.md`](sops/SOP-04-something-isnt-working.md), [`20-troubleshooting-runbook.md`](20-troubleshooting-runbook.md).*
