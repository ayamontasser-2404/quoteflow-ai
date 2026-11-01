# Roadmap — Two-Day Portfolio MVP

## Phase 0 — Foundation
- [x] Confirm guided single-agent approach.
- [x] Confirm solar-only MVP.
- [ ] Review and commit product/architecture/agent contracts.
- [ ] Create repository and Cursor rules.
- [ ] Scaffold npm workspaces and apps.

## Day 1 — Working product workflow
1. Backend foundation: Express app, health endpoint, error handling, tests.
2. Persistence: PostgreSQL, Prisma schema, migration, synthetic seed data.
3. Domain APIs: customers, leads, products.
4. Core domain services: product matching and deterministic quote calculator with unit tests.
5. Minimal React dashboard: customers/leads/catalog/quotation view.

## Day 2 — AI, review, delivery
1. OpenAI provider adapter and mock provider.
2. Requirement extraction schema and prompt.
3. Missing-information flow.
4. Agent orchestration and AgentRun persistence.
5. Draft creation, editing, human approval/rejection.
6. API and end-to-end tests.
7. Deployment, README screenshots/demo instructions, architecture explanation.

## Release gates

**Gate A — backend foundation:** health endpoint, build and tests pass.

**Gate B — deterministic business core:** matching and calculator tests pass; prices are not model-generated.

**Gate C — AI workflow:** structured output is validated; missing information blocks quote generation; provider failures are handled.

**Gate D — human control:** generated quote remains draft; approval requires an authorized human action.

**Gate E — deployable demo:** synthetic seed data, environment configuration, CI, deployment, and reproducible demo steps.

## Scope protection

If time is constrained, prioritize a complete, testable vertical slice over breadth. Defer authentication integrations, PDF generation, email sending, streaming, advanced analytics, supplier APIs, and multi-agent orchestration. Do not remove validation, deterministic pricing, or human approval to save time.
