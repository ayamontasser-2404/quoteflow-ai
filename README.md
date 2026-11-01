# QuoteFlow AI

**AI-assisted quotation management for solar installation companies.**

QuoteFlow AI turns a customer's solar-installation request into a structured quotation draft. A guided AI workflow extracts requirements, identifies missing information, and explains recommendations. Application code—not the language model—matches catalog items, calculates prices, validates totals, and controls approval.

> **MVP boundary:** This is a portfolio demonstration, not a certified solar-design, engineering, tax, or production quotation system. Demo catalog data and calculations must be clearly labelled as illustrative.

## Product outcome

A user can:
1. Create or select a customer and solar lead.
2. Enter a customer's installation request.
3. Run guided AI analysis to extract structured requirements.
4. Review missing information and assumptions.
5. Match eligible catalog products using application rules.
6. Generate a draft with deterministic line-item calculations.
7. Edit the draft and approve or reject it as a human.

## Non-goals for the MVP

- Autonomous agent loops or multi-agent collaboration.
- Automated engineering design, roof-layout simulation, yield guarantees, or grid-connection advice.
- Live supplier integrations, inventory, purchasing, or installation scheduling.
- Sending binding offers to customers automatically.
- Automatic tax/legal decisions. Tax rates and currency are configuration, not model guesses.
- Heating products or workflows (future extension only).

## Architecture at a glance

- **Web:** React + TypeScript + Vite.
- **API:** Node.js + Express + TypeScript.
- **Persistence:** PostgreSQL + Prisma.
- **Validation:** Zod at external and AI boundaries.
- **AI:** OpenAI API behind a provider adapter; structured outputs validated by Zod.
- **Tests:** Vitest, Supertest, and Playwright for the critical end-to-end flow.

The backend owns workflow orchestration. The LLM is used for language understanding and explanation, not pricing, authorization, or approval.

## Repository layout

```text
quoteflow-ai/
├── apps/
│   ├── web/                       # React client
│   └── api/                       # Express API
├── docs/                           # Product and engineering source of truth
├── .cursor/
│   └── rules/                      # Scoped AI coding rules
├── .github/workflows/              # CI
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

## Documentation source of truth

Read these before implementation and update them when decisions change:

| Document | Authority |
|---|---|
| `docs/PRODUCT.md` | Product goals, users, scope, workflow, acceptance criteria |
| `docs/ARCHITECTURE.md` | System boundaries, components, data flow, architecture decisions |
| `docs/AI_AGENT.md` | Agent contract, skills, prompts, failure modes, human control |
| `docs/DATA_MODEL.md` | Domain entities, relationships, invariants |
| `docs/API_CONTRACT.md` | API routes, payloads, status codes, error shape |
| `docs/DEVELOPMENT_GUIDELINES.md` | Code conventions, testing, definition of done |
| `docs/SECURITY.md` | Privacy, secrets, validation, authorization, AI safety |
| `docs/ROADMAP.md` | Milestones, sequencing, acceptance gates |

If code and documentation disagree, do not silently choose one: identify the discrepancy, propose a decision, update the relevant document, then implement. Tests describe verified behavior; they do not by themselves authorize changing product intent.

## Local development

Prerequisites: Node.js 22+, npm, PostgreSQL, and an OpenAI API key for live AI functionality.

Setup commands will be added after the monorepo workspace and application scaffolds are created. Copy `.env.example` to a local `.env` (never commit secrets). The AI integration must support a deterministic mock mode so core tests do not require network access or API credentials.

## Quality gates

Before a feature is considered complete:
- TypeScript build passes.
- Relevant unit and API tests pass.
- Inputs and AI outputs are validated.
- Errors are handled without leaking secrets or internal stack traces.
- Loading, empty, success, and failure UI states are considered.
- Documentation and API contracts reflect the implementation.
- No real customer personal data is committed to the repository.

## Demo story

Use synthetic customer and catalog data. Demonstrate one request from initial intake through AI extraction, missing-information review, product matching, deterministic calculation, draft editing, and explicit human approval. Explain which decisions are made by the model and which are enforced by application code.
