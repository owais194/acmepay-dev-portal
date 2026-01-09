# Errors

AcmePay uses standard HTTP status codes and a consistent JSON error format.

## Error format

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "invalid_request",
    "message": "amount must be greater than 0",
    "param": "amount",
    "request_id": "req_01J9Z8Q0WJ9R4F7N2Y0W9QK6H9",
    "docs_url": "https://docs.acmepay.example/errors#invalid_request"
  }
}
```

## HTTP status codes

| Status | Meaning | What to do |
|---:|---|---|
| 400 | Bad Request | Fix validation issues, missing fields, invalid formats. |
| 401 | Unauthorized | Check the `Authorization` header and API key. |
| 403 | Forbidden | Your key lacks permissions for the action. |
| 404 | Not Found | Verify the resource ID (for example, `pay_...`). |
| 409 | Conflict | Often due to idempotency misuse or state conflicts. |
| 422 | Unprocessable Entity | Inputs are syntactically valid but semantically invalid. |
| 429 | Too Many Requests | Back off and retry. See [Rate limits](rate-limits.md). |
| 500 | Internal Server Error | Retry with backoff; contact support if persistent. |

## Common error codes

| Code | Meaning |
|---|---|
| `invalid_request` | Required fields missing or invalid. |
| `authentication_failed` | API key missing, invalid, or revoked. |
| `permission_denied` | Access blocked by permissions or policy. |
| `resource_not_found` | Requested resource ID does not exist. |
| `rate_limited` | Too many requests. |
| `idempotency_conflict` | Same Idempotency-Key used with different payload. |

## Example: validation error (400)

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "invalid_request",
    "message": "currency must be a 3-letter ISO code",
    "param": "currency",
    "request_id": "req_example_001",
    "docs_url": "https://docs.acmepay.example/errors#invalid_request"
  }
}
```

## Example: auth error (401)

```json
{
  "error": {
    "type": "authentication_error",
    "code": "authentication_failed",
    "message": "Invalid API key",
    "request_id": "req_example_002",
    "docs_url": "https://docs.acmepay.example/errors#authentication_failed"
  }
}
```

## Handling errors (recommended)

- Log `request_id` to correlate issues with server logs.
- Retry only when appropriate:
  - ✅ Retry: `429`, `500`, `503`
  - ❌ Don’t retry blindly: `400`, `401`, `403`, `404`
- Use exponential backoff for retries.