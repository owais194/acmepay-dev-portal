# Rate limits

AcmePay enforces rate limits to protect platform reliability and ensure fair usage.

## Default limits (sandbox)

- **100 requests per minute** per API key
- Burst behavior may be restricted

## Rate limit headers

Responses may include:

- `X-RateLimit-Limit`: max requests allowed in the window
- `X-RateLimit-Remaining`: remaining requests in the window
- `X-RateLimit-Reset`: unix timestamp when the window resets

## 429 response

If you exceed the limit, you receive `429 Too Many Requests`:

```json
{
  "error": {
    "type": "rate_limit_error",
    "code": "rate_limited",
    "message": "Too many requests. Please retry after the rate limit resets.",
    "request_id": "req_example_429",
    "docs_url": "https://docs.acmepay.example/rate-limits"
  }
}
```

## Retry strategy

Recommended approach:

1. Wait until reset (or use `Retry-After` if provided)
2. Retry with exponential backoff
3. Add jitter to avoid synchronized retries

Example backoff schedule: 1s → 2s → 4s → 8s (with jitter)