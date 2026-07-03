# ADR-001 — Technology stack for the plant performance KPI platform

**Date:** 2026-07-03  
**Status:** Accepted

## Context

The plant performance KPI platform is a Bosch-internal, data-heavy web app hosted on Bosch's Azure tenant, accessible
only inside the Bosch network. It ingests KPI data via a REST API (FR-028), derives user roles from Entra ID / oneIDM
group headers (FR-033), must apply Bosch branding through the Bosch Frontend Kit 5.1.0 (NFR-001), and must respond
within 1 s p95 under normal load (NFR-005). Its data model derives from an existing star-schema PowerBI backend
(`requirements/examples/db.xlsx`). A stack is needed before task decomposition and implementation begin.

## Decision

We have decided to build with:

- **Backend:** Python 3.12 + FastAPI, SQLAlchemy 2.0 (ORM), Alembic (migrations), Pydantic (validation), Uvicorn.
- **Database:** PostgreSQL (Azure Database for PostgreSQL Flexible Server), modelled as a star schema derived from
  `db.xlsx`.
- **Frontend:** TypeScript + Vite, using the Bosch Frontend Kit 5.1.0 (framework-agnostic HTML/CSS/JS) for branded
  components, and Apache ECharts for time-series, gauge, and Pareto charts.
- **AuthN/Z:** Entra ID SSO terminated at the Azure edge (Enterprise app); the app trusts oneIDM group membership passed
  in request headers to derive roles (FR-033). No interactive OIDC inside the app.
- **Hosting & delivery:** Azure Container Apps; CI/CD via GitHub Actions; local parity via `docker-compose`.
- **Quality tooling:** `ruff` + `pytest`/`pytest-cov` (backend), `eslint`/`prettier` + `vitest` (frontend), per
  [`../quality-standards.md`](../quality-standards.md).

## Consequences

**Positive:**

- FastAPI + Pydantic gives typed, self-documenting APIs well suited to KPI ingest and read models, with strong test
  support to hit the 80 % coverage bar.
- PostgreSQL handles the star-schema, year-versioned scoring, and Pareto aggregation cleanly and is first-class on Azure.
- A framework-agnostic Frontend Kit plus Vite keeps the UI light and lets us adopt the Bosch components directly.
- ECharts covers all required chart types (time series, gauge, Pareto) with one dependency.

**Negative / risks:**

- Two languages (Python, TypeScript) in one repo increases tooling surface; mitigated by clear `backend/`–`frontend/`
  separation and shared CI.
- Header-based role trust requires the Azure edge to strip/enforce headers so they cannot be spoofed from clients —
  flagged for `security-engineer` review in R0.

**Neutral:**

- Charting library and ORM choices are reversible behind the service/data-access boundaries.

## Alternatives considered

| Alternative | Reason not chosen |
| ----------- | ----------------- |
| Node.js/TypeScript backend (single language) | Python chosen for stronger data/analytics ergonomics and team fit (`software-developer-python`). |
| React/Angular SPA framework | Bosch Frontend Kit is framework-agnostic; a heavy framework adds weight without clear benefit for this view-centric app. |
| Azure SQL (MSSQL) | PostgreSQL preferred for open tooling and cost; either meets the star-schema need — reversible behind data access. |
| App-side interactive OIDC | Roles already arrive as trusted oneIDM headers (FR-033); edge-terminated SSO is simpler and matches the constraint. |

## References

- [`../../requirements/non-functional-requirements.md`](../../requirements/non-functional-requirements.md) — Constraints, NFR-001/002/005
- [`../../requirements/functional-requirements.md`](../../requirements/functional-requirements.md) — FR-028, FR-033
- [`../../requirements/roadmap.md`](../../requirements/roadmap.md)
