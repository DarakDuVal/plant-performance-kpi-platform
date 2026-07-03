# Non-functional requirements

How well the **plant performance KPI platform** must do its job — the quality attributes that cut across features. Each
non-functional requirement is measurable and testable. When a slice is ready to build, baseline it into an initiative
spec from [`../product/requirements-template.md`](../product/requirements-template.md).

**How to use:** give each requirement a stable `NFR-NNN` id (never reused). State a concrete, measurable threshold and
how it is measured — avoid vague words like "fast" or "robust". Prioritise (`MUST` / `SHOULD` / `COULD`) and set a
target iteration so requirements are resolved stepwise.

## Requirements

| ID      | Category  | Priority | Requirement                                                                                                                                                       | Measurement                                                | Iteration | Spec status |
| ------- | --------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | --------- | ----------- |
| NFR-001 | Usability | MUST     | The user interface shall apply Bosch branding elements and visuals (logo, colour palette, typography, iconography, spacing) in compliance with the Bosch brand guide. | Brand review sign-off against the Bosch brand-guide checklist | 1         | Specified   |
| NFR-002 | Security  | MUST     | The application shall be accessible only from within the Bosch corporate network.                                                                                | Access attempt from outside the Bosch network is denied (network / security test) | 1         | Specified   |
| NFR-003 | Usability | MUST     | The application shall be operable as a desktop web-browser application for the first releases.                                                                   | Functional verification on the supported desktop browsers  | 1         | Specified   |
| NFR-004 | Portability | COULD  | The application shall additionally support mobile app access in later versions.                                                                                  | Access verified on the target mobile devices               | 3         | Specified   |
| NFR-005 | Performance | MUST   | The application shall respond to a user selection within 1 s under normal load (p95) and no more than 3 s under heavy load.                                       | UI response-time measurement under normal and heavy load (e.g. p95) | 1         | Specified   |

**Categories:** Performance · Reliability · Security · Maintainability · Scalability · Usability · Compliance ·
Portability.

**Priority key:** `MUST` — required for the baseline release · `SHOULD` — important but deferrable · `COULD` — nice to
have.

## Constraints

- **Hosting:** The application is hosted on Bosch's Microsoft Azure tenant.
- **Data source:** KPI data is provided to the application via an accessible API (see FR-028).
- **Authentication:** Users sign in via Bosch Microsoft Entra ID single sign-on (SSO), using a registered Enterprise
  application. Group membership originates in oneIDM (formerly OneIdentity), is batch-processed into Azure users and
  groups, and is supplied to the application in request headers (see FR-033).
- **Replacement / feature-parity gate:** An existing PowerBI application is the functional baseline and comparison
  reference. The new application may replace it only once it reaches at least the same minimal functionality (feature
  parity with the PowerBI app).
- **Reference data model / seed source:** An existing star-schema database held as an Excel file
  (`requirements/examples/db.xlsx`) is the current PowerBI backend source. Its structure and content guide the
  platform's data model and may be used to seed the future database for migration.
- **UI toolkit (Bosch Frontend Kit):** The UI is built with the Bosch Frontend Kit (part of the Bosch Digital Design
  System), release 5.1.0 — an HTML / CSS / JS pattern library of the core Bosch UI Kit components. The project
  references `frontend-kit.js` and the required CSS (loaded in small chunks per the Frontend Kit guidance). The dist
  folder is available at `requirements/frontend-kit`. The kit is framework-agnostic (confirmed with React, Angular and
  Vue); it is installed from the BDC Artifactory npm package, CSS may be imported complete or per-component, and
  `frontend-kit.js` achieves interactivity by toggling CSS classes (a framework may implement the same effect instead).
  Component markup is taken from the Bosch preview server. (Detailed integration guidance is design/implementation
  context for the architect and developers, not a separate requirement.)

## Open questions & dependencies

- **NFR-001 brand guide (dependency):** Compliance is assessed against the Bosch brand guide. Brand-guide assets
  (logos, colours, fonts, icons, illustrations, supergraphic, and more) are available at `requirements/brandguide`;
  record the applicable brand-guide version in the project context artifact once it exists. Branding is realised
  primarily through the Bosch Frontend Kit (see the UI toolkit constraint above).

**Spec status key:** `Specified` (not built) · `Implemented` (built) · `Verified` (built and covered by a passing,
traceable test) · `Drifted` (code and spec disagree — reconcile before the iteration closes).
