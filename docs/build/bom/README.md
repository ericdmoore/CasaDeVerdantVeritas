# Bills of Materials (BOM)

*Living procurement artifacts — one BOM per subsystem. Unlike the design docs (prose + principles), these are tables that evolve from "proposed" through "installed" and double as a procurement tracker.*

## The BOMs

| BOM | Subsystem | Status |
|-----|-----------|--------|
| [off-grid-power.md](off-grid-power.md) | Solar array, battery, charge control, distribution | 🟡 Scaffolding (awaiting sizing) |
| [controls.md](controls.md) | Compute core, sensors, actuators, comms, connectors | 🟡 Scaffolding (awaiting device list) |
| [irrigation.md](irrigation.md) | Harvest, storage, gravity drip, fertigation, freeze | 🟡 Scaffolding (awaiting zone layout) |
| [structure.md](structure.md) | Frame, glazing, vents, doors, beds, **tool/implement storage** | 🟡 Scaffolding (awaiting sealed design) |
| [BOM_considered.md](BOM_considered.md) | **Decision log** — products/approaches evaluated for controls, valve drivers, hydro, charge control; Selected / Pending / Disregarded + rationale | 🟡 Living |

## Standard format

Every BOM uses the same columns:

| Item | Spec / Model (or "or equal") | Qty | REQ trace | Source | Unit $ | Ext $ | Lead time | Status | Notes |
|------|------------------------------|-----|-----------|--------|--------|-------|-----------|--------|-------|

### Conventions

- **Spec, then SKU.** On school land, district **procurement rules (TEC Ch. 44, [REQ-REG-5](../10-regulatory-governance.md))** may require competitive bidding — so write biddable specs with **"or equal"** rather than locking to a single vendor's part number.
- **REQ trace** — every line ties back to a requirement in [`10-requirements.md`](../../design/10-requirements.md) so we can defend why it's on the list.
- **Status field** — `proposed → approved → ordered → installed`. The BOM *is* the procurement tracker.
- **Phaseable** ([Design Principle 6](../../design/00-design-principles.md)) — mark a **Phase** (core / later) so the build can open with the essentials and add extras as grants land.
- **Sizing before parts.** A BOM whose quantities depend on an engineering calc (power, irrigation) opens with a **sizing basis** section; numbers marked *TBD* until the calc is done.

*Costs are planning estimates until quotes come in. Keep a running subtotal per BOM and a project rollup once subsystems firm up.*
