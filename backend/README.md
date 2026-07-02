# Backend

Backend service for the plant performance KPI platform. This directory will hold
the API, business logic, and database access for the application.

> **Status: skeleton.** No code yet. The language, framework, and API style will
> be chosen as requirements firm up and recorded as an
> [ADR](../docs/decisions/).

## Intended contents

- API endpoints serving the frontend.
- Domain and business logic for plant performance KPIs.
- Data access to the database defined in [`../database/`](../database/).
- Configuration and environment handling (secrets stay out of Git).
- Automated tests, per [`../docs/quality-standards.md`](../docs/quality-standards.md).
