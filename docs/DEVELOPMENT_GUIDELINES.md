# Development Guidelines

## Engineering principles

- Prefer readable, explicit code over clever abstractions.
- Keep modules cohesive and dependencies flowing inward toward domain logic.
- Keep HTTP concerns out of domain services.
- Keep provider SDK details behind an adapter.
- Keep AI prompts and schemas separate from orchestration.
- Never trust browser input, database JSON, or LLM output without validation.
- Avoid premature microservices, event buses, generic frameworks, and unnecessary dependencies.

## TypeScript

- Enable `strict`.
- Avoid `any`; use `unknown` at untrusted boundaries and narrow it.
- Model domain states with explicit unions/enums.
- Use decimal-safe money handling.
- Avoid business rules in React components and route handlers.
- Return typed service results or throw typed domain errors consistently.

## API

- Validate params, query, and body with Zod.
- Centralize error mapping.
- Do not expose stack traces or provider messages.
- Use correct status codes and stable error codes.
- Keep routes thin: parse/validate, call service, map response.

## AI integration

- AI provider calls occur server-side only.
- Use structured outputs where supported, then validate with Zod regardless.
- Set timeouts and bounded token/output limits.
- Support a mock provider for deterministic tests.
- Do not log secrets or unnecessary personal data.
- Record model and prompt version where useful.
- Never let model output directly mutate prices, approval state, permissions, or catalog records.

## Testing strategy

- Unit tests: calculator, matching rules, state transitions, schemas.
- API tests: Supertest for route behavior and error contracts.
- Agent tests: mocked provider for valid, invalid, missing-info, and provider-failure cases.
- E2E: Playwright for the primary user journey.
- Tests must not require a live OpenAI API key or network access.

## Definition of done

A task is done only when:
1. Acceptance criteria are met.
2. TypeScript build passes.
3. Relevant tests pass.
4. Error and edge cases are considered.
5. No unrelated files or dependencies were changed.
6. Docs/contracts are updated when behavior or decisions change.
7. The developer can explain the implementation and trade-offs.
