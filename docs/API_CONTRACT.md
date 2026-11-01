# API Contract — MVP

Prefix: `/api`. JSON request and response bodies. All request inputs and external outputs are validated. Exact field schemas will be implemented with Zod and kept synchronized with this document.

## Conventions

- Use plural resource names.
- Return appropriate HTTP status codes.
- Use ISO-8601 UTC timestamps.
- Never return stack traces, secrets, raw provider errors, or internal database details.
- Paginate list endpoints if the dataset can grow; document pagination before implementation.
- Authentication/authorization must protect customer data and approval actions before any production claim.

## Initial endpoints

| Method | Path | Purpose |
|---|---|---|
| `GET` | `/api/health` | Service health |
| `GET` | `/api/customers` | List customers |
| `POST` | `/api/customers` | Create customer |
| `GET` | `/api/customers/:id` | Get customer |
| `POST` | `/api/leads` | Create lead |
| `GET` | `/api/leads/:id` | Get lead and intake status |
| `GET` | `/api/products` | List active catalog products |
| `POST` | `/api/agent/quote-drafts` | Start guided analysis and draft workflow |
| `GET` | `/api/agent/runs/:id` | Get agent-run status/result |
| `GET` | `/api/quotations/:id` | Get quotation |
| `PATCH` | `/api/quotations/:id` | Edit permitted draft fields |
| `POST` | `/api/quotations/:id/approve` | Human approval |
| `POST` | `/api/quotations/:id/reject` | Human rejection |

## Agent request example

`POST /api/agent/quote-drafts`

```json
{
  "leadId": "lead_123",
  "additionalInformation": "The customer is interested in adding a battery."
}
```

The API loads the lead and its context server-side. Do not trust client-supplied catalog prices or customer ownership.

## Agent response: clarification required

```json
{
  "status": "NEEDS_INFORMATION",
  "agentRunId": "run_123",
  "missingInformation": [
    {
      "field": "annualConsumptionKwh",
      "question": "Do you know the property's approximate annual electricity consumption?"
    }
  ]
}
```

## Agent response: draft created

```json
{
  "status": "DRAFT_CREATED",
  "agentRunId": "run_124",
  "quotationId": "quote_123",
  "currency": "EUR",
  "items": [],
  "subtotal": "0.00",
  "taxAmount": "0.00",
  "total": "0.00",
  "assumptions": [],
  "explanation": "Illustrative draft explanation."
}
```

The example values are contract illustrations, not actual prices or tax policy. Use decimal strings for money at API boundaries.

## Error response

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request is invalid.",
    "details": []
  }
}
```

## Status code guidance

- `200`: successful read/update/action.
- `201`: resource created.
- `400`: malformed or invalid request.
- `401`: unauthenticated.
- `403`: authenticated but not authorized.
- `404`: resource not found.
- `409`: invalid state transition or conflict.
- `422`: valid request that cannot proceed due to missing business requirements.
- `429`: rate limited.
- `500`: unexpected internal error.
- `502`/`503`: upstream AI provider unavailable or failed, mapped to a safe public error.

## Contract governance

Update this file and the Zod schemas together when endpoint behavior changes. Add Supertest coverage for status codes, response schemas, validation failures, not-found cases, and authorization boundaries.
