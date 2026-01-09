# Quickstart

Make your first AcmePay API call by creating a payment in the sandbox environment.

## What you'll do

1. Set your API key
2. Create a payment
3. Read the response
4. Understand what to do next

## Base URL

Sandbox base URL:

```
https://api.sandbox.acmepay.example/v1
```

## Authentication

AcmePay uses Bearer token authentication.

- Learn more: [Authentication](../concepts/authentication.md)

For this Quickstart, set your API key in an environment variable:

```bash
export ACMEPAY_API_KEY="sk_sandbox_example_123"
```

## Create a payment

Create a payment for **$19.99 USD**:

```bash
curl -X POST "https://api.sandbox.acmepay.example/v1/payments" \
  -H "Authorization: Bearer $ACMEPAY_API_KEY" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: 7b2c2a2f-2d1c-4b8c-9e70-1f22d90c0b3a" \
  -d '{
    "amount": 1999,
    "currency": "USD",
    "payment_method": {
      "type": "card",
      "card": {
        "number": "4242424242424242",
        "exp_month": 12,
        "exp_year": 2030,
        "cvc": "123"
      }
    },
    "metadata": {
      "order_id": "ORDER-10001"
    }
  }'
```

> `amount` is in the smallest currency unit (cents for USD).  
> Use [Idempotency](../concepts/idempotency.md) to prevent duplicate charges.

## Example response

```json
{
  "id": "pay_01J9Z8K6Y2G7K3T0XW7QJ2B3V0",
  "object": "payment",
  "status": "succeeded",
  "amount": 1999,
  "currency": "USD",
  "created_at": "2026-01-09T12:00:00Z",
  "metadata": {
    "order_id": "ORDER-10001"
  }
}
```

## Next steps

- Handle failures and retries: [Errors](../concepts/errors.md)
- Avoid duplicates on retries: [Idempotency](../concepts/idempotency.md)
- Receive real-time events: [Webhooks](../concepts/webhooks.md)
- Explore all endpoints: [Endpoints reference](../reference/endpoints.md)