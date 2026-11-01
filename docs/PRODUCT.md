# Product Definition — QuoteFlow AI

## 1. Product vision

Help small and medium-sized solar installation businesses prepare consistent quotation drafts faster by turning unstructured customer requests into validated, reviewable quote proposals.

## 2. Target user and problem

**Primary user:** a sales or operations employee at a solar installation company.

**Problem:** customer requests arrive in free text and often omit technical details. Staff must interpret the request, ask follow-up questions, select suitable catalog items, calculate a quote, and explain assumptions. This is repetitive and error-prone.

**Product promise:** accelerate the first draft while keeping product eligibility, arithmetic, and approval under explicit business control.

## 3. MVP user journey

1. Create a customer record.
2. Create a solar lead and paste/type the customer's request.
3. Ask the Quote Assistant to analyze the request.
4. Review extracted fields, confidence/uncertainty indicators, missing information, and assumptions.
5. Resolve missing information or explicitly proceed with marked assumptions where the workflow allows.
6. Match products from the configured demo catalog.
7. Calculate quote line items and totals in deterministic application code.
8. Review/edit the draft.
9. Approve or reject it as an authenticated human user.

## 4. MVP functional requirements

- Customer CRUD sufficient for the demo.
- Lead creation and request text capture.
- Structured requirement extraction with schema validation.
- Missing-information list with question suggestions.
- Product catalog with active status, category, attributes, SKU, unit, and configured price.
- Product matching based on explicit eligibility rules; LLM may explain matches but cannot invent catalog items.
- Quote draft with immutable price snapshots for its line items.
- Deterministic subtotal, configured tax, and total calculations.
- Human approval/rejection with actor and timestamp.
- Agent-run record containing safe input/output metadata and outcome.
- Useful loading, validation, empty, and failure states.

## 5. Solar domain boundaries

The MVP captures preliminary sales-intake information, such as:
- Installation address/postcode (synthetic in demo data).
- Property type and roof type, if known.
- Approximate electricity consumption, if known.
- Desired system size or customer goal, if known.
- Battery interest, if known.
- Existing constraints or customer notes.

These are intake fields, not engineering verification. The system must label unknown or inferred values. It must not claim that a configuration is technically suitable, compliant, structurally safe, or guaranteed to achieve a particular yield.

## 6. Non-functional requirements

- Clear separation between AI assistance and deterministic business rules.
- Predictable, explainable calculations.
- Traceability for agent runs and human approval.
- Responsive and accessible interface.
- Validated API contracts.
- Testable services with a mocked AI provider.
- No secrets or real customer data in source control.

## 7. MVP success criteria

A reviewer can complete the demo flow without editing the database manually. The app:
- extracts a valid structured request from a sample prompt;
- identifies at least one missing field or explicitly reports none;
- only recommends active catalog records that meet deterministic matching criteria;
- calculates totals reproducibly from stored price snapshots;
- creates a draft and requires a human action to approve;
- records the agent run and approval decision;
- handles malformed AI output and provider failure gracefully.

## 8. Product decisions

| ID | Decision |
|---|---|
| P-001 | Solar installation intake only in MVP; heating is out of scope. |
| P-002 | Guided single-agent workflow, orchestrated by backend code. |
| P-003 | AI creates structured suggestions and explanations, never binding prices. |
| P-004 | Product matching and all monetary calculations are application-owned. |
| P-005 | Every generated quote starts as `DRAFT`; human approval is explicit. |
| P-006 | Catalog and tax configuration are demo/configuration data, not market claims. |
| P-007 | Unknown information is represented as unknown, not silently fabricated. |
