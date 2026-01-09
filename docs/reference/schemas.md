# Schemas

This page describes key object schemas used in AcmePay.

For the OpenAPI definition, see: [openapi.yaml](../../openapi/openapi.yaml)

---

## Payment

```json
{
  "id": "pay_...",
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

**Fields**

| Field | Type | Description |
|---|---|---|
| `id` | string | Payment identifier |
| `object` | string | Always `payment` |
| `status` | string | `requires_action`, `processing`, `succeeded`, `failed` |
| `amount` | integer | Smallest currency unit |
| `currency` | string | ISO code |
| `created_at` | string | ISO-8601 timestamp |
| `metadata` | object | Custom key-value data |

---

## Refund

```json
{
  "id": "rfnd_...",
  "object": "refund",
  "status": "succeeded",
  "payment_id": "pay_...",
  "amount": 2000,
  "created_at": "2026-01-09T12:10:00Z",
  "reason": "requested_by_customer"
}
```

---

## WebhookEvent

```json
{
  "id": "evt_...",
  "type": "payment.succeeded",
  "created_at": "2026-01-09T12:05:00Z",
  "data": {
    "object": {
      "id": "pay_...",
      "status": "succeeded",
      "amount": 1999,
      "currency": "USD"
    }
  }
}
```

---

## Error

```json
{
  "error": {
    "type": "invalid_request_error",
    "code": "invalid_request",
    "message": "amount must be greater than 0",
    "param": "amount",
    "request_id": "req_...",
    "docs_url": "https://docs.acmepay.example/errors#invalid_request"
  }
}
```