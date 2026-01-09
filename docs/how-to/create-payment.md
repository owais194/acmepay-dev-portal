# Create a payment

Create a payment using a card payment method.

## Endpoint

`POST /v1/payments`

## Prerequisites

- API key configured (see [Authentication](../concepts/authentication.md))
- Use an idempotency key for safe retries (see [Idempotency](../concepts/idempotency.md))

## Example request

```bash
curl -X POST "https://api.sandbox.acmepay.example/v1/payments" \
  -H "Authorization: Bearer $ACMEPAY_API_KEY" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: 2fb1e2d7-63a2-4be2-a1d8-c6dcbf9f0b2a" \
  -d '{
    "amount": 4999,
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
      "customer_id": "cus_1001",
      "invoice_id": "inv_9001"
    }
  }'
```

## Example response

```json
{
  "id": "pay_example_001",
  "object": "payment",
  "status": "succeeded",
  "amount": 4999,
  "currency": "USD",
  "created_at": "2026-01-09T12:00:00Z",
  "metadata": {
    "customer_id": "cus_1001",
    "invoice_id": "inv_9001"
  }
}
```

## Troubleshooting

- If you get `401`, check your API key: [Errors](../concepts/errors.md)
- If you get `429`, back off and retry: [Rate limits](../concepts/rate-limits.md)