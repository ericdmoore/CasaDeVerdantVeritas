# Operate — how it runs

*The human system around the building. A greenhouse fails from neglect far more often than from bad construction, so this folder is about seasons, rotas, tiers, and procedures a new volunteer can follow in fifteen minutes. The [design](../design/README.md) shapes the building; these docs shape the people around it.*

---

## The docs

| Doc | What it is | Read this if… |
|-----|------------|---------------|
| [00-operating-principles.md](00-operating-principles.md) | Nine principles: assume the gap (don't assume a hero), SOPs over tribal knowledge, explicit seasons of operation, automation does the life-or-death work and humans do the judgment, alert early / escalate clearly, safety as practice, operation as curriculum, run it cheap, build the operating group deliberately. | …you're setting up or leading the volunteer group. |
| [10-roles-and-tiers.md](10-roles-and-tiers.md) | **🟢 Green · 🟠 Amber · 🔴 Red** — who does what, and who is *allowed* to touch what. The tier is a safety and competence boundary, not a skill label. Includes how escalation flows and a "name the people" fill-in. | …you're new. Find your color first. |
| [20-troubleshooting-runbook.md](20-troubleshooting-runbook.md) | For 🟠 Amber, picking up a Green SOS: triage from telemetry before walking out, localize on site, the greenhouse-specific failure points, fix what's in the low-voltage domain, hand the rest to Red. | …something's broken and SOP-04 escalated it to you. |
| [30-growing-program.md](30-growing-program.md) | What we grow, who grows it, where it goes (take-home, not cafeteria), crop priorities, the native-plant nursery, phasing as budget grows, built-in educational features. Grow-through-summer is the season model. | …you're the garden teacher or running the program. |
| [40-growing-calendar.md](40-growing-calendar.md) | The year at a glance for Dallas zone 8a/8b — anchor crops by priority and a rough planting cadence. A starting draft for the science/garden teacher to refine, not gospel. | …you're deciding what to plant this month. |
| [sops/](sops/README.md) | **Laminated, point-of-use procedures.** One page each, photographable, owned by a tier, with who / when / time at the top. | …you have a task to do right now. |
| ↳ [SOP-01 Daily Check](sops/SOP-01-daily-check.md) | Teacher with students · every school day · ~5 min. | |
| ↳ [SOP-02 Weekly Check](sops/SOP-02-weekly-check.md) | Volunteer · weekly, year-round · ~30 min. | |
| ↳ [SOP-03 Summer Survival](sops/SOP-03-summer-survival.md) | Summer owner + rota · set up *before* school lets out, then weekly · includes the emergency campus tether. | |
| ↳ [SOP-04 Something Isn't Working](sops/SOP-04-something-isnt-working.md) | 🟢 Green · whenever expected behavior isn't happening · ~2 min triage + escalation. | |
| ↳ [SOP-05 Compost Care](sops/SOP-05-compost-care.md) | 🟢 Green (volunteer for the hot pile) · weekly · ~15 min. | |
| ↳ [SOP-06 Water-System Check](sops/SOP-06-water-system-check.md) | 🟢 Green / volunteer · weekly · ~15 min · escalate to Amber. | |

## How a problem moves through the system

```
🟢 Green notices ──► SOP-04 (2-min triage) ──► 🟠 Amber ──► 20-troubleshooting-runbook
                                                     │
                                       low-voltage fix ◄┘└► 🔴 Red (licensed / mains / structural)
```

- **Automation handles the life-or-death loop** (overtemp → vent, irrigation, alarm) on the Tier-1 safety controller, with Home Assistant powered off if need be. People handle judgment — see [Network principle 0](../design/40-network-and-connectivity.md).
- **Seasons are explicit.** School year vs. summer break are different operating modes with different owners; SOP-03 is the handoff.
- **Every SOP names its tier** so no one is asked to do something outside their boundary.

## Status

🟡 **Drafted, unstaffed.** Principles, tiers, runbook and six SOPs exist; the growing calendar awaits the garden teacher; the "name the people" section in Roles & Tiers is still blank.

*Up: [`../README.md`](../README.md) (docs map) · [`../../README.md`](../../README.md) (project). Previous: [`../build/`](../build/README.md).*
