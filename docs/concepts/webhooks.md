# Webhooks

Webhooks let AcmePay notify your system when events happen, such as a successful payment or a refund.

## Common use cases

- Confirm payment success asynchronously
- Update order status
- Trigger email receipts
- Reconcile refunds

## Webhook events

Example events (fictional):

| Event | Description |
|---|---|
| `payment.succeeded` | A payment completed successfully |
| `payment.failed` | A payment attempt failed |
| `refund.created` | A refund was created |

## Webhook payload format

```json
{
  "id": "evt_01J9Z9ABCDE1234567890",
  "type": "payment.succeeded",
  "created_at": "2026-01-09T12:05:00Z",
  "data": {
    "object": {
      "id": "pay_01J9Z8K6Y2G7K3T0XW7QJ2B3V0",
      "status": "succeeded",
      "amount": 1999,
      "currency": "USD"
    }
  }
}
```

## Delivery and retries

Recommended behavior for production-grade systems:

- You must respond with **2xx** quickly to acknowledge receipt.
- If you respond with non-2xx, AcmePay retries with backoff (example):
  - 10s, 30s, 2m, 10m, 1h (max 24h total)

## Signature verification

AcmePay signs webhook requests so you can verify authenticity.

Example signature header:

```http
X-AcmePay-Signature: t=1736424300,v1=5d41402abc4b2a76b9719d911017c592
```

Verification overview:

1. Extract `t` and `v1` from the header
2. Compute HMAC-SHA256 over: `"{t}.{raw_body}"`
3. Compare your computed digest to `v1` using a constant-time compare

Step-by-step guide:

- [Verify a webhook signature](../how-to/verify-webhook-signature.md)