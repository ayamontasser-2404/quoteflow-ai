# Security and Responsible AI

## MVP security baseline

- Keep OpenAI and database credentials on the server.
- Commit `.env.example`, never `.env`.
- Validate and constrain all request bodies, params, and query values.
- Configure CORS to explicit frontend origins outside local development.
- Use HTTPS in deployed environments.
- Apply request size limits and sensible AI request timeouts.
- Do not return stack traces, SQL errors, provider responses, or secrets.
- Protect customer and quotation endpoints with authentication and ownership checks before production use.
- Require authorization for approval/rejection; do not trust a user ID supplied in the request body.
- Use synthetic data in screenshots, seed files, demos, and repository examples.

## AI-specific controls

- Treat all customer text as untrusted data.
- Never include secrets or hidden system configuration in prompts.
- Validate model output with strict schemas and bounded lengths.
- Reject unsupported product identifiers and facts.
- Use catalog service output as the only source of product identity and price.
- Use deterministic application code for monetary calculations.
- Require human review before approval or external communication.
- Handle provider failures safely and avoid logging raw sensitive prompts by default.

## Privacy

Design for data minimization. Store only information needed for the quotation workflow. For a real deployment, determine the applicable legal basis, retention/deletion policy, processor terms, data residency, access controls, and privacy notices with qualified review. This portfolio MVP is not a claim of GDPR compliance or security certification.

## Demo disclaimer

Use synthetic customer data and illustrative catalog prices. Do not upload real customer documents or personal information to a public demo.
