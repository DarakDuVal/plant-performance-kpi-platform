# User journeys

End-to-end journeys for each persona of the **plant performance KPI platform**. A journey frames a persona's goal and
the steps to reach it, and is the source of the [user stories](user-stories.md). Keep personas and domain background in
the project context artifact ([`../docs/context-template.md`](../docs/context-template.md)).

**How to use:** give each journey a stable `UJ-NNN` id. Break it into ordered steps, note the touchpoint and any pain
point per step, and link each step to the stories it produces. Prioritise with `MUST` / `SHOULD` / `COULD` and set a
target iteration so journeys are resolved stepwise.

## Journey index

| ID     | Persona                              | Goal                                                        | Priority | Iteration | Status |
| ------ | ------------------------------------ | ----------------------------------------------------------- | -------- | --------- | ------ |
| UJ-001 | Executive manager / plant manager    | Get an at-a-glance status overview of all active KPIs       | MUST     | 1         | Draft  |
| UJ-002 | Executive manager / plant manager    | Rank plants against each other by their total KPI score     | MUST     | 1         | Draft  |
| UJ-003 | Admin user                           | Correct and maintain KPI data so the platform stays accurate | MUST     | 1         | Draft  |
| UJ-004 | Executive / plant manager / plant controller | Analyse a single KPI's trend, status, benchmark, and context | MUST     | 1         | Draft  |
| UJ-005 | Executive / plant manager            | Compare cost-relevant KPIs across plants in a Pareto view    | MUST     | 1         | Draft  |
| UJ-006 | Executive / plant manager / admin    | Review which KPIs are available (tracked) per plant          | MUST     | 1         | Draft  |
| UJ-007 | New / any user                       | Onboard and get self-service support (tour, release notes, about) | SHOULD   | 1         | Draft  |

---

## UJ-001 — Review active KPI executive summary

- **Persona:** Executive management and plant managers responsible for overall plant performance.
- **Goal:** Understand, at a glance, how each active KPI is tracking and which ones need attention.
- **Trigger:** The manager opens the executive summary view.
- **Success:** The manager can see every active KPI with its status colour and key values (target, YTD actual, latest forecast) and knows how current the data is.

| Step | Action                                                              | Touchpoint        | Pain point / need                                         | Stories        |
| ---- | ------------------------------------------------------------------ | ----------------- | --------------------------------------------------------- | -------------- |
| 1    | Open the executive summary                                         | Executive summary | Needs a single, consolidated view of all active KPIs      | US-001         |
| 2    | Select the entity (ME total or a plant) and the reporting year     | Executive summary | Needs to focus on one scope and compare against prior years | US-002, US-003 |
| 3    | Personalise which KPIs appear in the view (custom selection)       | Executive summary | Needs to see only KPIs relevant to their work or domain   | US-017         |
| 4    | Scan the KPI list and its red / yellow / green status indicators   | Executive summary | Needs to spot under-performing KPIs quickly               | US-001         |
| 5    | Read each KPI's target, YTD actual, latest forecast and update date | Executive summary | Needs to judge magnitude of deviation and data freshness  | US-001         |

---

## UJ-002 — Rank plants by KPI score

- **Persona:** Executive management (and plant managers) steering the plants toward the year's focus topics.
- **Goal:** Compare and rank all plants by a total KPI score so the best and worst performers are visible.
- **Trigger:** The manager opens the plant performance ranking view.
- **Success:** The manager sees plants ordered by total score, with red / yellow / green feedback and a per-KPI score breakdown behind each total.

| Step | Action                                                                        | Touchpoint          | Pain point / need                                              | Stories        |
| ---- | ----------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------- | -------------- |
| 1    | Open the plant ranking view                                                   | Plant ranking       | Needs a single place to compare plants against each other      | US-004         |
| 2    | Review plants ordered by total score with red / yellow / green feedback       | Plant ranking       | Needs to see rank and overall health at a glance               | US-004, US-006 |
| 3    | Inspect each plant's individual KPI scores next to its total                  | Plant ranking       | Needs to understand what drives a plant's rank                 | US-005         |
| 4    | Maintain the year's scoring table (achievable scores, thresholds, exceptions) | Scoring maintenance | Needs to change focus topics year to year without losing history | US-007         |

---

## UJ-003 — Maintain KPI data (admin)

- **Persona:** Admin user responsible for keeping the KPI data accurate.
- **Goal:** Correct and update KPI values so the platform shows accurate data.
- **Trigger:** The admin notices an incorrect value or needs to update data.
- **Success:** The corrected values are saved and reflected across the app; regular users see the updated data read-only.

