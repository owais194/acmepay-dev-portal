# Endpoints reference

This page summarizes the main AcmePay v1 endpoints.

Base URLs:
- Sandbox: `https://api.sandbox.acmepay.example/v1`
- Production: `https://api.acmepay.example/v1`

Authentication:
- `Authorization: Bearer <API_KEY>`

---

## Payments

### Create a payment

**POST** `/payments`

**Request body**

| Field | Type | Required | Description |
|---|---|---:|---|
| `amount` | integer | ✅ | Amount in smallest currency unit |
| `currency` | string | ✅ | ISO currency code (e.g., `USD`) |
| `payment_method.type` | string | ✅ | `card` |
| `payment_method.card.number` | string | ✅ | Test number in sandbox |
| `payment_method.card.exp_month` | integer | ✅ | 1-12 |
| `payment_method.card.exp_year` | integer | ✅ | 4-digit year |
| `payment_method.card.cvc` | string | ✅ | Card CVC |
| `metadata` | object | ❌ | Key-value metadata |

**Example**
- See: [Create a payment (how-to)](../how-to/create-payment.md)

---

### Retrieve a payment

**GET** `/payments/{payment_id}`

**Path params**

| Param | Type | Required | Description |
|---|---|---:|---|
| `payment_id` | string | ✅ | Payment identifier (e.g., `pay_...`) |

**Example**

```bash
curl -X GET "https://api.sandbox.acmepay.example/v1/payments/pay_example_001" \
  -H "Authorization: Bearer $ACMEPAY_API_KEY"
```

---

## Refunds

### Create a refund

**POST** `/refunds`

**Request body**

| Field | Type | Required | Description |
|---|---|---:|---|
| `payment_id` | string | ✅ | Payment ID to refund |
| `amount` | integer | ❌ | Refund amount (defaults to full) |
| `reason` | string | ❌ | Refund reason |

**Example**
- See: [Refund a payment (how-to)](../how-to/refund-payment.md)

---

## Webhooks

### Register a webhook endpoint

**POST** `/webhook-endpoints`

**Request body**

| Field | Type | Required | Description |
|---|---|---:|---|
| `url` | string | ✅ | Your HTTPS webhook receiver URL |
| `events` | array[string] | ✅ | Events you want to receive |

**Notes**
- Learn how to verify signatures: [Verify webhook signature](../how-to/verify-webhook-signature.md)

---

## Related

- [OpenAPI spec](../../openapi/openapi.yaml)
- [Schemas](schemas.md)
- [Errors](../concepts/errors.md)