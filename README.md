# AcmePay Developer Documentation (Portfolio Sample)

This repository is a **portfolio project** demonstrating how I write and structure **developer documentation** using a **docs-as-code** workflow.

> **Confidentiality note:** AcmePay is a fictional company and the API is non-functional. This doc set mirrors real-world API patterns (auth, errors, webhooks, idempotency) without using any client or proprietary information.

## Highlights (what this demonstrates)

- A clear onboarding path via a **Quickstart** (time-to-first-call focus)
- Production-grade API concepts: **errors**, **rate limits**, **idempotency**
- Integration guidance for **webhooks** including **signature verification**
- Reference-ready materials: **endpoint summaries**, **schemas**, and a minimal **OpenAPI 3.0 spec**
- Git-based workflow signals: Markdown, repo structure, contribution docs, PR template

## Audience

This documentation is written for:
- Developers integrating a payments API
- QA engineers testing payment flows in sandbox
- Solutions/support engineers troubleshooting integration issues

## Scope (v1)

Covered in this sample:
- Payments: create + retrieve
- Refunds: create
- Webhooks: endpoint registration + signature verification
- Core API concepts: authentication, errors, rate limits, idempotency

## Documentation map (start here)

- Home: [Docs index](docs/index.md)
- Tutorial: [Quickstart](docs/tutorials/quickstart.md)
- Concepts: [Authentication](docs/concepts/authentication.md) · [Errors](docs/concepts/errors.md) · [Rate limits](docs/concepts/rate-limits.md) · [Idempotency](docs/concepts/idempotency.md) · [Webhooks](docs/concepts/webhooks.md)
- How-to: [Create a payment](docs/how-to/create-payment.md) · [Refund a payment](docs/how-to/refund-payment.md) · [Verify a webhook signature](docs/how-to/verify-webhook-signature.md)
- Reference: [Endpoints](docs/reference/endpoints.md) · [Schemas](docs/reference/schemas.md)
- OpenAPI: [openapi/openapi.yaml](openapi/openapi.yaml)
- Postman: [postman/collection.json](postman/collection.json)

## How to review this documentation (recommended)

1. Start with the onboarding flow: [Quickstart](docs/tutorials/quickstart.md)
2. Review integration-critical concepts:
   - [Authentication](docs/concepts/authentication.md)
   - [Errors](docs/concepts/errors.md)
   - [Idempotency](docs/concepts/idempotency.md)
   - [Webhooks](docs/concepts/webhooks.md)
3. Skim the API coverage:
   - [Endpoints reference](docs/reference/endpoints.md)
   - [Schemas](docs/reference/schemas.md)

## Validate the OpenAPI spec (optional)

- File: [openapi/openapi.yaml](openapi/openapi.yaml)
- Validate in Swagger Editor: https://editor.swagger.io/

## Documentation structure (Diátaxis-style)

- Tutorials (learning): `/docs/tutorials`
- How-to guides (tasks): `/docs/how-to`
- Concepts (understanding): `/docs/concepts`
- Reference (lookup): `/docs/reference`

## Docs-as-code workflow

- Documentation lives in Markdown under `/docs`
- Changes are intended to go through branches + pull requests
- See:
  - [CONTRIBUTING.md](CONTRIBUTING.md)
  - [STYLE-GUIDE.md](STYLE-GUIDE.md)
  - PR template under `.github/`

## API overview (fictional)

**Base URLs**
- Sandbox: `https://api.sandbox.acmepay.example/v1`
- Production: `https://api.acmepay.example/v1`

**Authentication**
- `Authorization: Bearer <API_KEY>`

## License

You may reuse the structure and templates for your own portfolio. If you fork it, please keep the confidentiality note intact.
