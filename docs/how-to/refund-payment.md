# Refund a payment

Create a refund for an existing payment.

## Endpoint

`POST /v1/refunds`

## Prerequisites

- You must have the payment ID (for example, `pay_...`)
- Use idempotency to avoid duplicate refunds (see [Idempotency](../concepts/idempotency.md))

## Example request

```bash
curl -X POST "https://api.sandbox.acmepay.example/v1/refunds" \
  -H "Authorization: Bearer $ACMEPAY_API_KEY" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: 9b0a2b4c-b9c4-4bfa-9d59-0c8d53c5df11" \
  -d '{
    "payment_id": "pay_example_001",
    "amount": 2000,
    "reason": "requested_by_customer"
  }'
```

## Example response

```json
{
  "id": "rfnd_example_001",
  "object": "refund",
  "status": "succeeded",
  "payment_id": "pay_example_001",
  "amount": 2000,
  "created_at": "2026-01-09T12:10:00Z",
  "reason": "requested_by_customer"
}
```

## Troubleshooting

- If `payment_id` is invalid, you may get `404`: [Errors](../concepts/errors.md)
- If you retry a request, keep the same idempotency key: [Idempotency](../concepts/idempotency.md)