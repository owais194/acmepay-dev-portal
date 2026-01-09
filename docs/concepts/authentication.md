# Authentication

AcmePay uses **Bearer token authentication** for API requests.

## Header format

Include your API key in the `Authorization` header:

```http
Authorization: Bearer <API_KEY>
```

Example:

```bash
curl -X GET "https://api.sandbox.acmepay.example/v1/payments/pay_example" \
  -H "Authorization: Bearer sk_sandbox_example_123"
```

## Sandbox vs production

Use different API keys for sandbox and production.

- Sandbox base URL: `https://api.sandbox.acmepay.example/v1`
- Production base URL: `https://api.acmepay.example/v1`

## Security best practices

- Never commit API keys to Git.
- Rotate keys regularly.
- Treat API keys like passwords.
- Use least privilege (if your platform supports scoped keys).

## Common auth errors

- `401 Unauthorized`: missing or invalid key  
  See: [Errors](errors.md)