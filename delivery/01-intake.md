# 01 — Intake & triage

**Delivery-loop step 1** · Agent: `customer-support` · Team version: **3.0.0** ·
Spec: [`../requirements/`](../requirements/) · Roadmap: [`../requirements/roadmap.md`](../requirements/roadmap.md)

## Request classification

- **Type:** New product build (greenfield web application), delivered iteratively.
- **Product:** Plant performance KPI platform — a Bosch-internal web app that replaces an existing PowerBI report with a
  richer, interactive KPI cockpit for Mobility Electronics (ME) and its production plants.
- **Scope source:** Fully captured spec — 7 journeys, 24 stories, 62 functional and 5 non-functional requirements.
- **Replacement gate:** May retire the PowerBI baseline only at feature parity (Iteration 1 `MUST` set).

## Completeness check

Requirements are structured and testable (Given-When-Then throughout). Remaining open items are tracked in the spec's
"Open questions & dependencies" sections and do not block Iteration 1 kickoff:

- KPI note attachment for quarterly KPIs (FR-041) — to confirm; does not block R0–R2.
- Bosch brand-guide version to record in context (assets present at `requirements/brandguide`).

## Known assets provided

| Asset | Location | Use |
| ----- | -------- | --- |
| Reference data model (star schema) | `requirements/examples/db.xlsx` | Seeds the data model and migration seed data |
| Bosch Frontend Kit 5.1.0 dist | `requirements/frontend-kit` | UI component library (framework-agnostic) |
| Bosch brand assets | `requirements/brandguide` | Branding compliance (NFR-001) |

## Handoff

→ Step 2 (`business-analyst`) for value framing, then step 3 (`requirements-engineer`) which baselines each release
slice from the already-captured spec. Context artifact initialised at [`00-context.md`](00-context.md).
