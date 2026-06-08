# Operating Principles

*How the greenhouse actually gets run, day to day and season to season. The [design principles](../design/00-design-principles.md) shape the building; these shape the human system around it. A greenhouse fails far more often from neglect than from bad construction — so we design the operating model with as much care as the structure.*

---

## The core reality

The people running this greenhouse are **teachers and students during the school year, with parent/volunteer backup** — and crucially, **the summer break overlaps the hottest, highest-stress growing months when the school is nearly empty.**

Every operating principle below is an answer to one question:

> **How does a living, growing system survive when the people responsible are busy, untrained, rotating, and sometimes absent for ten weeks?**

---

## 1. Assume the gap, don't assume a hero

Plans that depend on a dedicated, expert caretaker showing up daily will fail the first time that person is sick, graduates, or moves. Design the operation for the *typical* week, not the heroic one.

- **The baseline level of care is "a busy teacher and an occasional volunteer."** Anything that requires more than that is a bonus, not a dependency.
- **No single point of human failure.** No task should be knowable by only one person. If the one parent who understands the irrigation timer leaves, the system still runs.
- **Cross-train and rotate** so knowledge lives in the group, not one head.

## 2. Write it down — SOPs over tribal knowledge

If a task isn't written down, it doesn't reliably happen.

- **Every recurring task gets a one-page SOP**: what, when, how, what "good" looks like, who to call when it's wrong. Photographs beat paragraphs for an 8-year-old or a new volunteer.
- **SOPs live in `docs/operate/` and on the wall** of the greenhouse — laminated, at the point of use.
- **A new volunteer should be productive in 15 minutes** with the SOP and nothing else.
- Keep a **simple logbook** (paper or shared sheet): what was done, what looked off. Continuity across rotating hands depends on it.

## 3. Define the seasons of operation explicitly

The greenhouse runs in distinct modes, and the dangerous transitions are the boundaries between them.

| Season | Who's around | Operating mode |
|--------|--------------|----------------|
| **School year** | Teachers + students daily | Full program: lessons, planting, harvest, data. |
| **Weekends / breaks** | Volunteers, intermittent | Maintenance mode: automation runs, volunteers check & water. |
| **Summer (the hard one)** | Minimal/none | **Survival mode:** automation + alerting carry the load; plant only what tolerates neglect, or deliberately rest the space. |

- **Plan the summer *before* you plant in spring.** Decide by April: are we growing through summer with a committed volunteer rota, or resting the beds? Don't drift into summer with crops no one can tend.
- **Name an owner for each season.** Especially summer — it needs a coordinator and a written rota, locked in before school lets out.

## 4. Automation does the life-or-death work; humans do the judgment

Split tasks by consequence-of-failure.

The greenhouse tries to take care of itself. Humans may have to check that all the automations worked.

- **Automated (failure = dead plants or danger):** temperature-driven ventilation, irrigation, freeze/heat alerts. These never wait on a human. *(See [REQ-COOL](../design/10-requirements.md#b-cooling--ventilation--the-headline-system), [REQ-WATER-1](../design/10-requirements.md#e-irrigation--water).)*
- **Human (failure = a worse lesson or a smaller harvest):** observing, pruning, transplanting, harvesting, teaching, experimenting. These are the rewarding parts — leave them for people.
- **Trust but verify the automation.** A weekly checklist confirms the timers fired, the rainwater tank has water, the battery is charging, and the vents move. Automation that silently fails is worse than no automation.
- **Off-grid means watching the weather as an operator, not just a gardener.** A forecasted hot-and-cloudy stretch is the danger window: pre-charge what you can, shed Tier 3 loads early, and lean on the passive systems. The greenhouse is designed to survive it untended — but a heads-up volunteer makes it survive *comfortably*.

## 5. Alert early, escalate clearly

- **The system warns before it's a crisis** — high-temp, low-moisture, power-loss, freeze alerts to phones. *(See [REQ-ELEC-4](../design/10-requirements.md#f-electrical--controls).)*
- **A written escalation chain:** alert → on-call volunteer → backup → staff lead. Posted, with current phone numbers, and reviewed each semester.
- **Tune alerts to avoid fatigue.** Too many false alarms and people stop looking. Set thresholds with margin but not noise.

## 6. Safety is an operating practice, not a built-in feature

The building is designed safe (Principle 1 of the design doc), but safety is also something people *do*.

- **Adult supervision ratio** for student sessions, defined and enforced.
- **Daily heat check in summer-adjacent months** before anyone enters — a closed greenhouse can be dangerously hot even on a mild day.
- **Tools, amendments, and any chemicals locked** and inventoried; only child-safe products on the open shelves.
- **Handwashing in and out.** It's a space full of soil, water, and shared tools.
- **A posted emergency procedure** (heat, injury, who to call) and a stocked first-aid kit.

## 7. Make operation part of the curriculum, not a chore bolted on

The strongest sustainability strategy is to **fold running the greenhouse into the learning itself** — then upkeep is the lesson, not extra work.

- **Students own age-appropriate tasks** (watering checks, logging data, harvest) as part of class.
- **The logbook and sensor data are teaching material** — graphing temperature, tracking growth, noticing what the alerts caught.
- **Rotate "greenhouse jobs"** like classroom jobs so every student participates and learns the why.

## 8. Run it cheap to keep it running

Operating budget is the quiet killer of school greenhouses.

- **Track recurring costs** (water, power, consumables, replacement parts) and keep them low by design — passive cooling, rainwater, durable parts.
- **A maintenance reserve and a named budget line**, not just goodwill. *(Flag for the district/PTA.)*
- **A spares shelf** of the parts most likely to fail (timer, fan, tubing, fittings) so a breakdown is a weekend fix, not a month-long shutdown.

## 9. Build the operating group as deliberately as the building

- **Name roles, not just volunteers:** a staff lead (continuity across years), a volunteer coordinator, season owners, a maintenance contact.
- **Plan for turnover.** Students graduate, families move, teachers change. Onboarding and SOPs are what survive the churn.
- **Partner outward:** local master gardeners, a nursery, the district grounds crew, nearby high-school ag programs — borrow expertise the school doesn't have in-house.

---

## How these connect to the design

Operating principles and design requirements are two halves of one promise. A few tight couplings to keep honest:

- *Survive summer break* (Op 3) is only possible because of *automate the life-or-death loop* and *fail open* ([REQ-COOL-4/5](../design/10-requirements.md#b-cooling--ventilation--the-headline-system)).
- *SOPs over tribal knowledge* (Op 2) depends on *simple, repairable, standard parts* ([Design Principle 5](../design/00-design-principles.md)).
- *Run it cheap* (Op 8) is the operating echo of *cheaper to keep* ([Design Principle 6](../design/00-design-principles.md)).

If a design choice makes operation harder, revisit the design. The building exists to be run, not admired.

---

## Open questions to resolve next

> **OPEN QUESTION:** Who is the named staff lead — the person responsible across school years? Without this role, nothing else holds.
> **OPEN QUESTION:** Summer plan — committed volunteer rota, or rest the beds? Decide before the first spring planting.
> **OPEN QUESTION:** Is there budget commitment for recurring operating costs and a maintenance reserve, or only construction funding?
> **OPEN QUESTION:** What community partners (master gardeners, nurseries, ag programs) can we line up before opening?

*Next operating documents to write: a growing calendar (`10-growing-calendar.md`), and the first SOPs — daily check, weekly check, summer survival procedure.*
