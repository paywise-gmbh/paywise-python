# paywise Python SDK

[![PyPI](https://img.shields.io/pypi/v/paywise)](https://pypi.org/project/paywise/)

Official Python client for the paywise **Case Management API v2** and **Partner API v2**.

- API documentation: https://docs.paywise.de
- Specs and SDK configuration: [paywise-gmbh/developer-resources](https://github.com/paywise-gmbh/developer-resources)

> This SDK is generated with [Fern](https://buildwithfern.com) from the published OpenAPI specs. Please open issues and pull requests in [developer-resources](https://github.com/paywise-gmbh/developer-resources), not against the generated code here.

## Installation

```sh
pip install paywise
```

Requires Python 3.10 or newer.

## Usage

```python
import os
from paywise import Paywise, PaywiseEnvironment

client = Paywise(
    environment=PaywiseEnvironment.SANDBOX,  # or PaywiseEnvironment.PRODUCTION (default)
    token=os.environ["PAYWISE_API_KEY"],
)

health = client.case_management.health.check()
```

Both APIs share one client:

- `client.case_management.*` — claims, orders, mandates, debtors, payments, statements, webhooks, …
- `client.partner.*` — managed companies, company users, usage, webhooks, …

An async client with the same interface is available as `AsyncPaywise`.

### Acting on behalf of a company (Partner keys)

Partner keys call the Case Management API for a managed company by sending `X-On-Behalf-Of-Company`. Set it once on the client:

```python
company_client = Paywise(
    environment=PaywiseEnvironment.SANDBOX,
    token=os.environ["PAYWISE_PARTNER_API_KEY"],
    on_behalf_of_company="<company id>",
)
```

Direct Case Management keys must not send this header.

### Pagination

List methods return a pager that iterates across all pages:

```python
for claim in client.case_management.claims.list_claims(limit=50):
    print(claim.id)
```

Use `.iter_pages()` to work page by page.

### Errors

Non-2xx responses raise a typed error per status code (for example `paywise.case_management.UnauthorizedError`), all subclasses of `paywise.core.ApiError`:

```python
from paywise.core import ApiError

try:
    client.case_management.claims.list_claims()
except ApiError as err:
    print(err.status_code, err.body)
```

### Retries and idempotency

Failed requests (408, 409, 429, 5xx) are retried twice by default (`max_retries` on the client or per request via `request_options`), honouring `Retry-After`. Write operations that accept an `Idempotency-Key` take it as a parameter, and retries reuse the same key.

## Reference

The full list of methods is in [reference.md](./reference.md).

## License

MIT — see [LICENSE](./LICENSE).
