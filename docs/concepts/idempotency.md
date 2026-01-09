# Idempotency

Idempotency prevents duplicate charges when requests are retried (network timeouts, client retries, etc.).

## When to use idempotency

Use idempotency for any request that could create/charge something, such as:

- `POST /payments`
- `POST /refunds`

## How it works

Send a unique `Idempotency-Key` header with your request:

```http
Idempotency-Key: <unique-key>
```

If you retry the same request with the same Idempotency-Key, AcmePay returns the **same result** instead of creating a duplicate transaction.

## Requirements

- Use a UUID or similarly unique key
- Keep the key stable across retries for the same operation
- Do not reuse keys for different operations

## Conflict behavior

If you reuse an `Idempotency-Key` with a different payload, AcmePay returns a conflict error:

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "idempotency_conflict",
    "message": "Idempotency-Key was reused with a different request payload.",
    "request_id": "req_example_409",
    "docs_url": "https://docs.acmepay.example/idempotency"
  }
}
```

## Storage duration

Idempotency keys are retained for a limited window (for example, **24 hours**) in this sample design.