# Verify a webhook signature

This guide shows how to verify AcmePay webhook signatures using HMAC-SHA256.

## What you need

- Your webhook signing secret (for example, `whsec_...`)
- The raw request body (string/bytes, not parsed JSON)
- The `X-AcmePay-Signature` header

## Signature header format

```http
X-AcmePay-Signature: t=1736424300,v1=<hex_digest>
```

## Signing algorithm (AcmePay sample)

1. Create the signed payload string:

```
signed_payload = "{timestamp}.{raw_body}"
```

2. Compute:

- `digest = HMAC_SHA256(secret, signed_payload)` as hex

3. Compare `digest` to `v1` using a constant-time comparison.

## Node.js example

```js
import crypto from "crypto";

function parseSignatureHeader(headerValue) {
  const parts = headerValue.split(",").reduce((acc, item) => {
    const [k, v] = item.split("=");
    acc[k] = v;
    return acc;
  }, {});
  return { t: parts.t, v1: parts.v1 };
}

export function verifyAcmePayWebhook({ rawBody, signatureHeader, secret }) {
  const { t, v1 } = parseSignatureHeader(signatureHeader);
  const signedPayload = `${t}.${rawBody}`;

  const expected = crypto
    .createHmac("sha256", secret)
    .update(signedPayload, "utf8")
    .digest("hex");

  const a = Buffer.from(expected, "utf8");
  const b = Buffer.from(v1, "utf8");
  if (a.length !== b.length) return false;
  return crypto.timingSafeEqual(a, b);
}
```

## Python example

```py
import hmac
import hashlib

def parse_signature_header(header_value: str):
    parts = {}
    for item in header_value.split(","):
        k, v = item.split("=")
        parts[k] = v
    return parts["t"], parts["v1"]

def verify_acmepay_webhook(raw_body: bytes, signature_header: str, secret: str) -> bool:
    t, v1 = parse_signature_header(signature_header)
    signed_payload = (t + ".").encode("utf-8") + raw_body

    expected = hmac.new(
        key=secret.encode("utf-8"),
        msg=signed_payload,
        digestmod=hashlib.sha256
    ).hexdigest()

    return hmac.compare_digest(expected, v1)
```

## Failure handling

- If verification fails, respond with `400 Bad Request` (don’t process the event).
- Log a correlation ID (and/or `request_id` if your platform includes it).