| Step | Action                                              | Touchpoint      | Pain point / need                                   | Stories |
| ---- | --------------------------------------------------- | --------------- | --------------------------------------------------- | ------- |
| 1    | Log in as an admin user                             | Login           | Needs authenticated access before editing           | US-008  |
| 2    | Locate the KPI value to correct                     | Data maintenance | Needs to find the right value quickly               | US-008  |
| 3    | Modify / correct the value interactively            | Data maintenance | Needs to fix wrong values without a data re-import   | US-008  |
| 4    | Save the change and see it reflected in the app     | Data maintenance | Needs confidence the correction took effect          | US-008  |
| 5    | A programmatic client pushes KPI data non-interactively via the API | Data API | Needs unattended, automated data updates (later automation) | US-009  |

---

## UJ-004 — Analyse a KPI in detail

- **Persona:** Executives and plant managers seeking context, and plant controllers who add that context.
- **Goal:** Understand a single KPI's development over time, its current goal status, who sets the benchmark, where the data comes from, and any expert notes.
- **Trigger:** The user selects a KPI to drill into.
- **Success:** The user sees annual and monthly trends, the goal status, the benchmark plant, the data sources, per-point context, and any notes.

| Step | Action                                                                   | Touchpoint  | Pain point / need                                        | Stories        |
| ---- | ------------------------------------------------------------------------ | ----------- | -------------------------------------------------------- | -------------- |
| 1    | Open a KPI's detail view                                                 | KPI detail  | Needs to drill into one KPI                              | US-010         |
| 2    | Review annual actuals and targets, plus the running year's forecast      | KPI detail  | Needs to see multi-year development and where it is heading | US-010         |
| 3    | Review the intra-year actuals-vs-target trend for the selected year      | KPI detail  | Needs intra-year detail                                  | US-011         |
| 4    | For a KPI without a time series, review the gauge-versus-target display   | KPI detail  | Needs status for KPIs that have no trend                  | US-016         |
| 5    | Read the goal status, benchmark plant, and data sources                  | KPI detail  | Needs to judge status and see who leads and where data is from | US-012, US-013, US-014 |
| 6    | Open the KPI's descriptive metadata for context (unit, owner, and more)  | KPI detail  | Needs to understand what the KPI represents               | US-019         |
| 7    | Hover a data point to see its data source and last refresh date          | KPI detail  | Needs provenance and freshness per point                 | US-014         |
| 8    | Add a note giving executives extra context (privileged users)            | KPI detail  | Needs to explain anomalies or decisions                  | US-015         |

---

## UJ-005 — Compare cost KPIs across plants (Pareto)

- **Persona:** Executives and plant managers focused on cost and value drivers.
- **Goal:** Compare cost-relevant KPIs across plants, ordered by value, to see which plants drive them.
- **Trigger:** The user opens the cost (Pareto) tab.
- **Success:** Each cost-relevant KPI is shown as a Pareto chart of plants ordered by descending value.

| Step | Action                                                            | Touchpoint | Pain point / need                                    | Stories |
| ---- | ----------------------------------------------------------------- | ---------- | ---------------------------------------------------- | ------- |
| 1    | Open the cost (Pareto) tab                                        | Cost view  | Needs cost-relevant KPIs grouped in one place         | US-018  |
| 2    | Review each cost KPI as a Pareto chart of value by plant          | Cost view  | Needs to see which plants contribute most             | US-018  |

---

## UJ-006 — Review KPI availability per plant

- **Persona:** Executives, plant managers, and admins who need to know which KPIs are tracked for which plants.
- **Goal:** Understand, per KPI and plant, whether the KPI is tracked — and why some are not (e.g. no such production).
- **Trigger:** The user opens the availability tab.
- **Success:** The user sees a KPI-by-plant matrix with a four-state colour coding of availability.

| Step | Action                                             | Touchpoint         | Pain point / need                                    | Stories |
| ---- | -------------------------------------------------- | ------------------ | ---------------------------------------------------- | ------- |
| 1    | Open the availability tab                          | Availability view  | Needs a single place to see coverage                  | US-020  |
| 2    | Read the availability state per KPI and plant      | Availability view  | Needs to see which plants are tracked for which KPIs  | US-020  |
| 3    | Edit the per-cell (KPI/plant) availability note (super users) | Availability view  | Needs to explain why a cell is false / limited / invalid | US-024  |

---

## UJ-007 — Onboard and get self-service support

- **Persona:** New and returning users of the app.
- **Goal:** Learn the app and find help and information without external support.
- **Trigger:** A user opens the app for the first time or looks for help / information.
- **Success:** The user can take a guided tour, read the release notes, and find purpose, contacts, support and FAQ on the About page.

| Step | Action                                                              | Touchpoint    | Pain point / need                                  | Stories |
| ---- | ------------------------------------------------------------------ | ------------- | -------------------------------------------------- | ------- |
| 1    | Take the guided first-use tour                                     | Guided tour   | Needs to learn the app quickly                      | US-022  |
| 2    | Read the release notes to see what changed                        | Release notes | Needs to stay informed of app changes               | US-021  |
| 3    | Open the About page for purpose, contacts, support and FAQ        | About page    | Needs to understand the app and find help           | US-023  |
