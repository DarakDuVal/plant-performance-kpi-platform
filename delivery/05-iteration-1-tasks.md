# 05 — Iteration 1 task breakdown

**Delivery-loop step 5** · Agent: `senior-software-architect` · From
[`../docs/task-breakdown-template.md`](../docs/task-breakdown-template.md). Instantiated per the roadmap
([`../requirements/roadmap.md`](../requirements/roadmap.md)); one task block per release (R0–R7).

## Iteration

- **Iteration:** 1
- **Spec revision covered:** Iteration-1 `MUST` set + Iteration-1 `SHOULD` (R7)
- **Goal:** Reach feature parity with the PowerBI baseline — a Bosch-branded, deployed KPI cockpit covering the
  executive summary, KPI detail, availability, ranking, data maintenance, cost Pareto, and onboarding.

## R0 — Foundation

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-001 | ADR-001 | Scaffold `backend/` (FastAPI, ruff, pytest) and `frontend/` (Vite, TS, eslint, vitest); `docker-compose` for local parity | `docker compose up` serves backend health + frontend shell | — | tests+lint pass, reviewed |
| T-002 | NFR-001, NFR-003 | Frontend shell integrates Bosch Frontend Kit 5.1.0 + brand assets; desktop layout | Branded shell renders in supported desktop browser | T-001 | brand review, reviewed |
| T-003 | — | PostgreSQL schema (star model from `db.xlsx`) + Alembic baseline migration | `alembic upgrade head` creates schema on a clean DB | T-001 | migration+tests pass, reviewed |
| T-004 | — | Seed data loader from `db.xlsx` for local/dev | Seed populates entities, KPIs, values | T-003 | seed verified, reviewed |
| T-005 | FR-028 | KPI-data ingest API endpoint (authorized push) | Given valid pushed KPI data, it is stored | T-003 | BDD test cites FR-028 |
| T-006 | FR-029, FR-030, FR-033 | Role derivation from oneIDM/Entra group headers; read-only default, admin gate; edge header hardening | Given admin group header → admin caps; none → read-only; modify without auth rejected | T-001 | security review, tests cite FR-029/030/033 |
| T-007 | NFR-002 | Bosch-network-only access enforced at edge; deploy to Azure Container Apps via GitHub Actions | External access denied; pipeline deploys | T-001 | infra review, reviewed |
| T-008 | NFR-005 | Response-time budget instrumented (p95 ≤ 1 s normal, ≤ 3 s heavy) | Perf check reports p95 within budget on read endpoints | T-005 | perf test cites NFR-005 |

## R1 — Executive summary (UJ-001)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-101 | FR-001, FR-002 | Active-KPI list read model: domain, name, target, YTD actual, last-update | Inactive KPI hidden; active shows all fields | T-005 | tests cite FR-001/002 |
| T-102 | FR-005–010 | Status engine (R/Y/G) with directionality, tolerance, rating basis | Green/yellow/red per FR-006/007/008 cases | T-101 | tests cite FR-005–010 |
| T-103 | FR-003, FR-004 | Status indicator + latest CF value with cycle label in the summary | Row shows one R/Y/G and labelled CF value | T-102 | tests cite FR-003/004 |
| T-104 | FR-011, FR-012, FR-013 | Year selector (current + 2 prior, only when data exists) and year scoping | 2026/2025/2024 selectable; empty years disabled | T-101 | tests cite FR-011–013 |
| T-105 | FR-014–017 | Entity selector (ME or plant), configurable list, scoping, historic validity | Plant scoping + historic year still shows removed plant | T-101 | tests cite FR-014–017 |

## R2 — KPI detail & context (UJ-004)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-201 | FR-034, FR-035 | Annual actuals/targets time series + running-year forecast (ECharts) | Chart shows series; CF on running year | T-103 | tests cite FR-034/035 |
| T-202 | FR-036, FR-045 | Intra-year trend at monthly/quarterly frequency | Monthly vs quarterly KPI render correctly | T-201 | tests cite FR-036/045 |
| T-203 | FR-037 | Detail goal status reusing the R1 status engine | Same R/Y/G as summary | T-102 | tests cite FR-037 |
| T-204 | FR-038 | Benchmark plant (best directionality-normalised actual/target) | Correct benchmark for selected year | T-105 | tests cite FR-038 |
| T-205 | FR-039, FR-040 | Data sources + hover provenance (source, refresh date) | Sources labelled; hover shows provenance | T-201 | tests cite FR-039/040 |
| T-206 | FR-046 | Gauge display for time-series-less KPIs | Gauge vs target for CUV/VA-type KPI | T-201 | tests cite FR-046 |
| T-207 | FR-041–044 | KPI-month notes: add/edit/delete/release, author vs read-only visibility | Released note visible to read-only; unreleased hidden | T-006 | tests cite FR-041–044 |
| T-208 | FR-051–053 | KPI metadata storage + display, in-context presentation | Metadata fields shown in view and in context | T-101 | tests cite FR-051–053 |

## R3 — Availability matrix (UJ-006)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-301 | FR-054, FR-055 | KPI-by-plant availability matrix with four states | Each cell shows one of true/false/limited/invalid | T-105 | tests cite FR-054/055 |
| T-302 | FR-061, FR-062 | Per-cell availability note, super-user edit only | Super user edits; others cannot | T-006, T-301 | tests cite FR-061/062 |

## R4 — Ranking & scoring (UJ-002)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-401 | FR-018–023, FR-056 | Per-KPI scoring (full/half/zero, availability exceptions) and totals | Scores match FR-019/020/021/022/056 cases | T-102, T-301 | tests cite FR-018–023, FR-056 |
| T-402 | FR-024, FR-025 | Rank plants by total; show per-KPI breakdown | Descending order; breakdown shown | T-401 | tests cite FR-024/025 |
| T-403 | FR-026 | Total-score R/Y/G by % of max achievable (configurable thresholds) | 25 %→red, 50 %→yellow, 80 %→green | T-401 | tests cite FR-026 |
| T-404 | FR-027 | Year-versioned scoring table | Given year uses that year's table | T-401 | tests cite FR-027 |

## R5 — Data maintenance (UJ-003)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-501 | FR-031 | Admin interactive edit/correct KPI values | Admin edit persists and reflects; regular cannot | T-006, T-101 | tests cite FR-031 |

## R6 — Cost Pareto (UJ-005)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-601 | FR-049 | Flag cost-relevant KPIs; include in cost view | Flagged KPI appears in cost view | T-101 | tests cite FR-049 |
| T-602 | FR-050 | Pareto chart: plants by descending value for selected year | Plants ordered descending; value on y-axis | T-601 | tests cite FR-050 |

## R7 — Onboarding & support (UJ-007)

| Task ID | Requirement IDs | Description | Acceptance check | Dependencies | Definition of done |
| ------- | --------------- | ----------- | ---------------- | ------------ | ------------------ |
| T-701 | FR-057 | Release notes view | Opening release notes shows changes | T-002 | tests cite FR-057 |
| T-702 | FR-060 | About page (purpose, contacts, support, FAQ) | About shows all four | T-002 | tests cite FR-060 |

## Out of scope for this iteration (Iteration 2–3)

- FR-032 non-interactive automation push; FR-047/048 custom KPI views; FR-058/059 guided tour; NFR-004 mobile.
