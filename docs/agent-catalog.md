# Agent catalog

This catalog is the starting operating model for an AI-native software and IT company. The agents are grouped by department so responsibilities stay discoverable and future additions can follow the same structure.

## Department overview

### Engineering
- **senior-software-developer**: reviews code, asserts quality, flags spec drift, and drives lean, minimal code following Clean Code / Clean Coder principles.
- **senior-software-architect**: shapes architecture, applies Gang of Four design patterns judiciously, and decomposes design into traceable implementation tasks.
- **senior-infrastructure-architect**: designs environments, deployment options, infrastructure-as-code (Terraform and similar), and monitoring across the software lifecycle.
- **software-developer-python**: builds Python backends with Django, Flask, and FastAPI.
- **software-developer-javascript**: builds frontends with React and Angular, defaulting to TypeScript.
- **software-developer-java**: builds Java backends and services.
- **software-developer-php**: builds PHP backends and web applications.
- **software-developer-scripting**: automates tasks with PowerShell, bash, perl, and similar languages.
- **software-developer-ai**: embeds AI capabilities and integrates LLMs and agentic workflows.
- **software-developer-mobile**: builds native iOS and Android mobile apps.
- **devops-release-engineer**: owns CI/CD pipelines and release management for safe, repeatable delivery.

### Delivery management
- **project-delivery-manager**: owns scope, schedule, dependencies, risk, and stakeholder reporting across the delivery loop.
- **agile-delivery-lead**: facilitates the delivery cadence, removes blockers, and protects team flow (Scrum Master / agile coach).
- **engineering-manager**: leads engineering people, capacity, and cross-team coordination (distinct from technical code review).

### Product
- **requirements-engineer**: turns stakeholder needs into structured, testable requirements and owns the living spec across iterations (drift reconciliation).
- **business-analyst**: connects market context, process flows, and solution value, and maintains the project context / steering artifact.
- **product-manager**: owns prioritization, roadmap, and the what/why/when trade-offs.
- **technical-writer**: produces user docs, API references, and runbooks.

### Data
- **data-engineer**: builds data pipelines, warehousing, and ETL/ELT.
- **data-analyst**: turns data into reporting, metrics, and insight.
- **database-administrator**: designs schemas, tunes performance, and owns backup and recovery.

### Security
- **security-engineer**: threat modeling, secure-code review, vulnerability management, and pipeline hardening (DevSecOps).
- **compliance-and-data-protection-expert**: regulatory obligations, audits, and data governance (GDPR, ISO 27001, SOC 2).

### Testing
- **unit-test-expert**: works closest to developers, designing fast, reliable unit tests and improving code testability.
- **load-and-performance-test-expert**: works closest to the software architect, validating performance, scalability, and capacity under load.
- **integration-and-systems-test-expert**: works closest to the infrastructure architect, validating interfaces, end-to-end behavior, and environments.
- **user-acceptance-test-expert**: works with the requirements engineer, business analyst, and marketing to confirm software meets business needs.

### Studio operations
- **it-infrastructure-expert**: owns platforms, environments, reliability, automation, and internal IT support (helpdesk/sysadmin).
- **customer-support**: handles incoming issues, feedback loops, and knowledge base quality, and initialises the engagement's project context at intake.
- **purchasing-expert**: manages suppliers, procurement workflows, and contract readiness.
- **finance-and-controlling-expert**: plans budgets, tracks performance, and maintains governance.
- **people-and-talent-expert**: handles staffing, recruiting, onboarding, and talent and capacity planning.
- **legal-and-contracts-expert**: owns customer agreements, intellectual property, and licensing.
- **customer-success-manager**: owns post-sale relationships, retention, and account management.

### Marketing
- **sales-engineer**: supports pre-sales discovery, demos, and technical solutioning.
- **marketing-and-communications-expert**: owns positioning, campaigns, and message consistency.
- **social-media-expert**: adapts company messaging to community and platform dynamics.

### Design
- **ux-and-design-expert**: shapes user journeys, interaction quality, and design consistency.

## Delivery loop

Agents run as a shared **delivery loop** that turns a customer request into a delivered outcome. It is **iterative and spec-anchored**, not a one-time pass: each iteration delivers a thin, working increment against a slice of the requirements spec, the spec stays the living source of truth, and a **constitution** ([`constitution.md`](constitution.md)) plus a **project context / steering** artifact ([`context-template.md`](context-template.md)) are carried into every step. A task-decomposition step turns design into traceable tasks, and validation enforces a spec-conformance gate. Every agent file documents its position in the loop. See [`delivery-loop.md`](delivery-loop.md) for the full step-by-step, how to pass data between steps, and the rule that generated output must stay outside this catalog repository.

## Versioning and team updates

The agent setup is versioned so it stays clear which agents, at which versions, resolved a given customer request. Each agent carries a `version` in its frontmatter, the whole roster is captured as a versioned snapshot in [`team-manifest.md`](team-manifest.md), and changes are tracked in [`../CHANGELOG.md`](../CHANGELOG.md). The same scheme defines how to update the team over time — onboarding and offboarding agents in long-running projects. See [`versioning.md`](versioning.md) for the full policy.

## Communication standard

Although a customer request may be wordy and imprecise, the agents communicate
with each other — and write code — in a minimal, exact, and clear way to keep
token use low. See [`communication-standard.md`](communication-standard.md);
every agent file references it.

## Collaboration pattern

1. **Project delivery manager** and **agile delivery lead** steer the whole loop — scope, schedule, risk, and flow — while the **product manager** sets prioritization and direction.
2. **Business analyst** and **requirements engineer** structure the need, with the **user acceptance test expert** confirming acceptance criteria.
3. **Senior software architect**, **language-focused software developers** (including **mobile**), **senior software developer**, **UX and design expert**, and the **unit test expert** shape delivery, with the **data engineer**, **data analyst**, and **database administrator** handling data-driven work.
4. **Security engineer** and **compliance and data protection expert** review across design, implementation, and validation to keep delivery secure and compliant.
5. **Senior infrastructure architect**, **IT infrastructure expert**, and **devops release engineer** prepare environments, deployment, and releases, with the **integration and systems test expert** and **load and performance test expert** validating system behavior, scale, and readiness.
6. **Sales engineer**, **marketing and communications expert**, **social media expert**, and **customer success manager** support go-to-market, adoption, and retention, with the **technical writer** producing accompanying documentation.
7. **Customer support**, **purchasing expert**, **finance and controlling expert**, **engineering manager**, **people and talent expert**, and **legal and contracts expert** keep the business operational and scalable.

## Customization guidance

- Start with these outlines as baseline prompts.
- Expand tool access only when a role genuinely needs it.
- Keep naming kebab-case and group new agents by department.
- Add domain-specific examples once your internal workflows stabilize.
