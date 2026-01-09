# AcmePay Developer Documentation (Portfolio Sample)

This repository is a **portfolio project** that demonstrates how I write and structure developer documentation using a **docs-as-code** workflow.

> **Confidentiality note:** AcmePay is a fictional company and the API is non-functional. This documentation is intentionally designed to mirror real-world patterns (auth, errors, webhooks, idempotency) without disclosing any client or proprietary information.

## What this repo demonstrates

- Clear developer onboarding via a **Quickstart**
- Realistic API concepts: **Authentication**, **Errors**, **Rate limits**, **Idempotency**
- Production-grade integration patterns: **Webhooks + signature verification**
- Reference material and schemas
- Docs-as-code practices: Markdown structure, contribution docs, PR template
- A minimal **OpenAPI 3.0** spec and Postman collection

## Start here

- 📌 [Documentation Home](docs/index.md)
- 🚀 [Quickstart](docs/tutorials/quickstart.md)
- 🔐 [Authentication](docs/concepts/authentication.md)
- ❗ [Errors](docs/concepts/errors.md)
- 🔁 [Idempotency](docs/concepts/idempotency.md)
- 🪝 [Webhooks](docs/concepts/webhooks.md)
- 📚 [Endpoints Reference](docs/reference/endpoints.md)
- 🧩 [Schemas](docs/reference/schemas.md)
- 🧾 [OpenAPI spec](openapi/openapi.yaml)
- 🧪 [Postman collection](postman/collection.json)

## API overview (fictional)

**Base URLs**
- Sandbox: `https://api.sandbox.acmepay.example/v1`
- Production: `https://api.acmepay.example/v1`

**Auth**
- `Authorization: Bearer <API_KEY>`

## License

You may reuse the structure and templates for your own portfolio. If you fork it, please keep the confidentiality note intact.