# Reference

## Claims

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">list_claims</a>(...) -> PaginatedClaimList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Claims addressed by their stable UUID and current relationships.

Read claims throughout their lifecycle using URLs that remain valid after
internal order moves. Standalone creation requires a draft `order_id`;
the relationship is read-only thereafter. Create, PATCH, and DELETE require
a draft order and otherwise return `409 claim_not_editable`. An expired
draft instead returns `409 order_expired`. Tenant-scoped by the
authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.list_claims()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**document_reference:** `typing.Optional[str]` — Exact match on the document reference (e.g. the invoice number), ignoring case and surrounding whitespace.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**order_id:** `typing.Optional[str]` — Filter claims by their parent order's UUID.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListClaimsRequestStatus]`

- `draft` - draft
- `submitted` - submitted
- `awaiting_client_response` - awaiting_client_response
- `accepted` - accepted
- `rejected` - rejected
- `withdrawn` - withdrawn

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Exact match on your claim reference, ignoring case and surrounding whitespace.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">create_claim</a>(...) -> Claim</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Claims addressed by their stable UUID and current relationships.

Read claims throughout their lifecycle using URLs that remain valid after
internal order moves. Standalone creation requires a draft `order_id`;
the relationship is read-only thereafter. Create, PATCH, and DELETE require
a draft order and otherwise return `409 claim_not_editable`. An expired
draft instead returns `409 order_expired`. Tenant-scoped by the
authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import StandaloneClaimCreateRequest_Receivable, ClaimPrincipalAmountWriteRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.create_claim(
    idempotency_key="Idempotency-Key",
    request=StandaloneClaimCreateRequest_Receivable(
        is_disputed=True,
        order_id="order_id",
        principal_amount=ClaimPrincipalAmountWriteRequest(
            value="value",
        ),
    ),
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `StandaloneClaimCreateRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">get_enforceable_title</a>(...) -> EnforceableTitleRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The enforceable-title singleton owned by a titled claim.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.get_enforceable_title(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">replace_enforceable_title</a>(...) -> EnforceableTitleRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The enforceable-title singleton owned by a titled claim.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.replace_enforceable_title(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**amount:** `typing.Optional[TitleAmountWriteRequest]` — Gross amount confirmed by the client and owned by the enforceable title. May be absent or null while drafting; must be positive before finalization.

</dd>
</dl>

<dl>
<dd>

**file_number:** `typing.Optional[str]` — Official file or reference number shown on the title. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**issued_on:** `typing.Optional[datetime.date]` — Date on which the enforceable title was issued. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**issuing_authority:** `typing.Optional[str]` — Court, notary, or other authority that issued the title. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**legally_binding_since:** `typing.Optional[datetime.date]` — Optional date from which the title is legally binding; it cannot precede issued_on.

</dd>
</dl>

<dl>
<dd>

**served_on:** `typing.Optional[datetime.date]` — Optional date on which the title was served; it cannot precede issued_on.

</dd>
</dl>

<dl>
<dd>

**title_type:** `typing.Optional[TitleTypeEnum]` — Legal title category: enforcement_order = Vollstreckungsbescheid; default_judgment = Versäumnisurteil; final_judgment = Endurteil; acknowledgment_judgment = Anerkenntnisurteil; reservation_judgment = Vorbehaltsurteil; court_settlement = Gerichtlicher Vergleich; enforceable_notarial_deed = Vollstreckbare notarielle Urkunde; cost_assessment_order = Kostenfestsetzungsbeschluss; other = Sonstiger Titel. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">delete_enforceable_title</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The enforceable-title singleton owned by a titled claim.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.delete_enforceable_title(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">update_enforceable_title</a>(...) -> EnforceableTitleRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The enforceable-title singleton owned by a titled claim.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
import datetime

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.update_enforceable_title(
    claim_id="claim_id",
    legally_binding_since=datetime.date.fromisoformat("2026-02-15"),
    served_on=datetime.date.fromisoformat("2026-02-12"),
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**amount:** `typing.Optional[TitleAmountWriteRequest]` — Gross amount confirmed by the client and owned by the enforceable title. May be absent or null while drafting; must be positive before finalization.

</dd>
</dl>

<dl>
<dd>

**file_number:** `typing.Optional[str]` — Official file or reference number shown on the title. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**issued_on:** `typing.Optional[datetime.date]` — Date on which the enforceable title was issued. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**issuing_authority:** `typing.Optional[str]` — Court, notary, or other authority that issued the title. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**legally_binding_since:** `typing.Optional[datetime.date]` — Optional date from which the title is legally binding; it cannot precede issued_on.

</dd>
</dl>

<dl>
<dd>

**served_on:** `typing.Optional[datetime.date]` — Optional date on which the title was served; it cannot precede issued_on.

</dd>
</dl>

<dl>
<dd>

**title_type:** `typing.Optional[TitleTypeEnum]` — Legal title category: enforcement_order = Vollstreckungsbescheid; default_judgment = Versäumnisurteil; final_judgment = Endurteil; acknowledgment_judgment = Anerkenntnisurteil; reservation_judgment = Vorbehaltsurteil; court_settlement = Gerichtlicher Vergleich; enforceable_notarial_deed = Vollstreckbare notarielle Urkunde; cost_assessment_order = Kostenfestsetzungsbeschluss; other = Sonstiger Titel. Required before finalization.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">list_enforceable_title_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a titled claim's enforceable title.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.list_enforceable_title_documents(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">create_enforceable_title_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a titled claim's enforceable title.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.create_enforceable_title_document(
    claim_id="claim_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="enforceable_title",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `EnforceableTitleDocumentTypeEnum` — Title document purpose: enforceable_title is the single primary title document, required before finalization; other supplies a supporting document and may be used multiple times.

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">get_enforceable_title_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a titled claim's enforceable title.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.get_enforceable_title_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">delete_enforceable_title_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a titled claim's enforceable title.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.delete_enforceable_title_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">download_enforceable_title_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a titled claim's enforceable title.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.download_enforceable_title_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">list_claim_payments</a>(...) -> PaginatedPaymentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Client payments recorded on one claim across its whole lifecycle.

Draft and in-review orders take side-effect-free claim facts; once the
claim carries a mandate the create delegates to the shared claim payment
report. Deletion stays draft-only. Requires `case:payments:write` to report
or delete and `case:payments:read` to list, in every lifecycle state.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.list_claim_payments(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">create_claim_payment</a>(...) -> PaymentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Client payments recorded on one claim across its whole lifecycle.

Draft and in-review orders take side-effect-free claim facts; once the
claim carries a mandate the create delegates to the shared claim payment
report. Deletion stays draft-only. Requires `case:payments:write` to report
or delete and `case:payments:read` to list, in every lifecycle state.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import PaymentAmountWriteRequest, PaymentMetadataWriteRequest
import datetime

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.create_claim_payment(
    claim_id="claim_id",
    idempotency_key="Idempotency-Key",
    amount=PaymentAmountWriteRequest(
        currency="EUR",
        value="50.00",
    ),
    metadata=[
        PaymentMetadataWriteRequest(
            type="transaction:reference",
            value="BANK-TRANSACTION-99812",
        )
    ],
    value_date=datetime.date.fromisoformat("2026-07-17"),
    your_reference="BANK-TRANSACTION-99812",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `PaymentWriteRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">delete_claim_payment</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Client payments recorded on one claim across its whole lifecycle.

Draft and in-review orders take side-effect-free claim facts; once the
claim carries a mandate the create delegates to the shared claim payment
report. Deletion stays draft-only. Requires `case:payments:write` to report
or delete and `case:payments:read` to list, in every lifecycle state.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.delete_claim_payment(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — UUID of the parent claim in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the payment in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">get_claim</a>(...) -> Claim</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Claims addressed by their stable UUID and current relationships.

Read claims throughout their lifecycle using URLs that remain valid after
internal order moves. Standalone creation requires a draft `order_id`;
the relationship is read-only thereafter. Create, PATCH, and DELETE require
a draft order and otherwise return `409 claim_not_editable`. An expired
draft instead returns `409 order_expired`. Tenant-scoped by the
authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.get_claim(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">delete_claim</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Claims addressed by their stable UUID and current relationships.

Read claims throughout their lifecycle using URLs that remain valid after
internal order moves. Standalone creation requires a draft `order_id`;
the relationship is read-only thereafter. Create, PATCH, and DELETE require
a draft order and otherwise return `409 claim_not_editable`. An expired
draft instead returns `409 order_expired`. Tenant-scoped by the
authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.delete_claim(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.claims.<a href="src/paywise/case_management/claims/client.py">update_claim</a>(...) -> Claim</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Claims addressed by their stable UUID and current relationships.

Read claims throughout their lifecycle using URLs that remain valid after
internal order moves. Standalone creation requires a draft `order_id`;
the relationship is read-only thereafter. Create, PATCH, and DELETE require
a draft order and otherwise return `409 claim_not_editable`. An expired
draft instead returns `409 order_expired`. Tenant-scoped by the
authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
import datetime

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.claims.update_claim(
    id="id",
    due_date=datetime.date.fromisoformat("2026-06-26"),
    subject_matter="Website accessibility consulting in June 2026 (rev. 2)",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the claim in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**additional_charges:** `typing.Optional[typing.List[ClaimChargeWriteRequest]]` — Itemized incidental charges for a receivable claim, such as reminder or bank fees. This array replaces all existing charges; [] clears them and omission preserves them. Maximum 50 entries per claim.

</dd>
</dl>

<dl>
<dd>

**delay_date:** `typing.Optional[datetime.date]` — Payment-default date for a receivable claim. For H17/H19 rent, an explicit date overrides the derived day after due_date and null restores derivation. For other receivables, null clears it; changing document_date, due_date, or reminders without supplying delay_date recalculates it. An explicit date must follow the applicable due or reminder date.

</dd>
</dl>

<dl>
<dd>

**dispute_reason:** `typing.Optional[str]` — Debtor's stated reason for disputing the claim. The resulting disputed claim must have a non-blank reason; an existing reason satisfies this requirement when omitted from PATCH. Setting is_disputed to false clears the existing reason unless you supply this field, which must then be empty or null.

</dd>
</dl>

<dl>
<dd>

**document_date:** `typing.Optional[datetime.date]` — Date of the invoice, contract, or other claim document. For H17/H19 rent, supply the first day of the rental month; only one rental claim per calendar month is allowed. Only valid for receivable claims. Required and cannot be in the future at finalization.

</dd>
</dl>

<dl>
<dd>

**document_reference:** `typing.Optional[str]` — Invoice, contract, or other source-document number.

</dd>
</dl>

<dl>
<dd>

**due_date:** `typing.Optional[datetime.date]` — Date on which a receivable claim became due. For H17/H19 rent, an explicit date overrides the agreement rule, null restores derivation, and omission preserves the current date or its existing derivation. For other receivables it cannot precede document_date.

</dd>
</dl>

<dl>
<dd>

**is_disputed:** `typing.Optional[bool]` — Whether the debtor disputes the claim. Setting false also clears the existing dispute_reason unless you supply that field explicitly.

</dd>
</dl>

<dl>
<dd>

**items:** `typing.Optional[typing.List[ClaimItemWriteRequest]]` — Invoice or contract lines for a receivable claim. This array replaces all existing lines; [] clears them and omission preserves them. Supply principal_amount separately when the principal changes. Maximum 100 entries per claim.

</dd>
</dl>

<dl>
<dd>

**legal_basis:** `typing.Optional[ClaimLegalBasisWriteRequest]` — Contract or obligation establishing a receivable claim. Supplied properties update the existing legal basis; omitted properties stay unchanged. Not valid on titled claims or on receivable enforcement costs in titled orders, which always use K014.

</dd>
</dl>

<dl>
<dd>

**principal_amount:** `typing.Optional[ClaimPrincipalAmountWriteRequest]` — Replacement principal amount including VAT, before charges and payments. Only valid for receivable claims; titled claims use their enforceable-title amount. Changing items does not update this amount. The principal must be positive before finalization.

</dd>
</dl>

<dl>
<dd>

**reminders:** `typing.Optional[typing.List[ClaimReminderWriteRequest]]` — Payment reminders for a receivable claim, in chronological order starting no earlier than its due date (or document date when due_date is absent). This array replaces all reminders; [] clears them and omission preserves them. Retain existing entries with their id. Maximum 50 entries per claim.

</dd>
</dl>

<dl>
<dd>

**subject_matter:** `typing.Optional[str]` — Goods, services, or other obligation underlying the claim. Before finalization, a receivable claim must have non-blank subject_matter or at least one claim document. Maximum 2000 characters.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Your reference for this claim.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Documents

<details><summary><code>client.case_management.documents.<a href="src/paywise/case_management/documents/client.py">list_claim_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.documents.list_claim_documents(
    claim_id="claim_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — ID of the parent claim.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.documents.<a href="src/paywise/case_management/documents/client.py">create_claim_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.documents.create_claim_document(
    claim_id="claim_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="bank_statement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — ID of the parent claim.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `ClaimDocumentTypeEnum`

Business purpose of the document.

- `bank_statement` - bank_statement
- `claim_statement` - claim_statement
- `correspondence` - correspondence
- `invoice` - invoice
- `other` - other
- `payment_proof` - payment_proof
- `reminder` - reminder

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.documents.<a href="src/paywise/case_management/documents/client.py">get_claim_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.documents.get_claim_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — ID of the parent claim.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.documents.<a href="src/paywise/case_management/documents/client.py">delete_claim_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.documents.delete_claim_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — ID of the parent claim.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.documents.<a href="src/paywise/case_management/documents/client.py">download_claim_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.documents.download_claim_document(
    claim_id="claim_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim_id:** `str` — ID of the parent claim.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Debtors

<details><summary><code>client.case_management.debtors.<a href="src/paywise/case_management/debtors/client.py">list_debtors</a>(...) -> PaginatedDebtorListList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The reusable debtors of your company.

List, retrieve, create, and PATCH. A supplied owned collection
(addresses, bank accounts, communication channels, legal
representatives) replaces that collection completely; omitted
collections stay unchanged. A case's debtor is the case's own snapshot
(published as `MandateDebtor` without an id) and is not a reusable
debtor: it is neither listed nor readable here.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.debtors.list_debtors()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**acting_as:** `typing.Optional[ListDebtorsRequestActingAs]` — Exact capacity in which the debtor incurred the obligation: `consumer` or `business`.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**id:** `typing.Optional[str]` — Return the debtor with this UUID.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Case-insensitive substring of your debtor reference.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.debtors.<a href="src/paywise/case_management/debtors/client.py">create_debtor</a>(...) -> DebtorDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The reusable debtors of your company.

List, retrieve, create, and PATCH. A supplied owned collection
(addresses, bank accounts, communication channels, legal
representatives) replaces that collection completely; omitted
collections stay unchanged. A case's debtor is the case's own snapshot
(published as `MandateDebtor` without an id) and is not a reusable
debtor: it is neither listed nor readable here.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import DebtorWriteRequest_Consumer, DebtorPersonWriteRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.debtors.create_debtor(
    idempotency_key="Idempotency-Key",
    request=DebtorWriteRequest_Consumer(
        person=DebtorPersonWriteRequest(
            first_name="first_name",
            last_name="last_name",
        ),
    ),
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `DebtorWriteRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.debtors.<a href="src/paywise/case_management/debtors/client.py">get_debtor</a>(...) -> DebtorDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The reusable debtors of your company.

List, retrieve, create, and PATCH. A supplied owned collection
(addresses, bank accounts, communication channels, legal
representatives) replaces that collection completely; omitted
collections stay unchanged. A case's debtor is the case's own snapshot
(published as `MandateDebtor` without an id) and is not a reusable
debtor: it is neither listed nor readable here.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.debtors.get_debtor(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the debtor in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.debtors.<a href="src/paywise/case_management/debtors/client.py">update_debtor</a>(...) -> DebtorDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The reusable debtors of your company.

List, retrieve, create, and PATCH. A supplied owned collection
(addresses, bank accounts, communication channels, legal
representatives) replaces that collection completely; omitted
collections stay unchanged. A case's debtor is the case's own snapshot
(published as `MandateDebtor` without an id) and is not a reusable
debtor: it is neither listed nor readable here.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import CommunicationChannelWriteRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.debtors.update_debtor(
    id="id",
    communication_channels=[
        CommunicationChannelWriteRequest(
            type="email",
            value="billing@example.test",
        ),
        CommunicationChannelWriteRequest(
            type="mobile_phone",
            value="+4915123456789",
        )
    ],
    your_reference="CUSTOMER-1001-UPDATED",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the debtor in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**acting_as:** `typing.Optional[ActingAsEnum]` — Whether the debtor incurred the obligation as a consumer or in a business capacity. When changing it, update person, organization, and legal_form together to form a valid identity.

</dd>
</dl>

<dl>
<dd>

**addresses:** `typing.Optional[typing.List[AddressWriteRequest]]` — Postal addresses for the debtor. Supplied arrays replace the entire collection; [] clears it and omission leaves it unchanged. Include an existing child id to retain that entry. A non-empty list must have exactly one primary address; an order requires at least one complete address before finalization. Maximum 5 entries.

</dd>
</dl>

<dl>
<dd>

**bank_accounts:** `typing.Optional[typing.List[BankAccountWriteRequest]]` — Known bank accounts for the debtor. Supplied arrays replace the entire collection; [] clears it and omission leaves it unchanged. Include an existing child id to retain that entry. Duplicate IBANs are rejected. Maximum 10 entries.

</dd>
</dl>

<dl>
<dd>

**communication_channels:** `typing.Optional[typing.List[CommunicationChannelWriteRequest]]` — Email addresses and telephone numbers for the debtor. Supplied arrays replace the entire collection; [] clears it and omission leaves it unchanged. Include an existing child id to retain that entry. Duplicate type/value pairs are rejected. Maximum 10 entries.

</dd>
</dl>

<dl>
<dd>

**legal_form:** `typing.Optional[str]` — Optional permanent code from GET /v2/legal-forms/. Null or an empty string clears it; consumers cannot supply a code. A supplied catalog group determines the permitted identity. Omission preserves the current value.

</dd>
</dl>

<dl>
<dd>

**legal_representatives:** `typing.Optional[typing.List[LegalRepresentativeWriteRequest]]` — Legal representatives for the debtor. Supplied arrays replace the entire collection; [] clears it and omission leaves it unchanged. Include an existing child id to retain that entry. Representative nesting is limited to two levels. Maximum 10 entries.

</dd>
</dl>

<dl>
<dd>

**organization:** `typing.Optional[OrganizationPatchRequest]` — Organization identity for business legal forms outside the privatperson and einzelkaufmann groups. Supplied properties update the current organization; omission leaves it unchanged and null removes it. The resulting debtor must retain a valid identity.

</dd>
</dl>

<dl>
<dd>

**person:** `typing.Optional[PersonPatchRequest]` — Natural-person identity for consumers and business legal forms in the privatperson or einzelkaufmann group. Supplied properties update the current person; omission leaves it unchanged and null removes it. The resulting debtor must retain a valid identity.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Your reference for this debtor. Blank is stored as null.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Events

<details><summary><code>client.case_management.events.<a href="src/paywise/case_management/events/client.py">list_events</a>(...) -> PaginatedEventFeed</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return one page of the company's event feed, oldest first.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.events.list_events()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**event_type:** `typing.Optional[typing.Union[ListEventsRequestEventTypeItem, typing.Sequence[ListEventsRequestEventTypeItem]]]` — Return only events of these exact types. Repeat the parameter for several types.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**since:** `typing.Optional[str]` — Opaque cursor taken from the `cursor` (or `next`) field of a previous page. Omit it to start at the oldest retained event (30 days). Entries become visible about 60 seconds after they are recorded, so a cursor never runs ahead of an event that is still being written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Health

<details><summary><code>client.case_management.health.<a href="src/paywise/case_management/health/client.py">check</a>() -> CaseHealthResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return the unauthenticated Case Management API liveness response.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.health.check()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Info

<details><summary><code>client.case_management.info.<a href="src/paywise/case_management/info/client.py">get_case_credential_context</a>() -> CaseTokenInfoResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return non-PII metadata about the calling credential and selected company. Partner credentials must select the company through X-On-Behalf-Of-Company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.info.get_case_credential_context()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Legal forms

<details><summary><code>client.case_management.legal_forms.<a href="src/paywise/case_management/legal_forms/client.py">list_legal_forms</a>(...) -> typing.List[LegalFormCatalog]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return the authenticated, tenant-independent public catalog.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.legal_forms.list_legal_forms()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Mandates

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandates</a>(...) -> PaginatedMandateListList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Accepted cases (Aktenzeichen).

Main-case-centric: the list returns **main cases only**.
Sub-cases are reachable through the main case detail representation and
direct detail/subresource URLs, not a flat list expansion. Tenant-scoped by
the authenticated company.

Sub-resources of one mandate:

- payments — the reported, non-ignored payments
- documents — claim-document metadata and a proxy-stream download
- history — published client activity, related resources, and attachments.
  A main case includes its subcases; a subcase includes only itself.

The sub-resource operations resolve the mandate **including sub-cases** —
unlike the list, which hides sub-cases — so an individually-addressable
sub-case's own track stays reachable. These public mandate operations are
reads.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandates()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**archived:** `typing.Optional[bool]` — Whether the accepted case is archived. When omitted, archived cases are hidden unless `updated_since` is set; with `updated_since` archived and active cases are both returned.

</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[datetime.datetime]` — Created at or after this timestamp (inclusive).

</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[datetime.datetime]` — Created at or before this timestamp (inclusive).

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**legal_stage:** `typing.Optional[str]` — Exact legal stage of the accepted case.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**ordering:** `typing.Optional[str]` — Comma-separated sort fields: debtor `name`, `created`, total claim `amount`, or the latest published status title (`status`). Prefix a field with `-` for descending order. Defaults to `-created`; `updated_since` uses its synchronization order instead.

</dd>
</dl>

<dl>
<dd>

**payment_state:** `typing.Optional[typing.Union[ListMandatesRequestPaymentStateItem, typing.Sequence[ListMandatesRequestPaymentStateItem]]]` — Payment state: `unpaid`, `partially_paid`, or `fully_paid`. Repeat the parameter to include any of several states.

</dd>
</dl>

<dl>
<dd>

**processing_state:** `typing.Optional[typing.Union[ListMandatesRequestProcessingStateItem, typing.Sequence[ListMandatesRequestProcessingStateItem]]]` — Exact processing state. Repeat the parameter to include any of several states.

</dd>
</dl>

<dl>
<dd>

**q:** `typing.Optional[str]` — A UUID matches the case, one of its subcases, or one of its claims. Otherwise searches case-insensitively by substring: debtor names (accents ignored), your debtor reference, current and previous case references, claim and document references, and, from three characters, the titles, texts and event codes of published status updates. Subcase matches return their main case. Debtor name and reference matches include production-mode debtors only, as in the portal.

</dd>
</dl>

<dl>
<dd>

**reference_number:** `typing.Optional[str]` — Case-insensitive substring of the current paywise case reference, or an exact match on a previous paywise reference.

</dd>
</dl>

<dl>
<dd>

**requests:** `typing.Optional[typing.Union[ListMandatesRequestRequestsItem, typing.Sequence[ListMandatesRequestRequestsItem]]]` — Filter by published open or answered client requests, or by having no published client requests. Repeat the parameter to include any of these categories.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate</a>(...) -> MandateDetail</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Accepted cases (Aktenzeichen).

Main-case-centric: the list returns **main cases only**.
Sub-cases are reachable through the main case detail representation and
direct detail/subresource URLs, not a flat list expansion. Tenant-scoped by
the authenticated company.

Sub-resources of one mandate:

- payments — the reported, non-ignored payments
- documents — claim-document metadata and a proxy-stream download
- history — published client activity, related resources, and attachments.
  A main case includes its subcases; a subcase includes only itself.

The sub-resource operations resolve the mandate **including sub-cases** —
unlike the list, which hides sub-cases — so an individually-addressable
sub-case's own track stays reachable. These public mandate operations are
reads.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**expand:** `typing.Optional[GetMandateRequestExpand]` — With history=true, embed the typed related resource body.

</dd>
</dl>

<dl>
<dd>

**history:** `typing.Optional[bool]` — Embed up to 100 unified history entries.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_documents</a>(...) -> MandateDocumentPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Accepted cases (Aktenzeichen).

Main-case-centric: the list returns **main cases only**.
Sub-cases are reachable through the main case detail representation and
direct detail/subresource URLs, not a flat list expansion. Tenant-scoped by
the authenticated company.

Sub-resources of one mandate:

- payments — the reported, non-ignored payments
- documents — claim-document metadata and a proxy-stream download
- history — published client activity, related resources, and attachments.
  A main case includes its subcases; a subcase includes only itself.

The sub-resource operations resolve the mandate **including sub-cases** —
unlike the list, which hides sub-cases — so an individually-addressable
sub-case's own track stays reachable. These public mandate operations are
reads.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_documents(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return entries changed at or after this timezone-aware RFC 3339 timestamp (inclusive). With it set, results are ordered by change time and then id instead of newest first, page by `cursor` instead of `offset`, and entries changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">download_mandate_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Accepted cases (Aktenzeichen).

Main-case-centric: the list returns **main cases only**.
Sub-cases are reachable through the main case detail representation and
direct detail/subresource URLs, not a flat list expansion. Tenant-scoped by
the authenticated company.

Sub-resources of one mandate:

- payments — the reported, non-ignored payments
- documents — claim-document metadata and a proxy-stream download
- history — published client activity, related resources, and attachments.
  A main case includes its subcases; a subcase includes only itself.

The sub-resource operations resolve the mandate **including sub-cases** —
unlike the list, which hides sub-cases — so an individually-addressable
sub-case's own track stays reachable. These public mandate operations are
reads.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.download_mandate_document(
    id="id",
    doc_id="doc_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**doc_id:** `str` — Document UUID.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_history</a>(...) -> MandateHistoryPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Accepted cases (Aktenzeichen).

Main-case-centric: the list returns **main cases only**.
Sub-cases are reachable through the main case detail representation and
direct detail/subresource URLs, not a flat list expansion. Tenant-scoped by
the authenticated company.

Sub-resources of one mandate:

- payments — the reported, non-ignored payments
- documents — claim-document metadata and a proxy-stream download
- history — published client activity, related resources, and attachments.
  A main case includes its subcases; a subcase includes only itself.

The sub-resource operations resolve the mandate **including sub-cases** —
unlike the list, which hides sub-cases — so an individually-addressable
sub-case's own track stays reachable. These public mandate operations are
reads.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_history(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**expand:** `typing.Optional[GetMandateHistoryRequestExpand]` — Embed the typed related resource body.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return entries changed at or after this timezone-aware RFC 3339 timestamp (inclusive). With it set, results are ordered by change time and then id instead of newest first, page by `cursor` instead of `offset`, and entries changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">download_mandate_history_attachment</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Download a file explicitly published with a history entry. The entry must belong to the selected mandate's history: main case plus its subcases for a main-case URL, or only the selected subcase.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.download_mandate_history_attachment(
    id="id",
    entry_id="entry_id",
    file_id="file_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**entry_id:** `str` — History entry UUID.

</dd>
</dl>

<dl>
<dd>

**file_id:** `str` — Status attachment UUID.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandate_messages</a>(...) -> PaginatedMessageReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandate_messages(
    mandate_id="mandate_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">create_mandate_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import InlineDocumentCreateRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.create_mandate_message(
    mandate_id="mandate_id",
    idempotency_key="Idempotency-Key",
    body="The customer provided an updated invoice address.",
    documents=[
        InlineDocumentCreateRequest(
            base64="base64",
            type="bank_statement",
        )
    ],
    title="Updated invoice address",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `MessageCreateRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_message(
    mandate_id="mandate_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the message in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">update_mandate_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.update_mandate_message(
    mandate_id="mandate_id",
    id="id",
    body="Correction: the new invoice address applies from 1 August 2026.",
    title="Updated invoice address (corrected)",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the message in this request.

</dd>
</dl>

<dl>
<dd>

**request:** `PatchedMessagePatchRequest`

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandate_message_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandate_message_documents(
    mandate_id="mandate_id",
    message_id="message_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">create_mandate_message_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.create_mandate_message_document(
    mandate_id="mandate_id",
    message_id="message_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="bank_statement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `CaseDocumentTypeEnum`

Business purpose of the document.

- `bank_statement` - bank_statement
- `claim_statement` - claim_statement
- `correspondence` - correspondence
- `enforceable_title` - enforceable_title
- `invoice` - invoice
- `other` - other
- `payment_proof` - payment_proof
- `reminder` - reminder
- `rental_agreement` - rental_agreement

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_message_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_message_document(
    mandate_id="mandate_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">delete_mandate_message_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.delete_mandate_message_document(
    mandate_id="mandate_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">download_mandate_message_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.download_mandate_message_document(
    mandate_id="mandate_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandate_payments</a>(...) -> PaginatedPaymentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Immutable client payment reports under a main mandate or subcase.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandate_payments(
    mandate_id="mandate_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">create_mandate_payment</a>(...) -> PaymentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Immutable client payment reports under a main mandate or subcase.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import PaymentAmountWriteRequest, PaymentMetadataWriteRequest
import datetime

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.create_mandate_payment(
    mandate_id="mandate_id",
    idempotency_key="Idempotency-Key",
    amount=PaymentAmountWriteRequest(
        currency="EUR",
        value="50.00",
    ),
    metadata=[
        PaymentMetadataWriteRequest(
            type="transaction:reference",
            value="BANK-TRANSACTION-99812",
        )
    ],
    value_date=datetime.date.fromisoformat("2026-07-17"),
    your_reference="BANK-TRANSACTION-99812",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `PaymentWriteRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandate_requests_to_client</a>(...) -> PaginatedRequestToClientReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions paywise asks the client about one case.

list/retrieve, plus `answer` to respond exactly once per request.
Tenant-scoped by the authenticated company; only published requests are
visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandate_requests_to_client(
    mandate_id="mandate_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**answered:** `typing.Optional[bool]` — Whether the client has answered the request. Omit to include both answered and unanswered requests.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_request_to_client</a>(...) -> RequestToClientRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions paywise asks the client about one case.

list/retrieve, plus `answer` to respond exactly once per request.
Tenant-scoped by the authenticated company; only published requests are
visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_request_to_client(
    mandate_id="mandate_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">answer_mandate_request_to_client</a>(...) -> RequestToClientRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions paywise asks the client about one case.

list/retrieve, plus `answer` to respond exactly once per request.
Tenant-scoped by the authenticated company; only published requests are
visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import InlineDocumentCreateRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.answer_mandate_request_to_client(
    mandate_id="mandate_id",
    id="id",
    idempotency_key="Idempotency-Key",
    additional_comment="Please continue processing.",
    documents=[
        InlineDocumentCreateRequest(
            base64="base64",
            type="bank_statement",
        )
    ],
    text="The outstanding amount is correct.",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `AnswerWriteRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">download_mandate_request_to_client_attachment</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Proxy-stream one of the question's case-worker attachments.

Attachments are resolved through the tenant-scoped request itself,
so a caller can only reach attachments on a request its company owns.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.download_mandate_request_to_client_attachment(
    mandate_id="mandate_id",
    id="id",
    attachment_id="attachment_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**attachment_id:** `str` — ID of the question attachment to download.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">list_mandate_request_to_client_answer_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents added to one v2 answer before its review task starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.list_mandate_request_to_client_answer_documents(
    mandate_id="mandate_id",
    request_id="request_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">create_mandate_request_to_client_answer_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents added to one v2 answer before its review task starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.create_mandate_request_to_client_answer_document(
    mandate_id="mandate_id",
    request_id="request_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="bank_statement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `CaseDocumentTypeEnum`

Business purpose of the document.

- `bank_statement` - bank_statement
- `claim_statement` - claim_statement
- `correspondence` - correspondence
- `enforceable_title` - enforceable_title
- `invoice` - invoice
- `other` - other
- `payment_proof` - payment_proof
- `reminder` - reminder
- `rental_agreement` - rental_agreement

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">get_mandate_request_to_client_answer_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents added to one v2 answer before its review task starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.get_mandate_request_to_client_answer_document(
    mandate_id="mandate_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">delete_mandate_request_to_client_answer_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents added to one v2 answer before its review task starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.delete_mandate_request_to_client_answer_document(
    mandate_id="mandate_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.mandates.<a href="src/paywise/case_management/mandates/client.py">download_mandate_request_to_client_answer_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents added to one v2 answer before its review task starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.mandates.download_mandate_request_to_client_answer_document(
    mandate_id="mandate_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mandate_id:** `str` — UUID of the parent accepted case in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Orders

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_orders</a>(...) -> PaginatedOrderList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The collection orders of your company.

Create a draft with a referenced debtor and embedded claims,
edit it while it is a draft, finalize it for review, and follow it to
acceptance. Tenant-scoped by the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_orders()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**created_after:** `typing.Optional[datetime.datetime]` — Created at or after this timestamp (inclusive).

</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[datetime.datetime]` — Created at or before this timestamp (inclusive).

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**ordering:** `typing.Optional[str]` — Comma-separated sort fields: debtor `name`, `created`, total claim `amount`, or public order `status`. Prefix a field with `-` for descending order. Defaults to `-created`; `updated_since` uses its synchronization order instead.

</dd>
</dl>

<dl>
<dd>

**q:** `typing.Optional[str]` — A UUID matches the order or its debtor. Otherwise searches debtor names, claim references, document references, and claim subject matter by case-insensitive substring.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListOrdersRequestStatus]` — Exact public order status, including drafts whose expiry time has passed.

</dd>
</dl>

<dl>
<dd>

**type:** `typing.Optional[ListOrdersRequestType]` — Exact order variant: `invoice`, `rental`, or `titled`.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">create_order</a>(...) -> Order</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The collection orders of your company.

Create a draft with a referenced debtor and embedded claims,
edit it while it is a draft, finalize it for review, and follow it to
acceptance. Tenant-scoped by the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import ClaimCreateRequest_Receivable, ClaimPrincipalAmountWriteRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.create_order(
    idempotency_key="Idempotency-Key",
    additional_debtor_ids=[
        "additional_debtor_ids"
    ],
    claims=[
        ClaimCreateRequest_Receivable(
            is_disputed=True,
            principal_amount=ClaimPrincipalAmountWriteRequest(
                value="value",
            ),
        )
    ],
    creditor_obligation_fulfilled=True,
    debtor_id="40000000-0000-4000-8000-000000000001",
    starting_approach="extrajudicial",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**debtor_id:** `str` — Existing primary debtor in the selected company.

</dd>
</dl>

<dl>
<dd>

**additional_debtor_ids:** `typing.Optional[typing.List[str]]` — Other debtors, each supplied by an existing UUID from the active company. The primary debtor cannot also appear here, and each referenced additional debtor may appear only once. Maximum 10 entries.

</dd>
</dl>

<dl>
<dd>

**claims:** `typing.Optional[typing.List[ClaimCreateRequest]]` — Claims to create in this draft; each must specify type. Invoice and rental orders accept receivable claims. Titled orders accept titled claims and receivable enforcement costs (K014); at least one complete claim, including one titled claim for titled orders, is required before finalization. Maximum 50 entries. The 50-claim limit applies to the complete order, including claims added later through the claim endpoint; exceeding it returns 400 validation_error.

</dd>
</dl>

<dl>
<dd>

**confirmation_email:** `typing.Optional[str]` — Address that receives the order entry confirmation (Eingangsbestätigung) when the order is finalized. Omit or set null for no confirmation email.

</dd>
</dl>

<dl>
<dd>

**creditor_obligation_fulfilled:** `typing.Optional[bool]` — Whether you have fully performed your obligation to the debtor. For invoice and rental orders, supply true or false before finalization; null leaves the decision unset. Omit for titled orders.

</dd>
</dl>

<dl>
<dd>

**rental_agreement:** `typing.Optional[RentalAgreementInlineRequest]` — Rental-agreement singleton supplied only for a rental order.

</dd>
</dl>

<dl>
<dd>

**starting_approach:** `typing.Optional[StartingApproachEnum]` — Initial route for invoice and rental orders: extrajudicial starts with out-of-court collection; judicial starts by applying for a payment order (Mahnbescheid). Required before finalization; omit for titled orders, where enforcement is implicit.

</dd>
</dl>

<dl>
<dd>

**success_fee_confirmed:** `typing.Optional[bool]` — Only valid for titled orders. Confirmation of the titled-order success-fee arrangement; it must be true before finalization. See the [paywise General Terms and Conditions (AGB)](https://paywise.de/agb/) for the exact conditions for titled orders.

</dd>
</dl>

<dl>
<dd>

**type:** `typing.Optional[OrderTypeEnum]` — Order type discriminator: invoice, rental, or titled. Defaults to invoice when omitted.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_order</a>(...) -> Order</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The collection orders of your company.

Create a draft with a referenced debtor and embedded claims,
edit it while it is a draft, finalize it for review, and follow it to
acceptance. Tenant-scoped by the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_order(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the order in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">delete_draft_order</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The collection orders of your company.

Create a draft with a referenced debtor and embedded claims,
edit it while it is a draft, finalize it for review, and follow it to
acceptance. Tenant-scoped by the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.delete_draft_order(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the order in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">update_order</a>(...) -> Order</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update the order's mutable fields while it is a draft.

A supplied `additional_debtor_ids` array replaces its membership; omit it
to preserve the links or send `[]` to unlink all additional debtors
without deleting their records. Read full debtor details through
`GET /v2/debtors/{id}/`.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.update_order(
    id="id",
    confirmation_email="billing@example.test",
    starting_approach="extrajudicial",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the order in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**additional_debtor_ids:** `typing.Optional[typing.List[str]]` — Replace the order's additional-debtor membership with up to 10 existing debtor UUIDs from the active company. Omit to leave membership unchanged; [] unlinks all additional debtors without deleting their records. The primary debtor cannot also appear here, and duplicates are rejected. Available only while the order is a draft.

</dd>
</dl>

<dl>
<dd>

**confirmation_email:** `typing.Optional[str]` — Address that receives the order entry confirmation (Eingangsbestätigung) when the order is finalized. Set null to turn the confirmation email off again.

</dd>
</dl>

<dl>
<dd>

**creditor_obligation_fulfilled:** `typing.Optional[bool]` — Whether you have fully performed your obligation to the debtor. For invoice and rental orders, supply true or false before finalization; null leaves the decision unset. Omit for titled orders.

</dd>
</dl>

<dl>
<dd>

**debtor_id:** `typing.Optional[str]` — Replace the primary debtor with an existing debtor in the selected company.

</dd>
</dl>

<dl>
<dd>

**starting_approach:** `typing.Optional[StartingApproachEnum]` — Initial route for invoice and rental orders: extrajudicial starts with out-of-court collection; judicial starts by applying for a payment order (Mahnbescheid). Required before finalization; omit for titled orders, where enforcement is implicit.

</dd>
</dl>

<dl>
<dd>

**success_fee_confirmed:** `typing.Optional[bool]` — Only valid for titled orders. Confirmation of the titled-order success-fee arrangement; it must be true before finalization. See the [paywise General Terms and Conditions (AGB)](https://paywise.de/agb/) for the exact conditions for titled orders.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">finalize_order</a>(...) -> Order</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Finalize the order: validates the complete aggregate, makes it
immutable, and submits it for review. Declares no request body.
Acceptance happens later during review and is announced via
`order.accepted`.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.finalize_order(
    id="id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the order in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">withdraw_order</a>(...) -> Order</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Withdraw one submitted order before staff acceptance starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.withdraw_order(
    id="id",
    idempotency_key="Idempotency-Key",
    reason="The customer paid before review began.",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the order in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**reason:** `typing.Optional[str]` — Optional explanation for withdrawing an eligible submitted order before acceptance or active review prevents withdrawal. Maximum 5000 characters.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_order_messages</a>(...) -> PaginatedMessageReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_order_messages(
    order_id="order_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">create_order_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import InlineDocumentCreateRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.create_order_message(
    order_id="order_id",
    idempotency_key="Idempotency-Key",
    body="The customer provided an updated invoice address.",
    documents=[
        InlineDocumentCreateRequest(
            base64="base64",
            type="bank_statement",
        )
    ],
    title="Updated invoice address",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `MessageCreateRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_order_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_order_message(
    order_id="order_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the message in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">update_order_message</a>(...) -> MessageRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Messages exchanged with paywise about one order or one case.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.update_order_message(
    order_id="order_id",
    id="id",
    body="Correction: the new invoice address applies from 1 August 2026.",
    title="Updated invoice address (corrected)",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the message in this request.

</dd>
</dl>

<dl>
<dd>

**request:** `PatchedMessagePatchRequest`

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_order_message_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_order_message_documents(
    order_id="order_id",
    message_id="message_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">create_order_message_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.create_order_message_document(
    order_id="order_id",
    message_id="message_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="bank_statement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `CaseDocumentTypeEnum`

Business purpose of the document.

- `bank_statement` - bank_statement
- `claim_statement` - claim_statement
- `correspondence` - correspondence
- `enforceable_title` - enforceable_title
- `invoice` - invoice
- `other` - other
- `payment_proof` - payment_proof
- `reminder` - reminder
- `rental_agreement` - rental_agreement

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_order_message_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_order_message_document(
    order_id="order_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">delete_order_message_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.delete_order_message_document(
    order_id="order_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">download_order_message_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents below one parent resource: upload, list, download, delete.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.download_order_message_document(
    order_id="order_id",
    message_id="message_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**message_id:** `str` — UUID of the parent message in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_rental_agreement</a>(...) -> RentalAgreementRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tenant-scoped resource collection of the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_rental_agreement(
    order_id="order_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">update_rental_agreement</a>(...) -> RentalAgreementRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tenant-scoped resource collection of the authenticated company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import RentalDueRuleRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.update_rental_agreement(
    order_id="order_id",
    due_rule=RentalDueRuleRequest(
        day=5,
        kind="business_day",
    ),
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**contract_date:** `typing.Optional[datetime.date]` — Date on which the rental contract was concluded; this is not the tenancy start or move-in date. Required before finalization. Updating it also updates the legal_basis.contract_date of H17/H19 claims in the order.

</dd>
</dl>

<dl>
<dd>

**due_rule:** `typing.Optional[RentalDueRuleRequest]` — Rule used to derive H17/H19 rental due dates. Omission preserves the current rule; null restores the default third German business day. Changes recalculate dates except claim-level dates explicitly overridden by the client.

</dd>
</dl>

<dl>
<dd>

**monthly_rent:** `typing.Optional[MonthlyRentWriteRequest]` — Total recurring Warmmiete, including ancillary-cost prepayments; it does not constrain an individual claim amount. May be absent or null while drafting; must be positive before finalization.

</dd>
</dl>

<dl>
<dd>

**property_address:** `typing.Optional[RentalPropertyAddressWriteRequest]` — Complete address of the rented property, even when it matches the debtor address. Supply street, postal_code, city, and country; this creates a separate property address and does not reuse a debtor address id or primary flag. A complete property address is required before finalization.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_rental_agreement_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a rental order's agreement singleton.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_rental_agreement_documents(
    order_id="order_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">create_rental_agreement_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a rental order's agreement singleton.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.create_rental_agreement_document(
    order_id="order_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="rental_agreement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `RentalAgreementDocumentTypeEnum` — Agreement document purpose: rental_agreement and claim_statement each occupy a single optional document slot; other supplies supporting documents and may be used multiple times.

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_rental_agreement_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a rental order's agreement singleton.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_rental_agreement_document(
    order_id="order_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">delete_rental_agreement_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a rental order's agreement singleton.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.delete_rental_agreement_document(
    order_id="order_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">download_rental_agreement_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents owned by a rental order's agreement singleton.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.download_rental_agreement_document(
    order_id="order_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_order_requests_to_client</a>(...) -> PaginatedOrderRequestToClientReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions about one order, including orders awaiting review.

Answer once using the advertised answer type. Closed orders reject answers
with 409. Review resumes after all published requests are answered.
Documents become downloadable when ready. Only the authenticated company's published requests
are visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_order_requests_to_client(
    order_id="order_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**answered:** `typing.Optional[bool]` — Whether the client has answered the request. Omit to include both answered and unanswered requests.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_order_request_to_client</a>(...) -> OrderRequestToClientRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions about one order, including orders awaiting review.

Answer once using the advertised answer type. Closed orders reject answers
with 409. Review resumes after all published requests are answered.
Documents become downloadable when ready. Only the authenticated company's published requests
are visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_order_request_to_client(
    order_id="order_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">answer_order_request_to_client</a>(...) -> OrderRequestToClientRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published questions about one order, including orders awaiting review.

Answer once using the advertised answer type. Closed orders reject answers
with 409. Review resumes after all published requests are answered.
Documents become downloadable when ready. Only the authenticated company's published requests
are visible.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.case_management import InlineDocumentCreateRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.answer_order_request_to_client(
    order_id="order_id",
    id="id",
    idempotency_key="Idempotency-Key",
    additional_comment="The invoice is correct.",
    documents=[
        InlineDocumentCreateRequest(
            base64="base64",
            type="bank_statement",
        )
    ],
    text="yes",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `AnswerWriteRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">download_order_request_to_client_attachment</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Proxy-stream one of the question's case-worker attachments.

Attachments are resolved through the tenant-scoped request itself,
so a caller can only reach attachments on a request its company owns.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.download_order_request_to_client_attachment(
    order_id="order_id",
    id="id",
    attachment_id="attachment_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the client request in this request.

</dd>
</dl>

<dl>
<dd>

**attachment_id:** `str` — ID of the question attachment to download.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">list_order_request_to_client_answer_documents</a>(...) -> PaginatedDocumentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents on an order request answer, editable until staff review starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.list_order_request_to_client_answer_documents(
    order_id="order_id",
    request_id="request_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">create_order_request_to_client_answer_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents on an order request answer, editable until staff review starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.create_order_request_to_client_answer_document(
    order_id="order_id",
    request_id="request_id",
    idempotency_key="Idempotency-Key",
    file="example_file",
    type="bank_statement",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**type:** `CaseDocumentTypeEnum`

Business purpose of the document.

- `bank_statement` - bank_statement
- `claim_statement` - claim_statement
- `correspondence` - correspondence
- `enforceable_title` - enforceable_title
- `invoice` - invoice
- `other` - other
- `payment_proof` - payment_proof
- `reminder` - reminder
- `rental_agreement` - rental_agreement

</dd>
</dl>

<dl>
<dd>

**base64:** `typing.Optional[str]` — Base64-encoded PDF, JPEG, or PNG content. Supply exactly one of base64 or multipart file. Maximum decoded file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[core.File]` — PDF, JPEG, or PNG file supplied as multipart form data. Supply exactly one of file or base64. Maximum file size: 10 MiB (10,485,760 bytes); maximum PDF length: 100 pages. Oversized content returns 400; too many PDF pages uses page_limit_exceeded.

</dd>
</dl>

<dl>
<dd>

**filename:** `typing.Optional[str]` — Original filename shown to users. Path components and control characters are removed and the extension always follows the detected content type.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">get_order_request_to_client_answer_document</a>(...) -> DocumentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents on an order request answer, editable until staff review starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.get_order_request_to_client_answer_document(
    order_id="order_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">delete_order_request_to_client_answer_document</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents on an order request answer, editable until staff review starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.delete_order_request_to_client_answer_document(
    order_id="order_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.orders.<a href="src/paywise/case_management/orders/client.py">download_order_request_to_client_answer_document</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Documents on an order request answer, editable until staff review starts.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.orders.download_order_request_to_client_answer_document(
    order_id="order_id",
    request_id="request_id",
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**order_id:** `str` — UUID of the parent order in this request.

</dd>
</dl>

<dl>
<dd>

**request_id:** `str` — UUID of the parent client request in this request.

</dd>
</dl>

<dl>
<dd>

**id:** `str` — UUID of the document in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Payments

<details><summary><code>client.case_management.payments.<a href="src/paywise/case_management/payments/client.py">list_payments</a>(...) -> PaginatedPaymentReadList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only top-level payment collection.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.payments.list_payments()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**claim:** `typing.Optional[str]` — Return payments assigned to this claim UUID.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**mandate:** `typing.Optional[str]` — Return payments assigned to this accepted case UUID.

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**value_date_after:** `typing.Optional[datetime.date]` — Payment value date on or after this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**value_date_before:** `typing.Optional[datetime.date]` — Payment value date on or before this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Case-insensitive substring of your payment reference.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.payments.<a href="src/paywise/case_management/payments/client.py">get_payment</a>(...) -> PaymentRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only top-level payment collection.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.payments.get_payment(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the payment in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Single mandate statements

<details><summary><code>client.case_management.single_mandate_statements.<a href="src/paywise/case_management/single_mandate_statements/client.py">list_single_mandate_statements</a>(...) -> PaginatedSingleMandateStatementListList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published per-case settlements (Aktenabrechnungen) and their PDF.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.single_mandate_statements.list_single_mandate_statements()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**booking_date:** `typing.Optional[datetime.date]` — Booked on exactly this date.

</dd>
</dl>

<dl>
<dd>

**booking_date_from:** `typing.Optional[datetime.date]` — Booking date on or after this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**booking_date_to:** `typing.Optional[datetime.date]` — Booking date on or before this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**clearing_no:** `typing.Optional[str]` — Exact clearing number.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**invoice_no:** `typing.Optional[str]` — Exact invoice number.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**mandate:** `typing.Optional[str]` — Return statements for this accepted case UUID.

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**ordering:** `typing.Optional[str]` — Comma-separated sort fields: `booking_date`, `period_start`, `period_end`, `created`, `updated`, `clearing_no`, or `invoice_no`. Prefix a field with `-` for descending order. Defaults to `-created`; `updated_since` uses its synchronization order instead.

</dd>
</dl>

<dl>
<dd>

**reference_number:** `typing.Optional[str]` — Exact paywise case reference recorded on the statement.

</dd>
</dl>

<dl>
<dd>

**statement_type:** `typing.Optional[ListSingleMandateStatementsRequestStatementType]` — Statement kind: interim, final, expenses invoice, transition to long-term monitoring, or negative closing. Use the corresponding enum value.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListSingleMandateStatementsRequestStatus]` — Return `published` statements that have not been cancelled, or `cancelled` statements.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Exact client reference recorded on the statement.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.single_mandate_statements.<a href="src/paywise/case_management/single_mandate_statements/client.py">get_single_mandate_statement</a>(...) -> SingleMandateStatementRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published per-case settlements (Aktenabrechnungen) and their PDF.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.single_mandate_statements.get_single_mandate_statement(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the per-case statement in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.single_mandate_statements.<a href="src/paywise/case_management/single_mandate_statements/client.py">download_single_mandate_statement_pdf</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Proxy the stored PDF without disclosing its storage location.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.single_mandate_statements.download_single_mandate_statement_pdf(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the per-case statement in this request.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Statements

<details><summary><code>client.case_management.statements.<a href="src/paywise/case_management/statements/client.py">list_statements</a>(...) -> PaginatedStatementListList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published payout statements and their customer-visible breakdown.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.statements.list_statements()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**booking_date_from:** `typing.Optional[datetime.date]` — Booking date on or after this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**booking_date_to:** `typing.Optional[datetime.date]` — Booking date on or before this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**clearing_no:** `typing.Optional[str]` — Exact clearing number.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**invoice_no:** `typing.Optional[str]` — Exact invoice number.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**mandate_reference_number:** `typing.Optional[str]` — Statements that include the accepted case with this paywise reference number, exact match.

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**ordering:** `typing.Optional[str]` — Comma-separated sort fields: `booking_date`, `period_start`, `period_end`, `created`, `updated`, `clearing_no`, or `invoice_no`. Prefix a field with `-` for descending order. Defaults to `-created`; `updated_since` uses its synchronization order instead.

</dd>
</dl>

<dl>
<dd>

**period_end_from:** `typing.Optional[datetime.date]` — Statement period ends on or after this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**period_end_to:** `typing.Optional[datetime.date]` — Statement period ends on or before this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**period_start_from:** `typing.Optional[datetime.date]` — Statement period starts on or after this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**period_start_to:** `typing.Optional[datetime.date]` — Statement period starts on or before this date (inclusive).

</dd>
</dl>

<dl>
<dd>

**q:** `typing.Optional[str]` — A UUID matches the statement. Otherwise searches clearing number, invoice number, and company name by case-insensitive substring. Related case, claim, and document references use exact, case-insensitive matches.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListStatementsRequestStatus]` — Return `published` statements that have not been cancelled, or `cancelled` statements.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.statements.<a href="src/paywise/case_management/statements/client.py">get_statement</a>(...) -> StatementRead</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Published payout statements and their customer-visible breakdown.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.statements.get_statement(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the statement in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.statements.<a href="src/paywise/case_management/statements/client.py">download_statement</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Proxy one stored statement file without disclosing its storage location.

The type parameter selects the PDF (default) or one of the three
Excel exports; a type whose file has not been transferred is 404.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.statements.download_statement(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the statement in this request.

</dd>
</dl>

<dl>
<dd>

**type:** `typing.Optional[DownloadStatementRequestType]` — Which file to download: full-pdf (the statement document, the default), third-party-money-xlsx (Fremdgeldabrechnung), cost-burden-xlsx (Kostenbelastung) or closing-xlsx (Abschlussmeldungen). Each type is listed in the statement's files array once it is available.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.statements.<a href="src/paywise/case_management/statements/client.py">list_statement_cases</a>(...) -> StatementMandateRowPage</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Page through the accepted cases included in one statement.

Same rows as the mandates array of the statement detail, with
limit/offset pagination and filters on the case and claim references.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.statements.list_statement_cases(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the statement in this request.

</dd>
</dl>

<dl>
<dd>

**document_reference:** `typing.Optional[str]` — Case-insensitive substring of any claim document reference in the case, usually your invoice number.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset.

</dd>
</dl>

<dl>
<dd>

**reference_number:** `typing.Optional[str]` — Case-insensitive substring of the paywise case reference.

</dd>
</dl>

<dl>
<dd>

**your_reference:** `typing.Optional[str]` — Case-insensitive substring of any claim reference in the case, such as your order or contract reference.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Usage

<details><summary><code>client.case_management.usage.<a href="src/paywise/case_management/usage/client.py">get_rate_limit_headroom</a>() -> UsageResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return an authoritative point-in-time snapshot of every rate-limit bucket applicable to the authenticated Case credential. The call itself counts against each applicable principal bucket: the token, the Partner for delegated traffic, and the active company.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.usage.get_rate_limit_headroom()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Webhook deliveries

<details><summary><code>client.case_management.webhook_deliveries.<a href="src/paywise/case_management/webhook_deliveries/client.py">list_webhook_deliveries</a>(...) -> PaginatedWebhookDeliveryList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only webhook delivery log, plus manual redelivery.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhook_deliveries.list_webhook_deliveries()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**event_type:** `typing.Optional[ListWebhookDeliveriesRequestEventType]` — Exact Case event type.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListWebhookDeliveriesRequestStatus]` — Exact delivery state: `pending`, `delivering`, `retrying`, `success`, or `failed`.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**webhook:** `typing.Optional[str]` — Return only deliveries for this webhook subscription's UUID.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhook_deliveries.<a href="src/paywise/case_management/webhook_deliveries/client.py">get_webhook_delivery</a>(...) -> WebhookDelivery</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only webhook delivery log, plus manual redelivery.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhook_deliveries.get_webhook_delivery(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook delivery in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhook_deliveries.<a href="src/paywise/case_management/webhook_deliveries/client.py">redeliver_webhook_delivery</a>(...) -> CaseWebhookCommandResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Read-only webhook delivery log, plus manual redelivery.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhook_deliveries.redeliver_webhook_delivery(
    id="id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook delivery in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Webhooks

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">list_webhooks</a>(...) -> PaginatedWebhookList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.list_webhooks()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether the webhook subscription is enabled. Omit to include both enabled and disabled subscriptions.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">create_webhook</a>(...) -> CaseWebhookWithSecret</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.create_webhook(
    idempotency_key="Idempotency-Key",
    description="Primary integration webhook",
    enabled=True,
    events=[
        "mandate.created",
        "payment.reported"
    ],
    url="https://hooks.example.test/paywise",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**url:** `str` — Publicly reachable HTTPS URL for webhook notifications. Must be unique among this company’s v2 endpoints; duplicate checks normalize the scheme, host, and default port. A company can register at most 20 webhook endpoints. Enabled and manually disabled endpoints count toward this limit; automatically disabled endpoints do not, and re-enabling one requires a free slot. Exceeding the limit returns 409 webhook_limit_reached; delete an unused endpoint to free capacity.

</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — Optional single-line label for this webhook.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether deliveries are attempted. Re-enabling an endpoint resets its consecutive failure counter. Auto-disabled endpoints do not count toward the endpoint limit, so re-enabling one requires a free slot; otherwise the request returns 409 webhook_limit_reached.

</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[CaseWebhookSubscriptionEventEnum]]` — Public event types to subscribe to. Use `["*"]` for all public events; the wildcard must be the only list entry. If omitted on creation, subscribes to the current public Case event catalogue.

</dd>
</dl>

<dl>
<dd>

**max_consecutive_failures:** `typing.Optional[int]` — Automatically disables the endpoint when this many consecutive deliveries reach terminal failure. Retry attempts within one delivery do not each count. Raising it above the failure count of an automatically disabled endpoint makes that endpoint count toward the endpoint limit again and requires a free slot.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">get_webhook</a>(...) -> Webhook</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.get_webhook(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">delete_webhook</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.delete_webhook(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">update_webhook</a>(...) -> Webhook</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.update_webhook(
    id="id",
    description="Primary integration webhook (now with statements)",
    events=[
        "mandate.created",
        "payment.reported",
        "statement.published"
    ],
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — Optional single-line label for this webhook.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether deliveries are attempted. Re-enabling an endpoint resets its consecutive failure counter. Auto-disabled endpoints do not count toward the endpoint limit, so re-enabling one requires a free slot; otherwise the request returns 409 webhook_limit_reached.

</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[CaseWebhookSubscriptionEventEnum]]` — Replacement list of public event subscriptions. Use `["*"]` for all public events; the wildcard must be the only list entry. Omit to keep the endpoint’s current subscriptions.

</dd>
</dl>

<dl>
<dd>

**max_consecutive_failures:** `typing.Optional[int]` — Automatically disables the endpoint when this many consecutive deliveries reach terminal failure. Retry attempts within one delivery do not each count. Raising it above the failure count of an automatically disabled endpoint makes that endpoint count toward the endpoint limit again and requires a free slot.

</dd>
</dl>

<dl>
<dd>

**url:** `typing.Optional[str]` — Publicly reachable HTTPS URL for webhook notifications. Must be unique among this company’s v2 endpoints; duplicate checks normalize the scheme, host, and default port. A company can register at most 20 webhook endpoints. Enabled and manually disabled endpoints count toward this limit; automatically disabled endpoints do not, and re-enabling one requires a free slot. Exceeding the limit returns 409 webhook_limit_reached; delete an unused endpoint to free capacity.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">rotate_webhook_secret</a>(...) -> CaseWebhookWithSecret</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.rotate_webhook_secret(
    id="id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.case_management.webhooks.<a href="src/paywise/case_management/webhooks/client.py">test_webhook</a>(...) -> CaseWebhookCommandResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Company-scoped webhook endpoint management.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.case_management.webhooks.test_webhook(
    id="id",
    idempotency_key="Idempotency-Key",
    event="payment.reported",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**event:** `CaseWebhookTestEventEnum`

Event type to use for the test delivery; must be one the webhook is subscribed to.

- `order.submitted` - order.submitted
- `order.withdrawn` - order.withdrawn
- `order.rejected` - order.rejected
- `order.accepted` - order.accepted
- `order.expired` - order.expired
- `mandate.created` - mandate.created
- `mandate.state.changed` - mandate.state.changed
- `mandate.status_update.published` - mandate.status_update.published
- `mandate.balance_updated` - mandate.balance_updated
- `order.message.created` - order.message.created
- `mandate.message.created` - mandate.message.created
- `request_to_client.created` - request_to_client.created
- `request_to_client.answered` - request_to_client.answered
- `payment.reported` - payment.reported
- `statement.published` - statement.published
- `statement.cancelled` - statement.cancelled
- `single_mandate_statement.published` - single_mandate_statement.published
- `single_mandate_statement.cancelled` - single_mandate_statement.cancelled
- `invoice.created` - invoice.created
- `invoice.paid` - invoice.paid
- `invoice.cancelled` - invoice.cancelled
- `invoice.written_off` - invoice.written_off
- `invoice.reopened` - invoice.reopened
- `dunning.level_advanced` - dunning.level_advanced
- `dunning.handed_to_collection` - dunning.handed_to_collection

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Companies

<details><summary><code>client.partner.companies.<a href="src/paywise/partner/companies/client.py">list_managed_companies</a>(...) -> PaginatedCompanyListList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the companies this partner manages.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.companies.list_managed_companies()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**customer_number:** `typing.Optional[str]` — Exact paywise customer number of the managed company.

</dd>
</dl>

<dl>
<dd>

**external_reference:** `typing.Optional[str]` — Exact match on the partner-supplied external_reference.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**ordering:** `typing.Optional[str]` — Order by company `name` (the default), or `-name` for descending order. `updated_since` uses its synchronization order instead.

</dd>
</dl>

<dl>
<dd>

**search:** `typing.Optional[str]` — Case-insensitive search in company names. Multiple terms must all match; quote a phrase to keep it together.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.companies.<a href="src/paywise/partner/companies/client.py">onboard_a_company</a>(...) -> CompanyCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a company managed by this partner. Requires an `Idempotency-Key` header (a retry with the same key replays the original response without setup URLs). Requires the `partner:companies:write` scope. Select required `onboarding_mode` (`api_only` or `web_flow`). Missing mode returns 400 `onboarding_mode_required`; a mode without the exact live Partner entitlement returns 403 `onboarding_mode_not_allowed`.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.partner import AddressRequest, LegalRepresentativeRequest, PartnerCompanyNotificationChannelRequest, PayoutBankAccountRequest, MembershipRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.companies.onboard_a_company(
    idempotency_key="Idempotency-Key",
    address=AddressRequest(
        city="Berlin",
        country="DE",
        postal_code="10115",
        street="Example Avenue 5",
    ),
    data_sharing_basis="self_authorized",
    default_claim_type="H11",
    external_reference="crm-4711",
    legal_form="gmbh",
    legal_representatives=[
        LegalRepresentativeRequest(
            name="Taylor Example",
            type="managing_director",
        )
    ],
    name="Example Manufacturing GmbH",
    notification_channels=[
        PartnerCompanyNotificationChannelRequest(
            notifications=[
                "requests_to_client",
                "status_updates",
                "statements"
            ],
            type="email",
            value="operations@example.test",
        )
    ],
    onboarding_mode="api_only",
    payout_bank_account=PayoutBankAccountRequest(
        account_holder="Example Manufacturing GmbH",
        iban="DE89370400440532013000",
    ),
    phone="+49301234567",
    tax_treatment="input_tax_deductible",
    users=[
        MembershipRequest(
            email="admin@example.test",
            first_name="Taylor",
            last_name="Example",
            role="admin",
            skip_email_verification=False,
        )
    ],
    vat_number="DE129273398",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**name:** `str` — Registered or trading name of the company. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**onboarding_mode:** `OnboardingModeEnum` — Required choice of api_only or web_flow for this company. paywise must enable the exact corresponding Partner entitlement; wildcard scopes grant neither. Missing mode returns 400 onboarding_mode_required; an unentitled mode returns 403 onboarding_mode_not_allowed. The selected mode cannot be changed by PATCH (409 onboarding_mode_immutable).

</dd>
</dl>

<dl>
<dd>

**address:** `typing.Optional[AddressRequest]` — Postal address of the company. Omit or set null to create the company without an address.

</dd>
</dl>

<dl>
<dd>

**data_sharing_basis:** `typing.Optional[DataSharingBasisEnum]` — Legal basis on which the partner may share this company's data. The declaration is optional here; once recorded, repeating the same value is allowed but replacing it returns 409 data_sharing_basis_already_declared.

</dd>
</dl>

<dl>
<dd>

**default_claim_type:** `typing.Optional[DefaultClaimTypeEnum]`

Default contract or transaction type for new principal claims.

- `H05` - Dienstleistungsvertrag
- `H43` - Warenlieferung/-en
- `H22` - Mitgliedsbeitrag
- `H21` - Miete
- `H11` - Kaufvertrag
- `H44` - Werkvertrag/Werklieferungsvertrag
- `H08` - Handwerkerleistung
- `H41` - Versicherungsprämie/-beitrag
- `H16` - Lehrgangs-/Unterrichtskosten
- `H10` - Hotelkosten
- `H02` - Ärztliche oder zahnärztliche Leistung
- `H28` - Schadenersatz aus Vertrag
- `H26` - Reparaturleistung
- `H24` - Rechtsanwalts-/Rechtsbeistandshonorar
- `H06` - Frachtkosten
- `H18` - Miete für Kraftfahrzeug
- `H34` - Speditionskosten
- `H19` - Miete für Wohnraum einschl. Nebenkosten
- `H42` - Versorgungsleistung - Strom, Wasser, Gas, Wärme-
- `H17` - Miete für Geschäftsraum einschl. Nebenkosten
- `H45` - Zeitungs-/Zeitschriftenbezug
- `H37` - Ungerechtfertigte Bereicherung
- `H29` - Schadenersatz aus Unfall/Vorfall
- `H01` - Anzeigen in Zeitungen u.a.
- `H78` - Tierärztliche Leistung
- `H14` - Lagerkosten
- `H77` - Krankentransportkosten
- `H40` - Vermittlungs-/Maklerprovision
- `H15` - Leasing/Mietkauf
- `H23` - Pacht
- `H04` - Darlehensrückzahlung
- `H20` - Mietnebenkosten - auch Renovierungskosten-
- `H79` - Verpflegungskosten
- `H75` - Reisevertrag
- `H33` - Schuldanerkenntnis
- `H39` - Vergleich, außergerichtlicher
- `H70` - Kindertagesstättenbeitrag
- `H90` - Wohngeld/Hausgeld für Wohnungseigentümergemeinschaft
- `H09` - Heimunterbringung
- `H03` - Bürgschaft
- `H07` - Geschäftsbesorgung durch Selbständige
- `H12` - Kontokorrentabrechnung
- `H13` - Krankenhauskosten-Pflege/Behandlung
- `H36` - Überziehung des Bankkontos
- `H61` - Wahlleistungen bei stationärer Behandlung
- `H76` - Telekommunikationsleistungen

</dd>
</dl>

<dl>
<dd>

**external_reference:** `typing.Optional[str]` — Your identifier for this company, unique within your partner organization. A duplicate returns 409 company_exists with the existing company_id. Omit or set null if you do not assign one. Filter by ?external_reference= on the company list.

</dd>
</dl>

<dl>
<dd>

**legal_form:** `typing.Optional[str]` — Permanent public code from GET /legal-forms/, or null when not set. A non-null legal_form is required when legal_representatives is nonempty. On PATCH, omission preserves the current form; it cannot be cleared while retaining representatives. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**legal_representatives:** `typing.Optional[typing.List[LegalRepresentativeRequest]]` — People or organizations legally representing the company, up to three, with roles matching legal_form. A nonempty array requires a non-null legal_form. They cannot be changed once company data submission is complete, even before the first case submission. Maximum 3 entries; exceeding this limit returns 400 validation_error.

</dd>
</dl>

<dl>
<dd>

**notification_channels:** `typing.Optional[typing.List[PartnerCompanyNotificationChannelRequest]]` — Company-level email recipients for operational notifications, up to 10. Omit or send [] if no company-level recipients are supplied yet. Each recipient has its own notification selection.

</dd>
</dl>

<dl>
<dd>

**payout_bank_account:** `typing.Optional[PayoutBankAccountRequest]` — Account to which collected funds are transferred. Omit or set null if no account is provided yet. After the first case submission, changes must use the secured payout-account change process in the paywise UI.

</dd>
</dl>

<dl>
<dd>

**phone:** `typing.Optional[str]` — Primary telephone number of the company in E.164 format; `null` clears it.

</dd>
</dl>

<dl>
<dd>

**tax_treatment:** `typing.Optional[TaxTreatmentEnum]` — Company VAT treatment, consistent with the address country. reverse_charge requires vat_number. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**users:** `typing.Optional[typing.List[MembershipRequest]]` — Users to invite to the managed company during creation, up to 10. Omit or send [] to create the company without users. A nonempty array must include at least one entry with role admin; its position in the array does not matter. Each is created as pending_setup and gains access only after accepting the setup invitation. Manage memberships through the company users endpoints after creation. Each inline membership also consumes one of the Partner-wide 60 membership additions per hour; company creation consumes one of 30 company creations per hour. All credentials share these allowances. Only successful non-replay commands count. If either allowance is exceeded, the entire command returns 429 throttled with Retry-After and creates nothing.

</dd>
</dl>

<dl>
<dd>

**vat_number:** `typing.Optional[str]` — Company VAT identification number. Required when tax_treatment is reverse_charge. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.companies.<a href="src/paywise/partner/companies/client.py">get_a_managed_company</a>(...) -> Company</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a single managed company by its uuid.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.companies.get_a_managed_company(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.companies.<a href="src/paywise/partner/companies/client.py">update_a_company_patch</a>(...) -> Company</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Partially update a managed company. A company disconnected by this partner is inaccessible and returns `404 not_found`. An empty or unchanged PATCH is a no-op that leaves `updated_at` and the ETag untouched. Sending `onboarding_mode` returns 409 `onboarding_mode_immutable`.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment
from paywise.partner import PartnerCompanyNotificationChannelRequest

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.companies.update_a_company_patch(
    id="id",
    notification_channels=[
        PartnerCompanyNotificationChannelRequest(
            notifications=[
                "requests_to_client",
                "status_updates",
                "statements"
            ],
            type="email",
            value="operations@example.test",
        )
    ],
    phone="+49307654321",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**address:** `typing.Optional[CompanyAddressPatchRequest]` — Postal address of the company. Supplied address fields update the existing address; omitted fields retain their values. When the company has no address, supply all four fields: street, postal_code, city, and country. Omit the address to preserve it or set null to remove it.

</dd>
</dl>

<dl>
<dd>

**data_sharing_basis:** `typing.Optional[DataSharingBasisEnum]` — Legal basis on which the partner may share this company's data. The declaration is optional here; once recorded, repeating the same value is allowed but replacing it returns 409 data_sharing_basis_already_declared.

</dd>
</dl>

<dl>
<dd>

**default_claim_type:** `typing.Optional[DefaultClaimTypeEnum]`

Default contract or transaction type for new principal claims.

- `H05` - Dienstleistungsvertrag
- `H43` - Warenlieferung/-en
- `H22` - Mitgliedsbeitrag
- `H21` - Miete
- `H11` - Kaufvertrag
- `H44` - Werkvertrag/Werklieferungsvertrag
- `H08` - Handwerkerleistung
- `H41` - Versicherungsprämie/-beitrag
- `H16` - Lehrgangs-/Unterrichtskosten
- `H10` - Hotelkosten
- `H02` - Ärztliche oder zahnärztliche Leistung
- `H28` - Schadenersatz aus Vertrag
- `H26` - Reparaturleistung
- `H24` - Rechtsanwalts-/Rechtsbeistandshonorar
- `H06` - Frachtkosten
- `H18` - Miete für Kraftfahrzeug
- `H34` - Speditionskosten
- `H19` - Miete für Wohnraum einschl. Nebenkosten
- `H42` - Versorgungsleistung - Strom, Wasser, Gas, Wärme-
- `H17` - Miete für Geschäftsraum einschl. Nebenkosten
- `H45` - Zeitungs-/Zeitschriftenbezug
- `H37` - Ungerechtfertigte Bereicherung
- `H29` - Schadenersatz aus Unfall/Vorfall
- `H01` - Anzeigen in Zeitungen u.a.
- `H78` - Tierärztliche Leistung
- `H14` - Lagerkosten
- `H77` - Krankentransportkosten
- `H40` - Vermittlungs-/Maklerprovision
- `H15` - Leasing/Mietkauf
- `H23` - Pacht
- `H04` - Darlehensrückzahlung
- `H20` - Mietnebenkosten - auch Renovierungskosten-
- `H79` - Verpflegungskosten
- `H75` - Reisevertrag
- `H33` - Schuldanerkenntnis
- `H39` - Vergleich, außergerichtlicher
- `H70` - Kindertagesstättenbeitrag
- `H90` - Wohngeld/Hausgeld für Wohnungseigentümergemeinschaft
- `H09` - Heimunterbringung
- `H03` - Bürgschaft
- `H07` - Geschäftsbesorgung durch Selbständige
- `H12` - Kontokorrentabrechnung
- `H13` - Krankenhauskosten-Pflege/Behandlung
- `H36` - Überziehung des Bankkontos
- `H61` - Wahlleistungen bei stationärer Behandlung
- `H76` - Telekommunikationsleistungen

</dd>
</dl>

<dl>
<dd>

**external_reference:** `typing.Optional[str]` — Your identifier for this company, unique within your partner organization. A duplicate returns 409 company_exists with the existing company_id. Set null to clear it; omit it to keep the current value.

</dd>
</dl>

<dl>
<dd>

**legal_form:** `typing.Optional[str]` — Permanent public code from GET /legal-forms/, or null when not set. A non-null legal_form is required when legal_representatives is nonempty. On PATCH, omission preserves the current form; it cannot be cleared while retaining representatives. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**legal_representatives:** `typing.Optional[typing.List[LegalRepresentativeRequest]]` — People or organizations legally representing the company, up to three, with roles matching legal_form. A nonempty array requires a non-null legal_form, using the stored form when legal_form is omitted. Omit to preserve them; a supplied array replaces them. They cannot be changed once company data submission is complete, even before the first case submission. Maximum 3 entries in the replacement list; exceeding this limit returns 400 validation_error.

</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — Registered or trading name of the company. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**notification_channels:** `typing.Optional[typing.List[PartnerCompanyNotificationChannelRequest]]` — Company-level email recipients for operational notifications, up to 10. Omit to preserve the recipients; a supplied array replaces them, and [] removes them. After the first case submission, required recipients for requests to client and statements must remain. Maximum 10 recipients in the replacement list; exceeding this limit returns 400 validation_error.

</dd>
</dl>

<dl>
<dd>

**payout_bank_account:** `typing.Optional[PayoutBankAccountRequest]` — Account to which collected funds are transferred. Omit to preserve the current account; before the first case submission, provide an account to replace it or null to remove it. After submission, changes must use the secured payout-account change process in the paywise UI. Resubmitting the unchanged account is allowed.

</dd>
</dl>

<dl>
<dd>

**phone:** `typing.Optional[str]` — Primary telephone number of the company in E.164 format; `null` clears it.

</dd>
</dl>

<dl>
<dd>

**tax_treatment:** `typing.Optional[TaxTreatmentEnum]` — Company VAT treatment, consistent with the address country. reverse_charge requires vat_number. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**vat_number:** `typing.Optional[str]` — Company VAT identification number. Required when tax_treatment is reverse_charge. Changes follow the paywise UI identity lock: after transfer for processing, or once company data is complete and a case has been submitted.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.companies.<a href="src/paywise/partner/companies/client.py">release_a_company</a>(...) -> CompanyReleaseReceipt</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

End all of this partner's access to a managed company. The company keeps its submitted cases, users, portal access and any credentials of its own. Orders this partner created on the company's behalf and never submitted are deleted; submitted orders and the company's own drafts survive. The company's `external_reference` is cleared so the same reference can onboard a fresh company later; the record itself stays attributed to the partner for history. Emits `company.access.revoked` with `reason: "partner_released"`. Requires an `Idempotency-Key` header and the `partner:companies:write` scope. Returns only an id and `case_access: unavailable` receipt. The same key replays this receipt; a new key after disconnection returns 404.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.companies.release_a_company(
    id="id",
    idempotency_key="Idempotency-Key",
    reason="Client ended the partner engagement.",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**reason:** `typing.Optional[str]` — Optional single-line note for the partner's own records, up to 5000 characters. It is not stored on the company and never appears in webhook payloads.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Company users

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">list_company_memberships</a>(...) -> PaginatedMembershipList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.list_company_memberships(
    company_id="company_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">add_a_company_membership</a>(...) -> MembershipWithSetupUrl</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.add_a_company_membership(
    company_id="company_id",
    idempotency_key="Idempotency-Key",
    email="email",
    first_name="first_name",
    last_name="last_name",
    role="admin",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request:** `MembershipRequest`

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">get_a_company_membership</a>(...) -> Membership</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.get_a_company_membership(
    company_id="company_id",
    membership_id="membership_id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**membership_id:** `str` — UUID of the company membership in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">change_a_pending_membership_role</a>(...) -> Membership</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.change_a_pending_membership_role(
    company_id="company_id",
    membership_id="membership_id",
    role="admin",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**membership_id:** `str` — UUID of the company membership in this request.

</dd>
</dl>

<dl>
<dd>

**role:** `RoleEnum`

New permissions for the pending membership.

- `admin` - admin
- `tax_consultant` - tax_consultant
- `member` - member
- `readonly` - readonly
- `developer` - developer

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">cancel_a_pending_company_membership</a>(...) -> Membership</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.cancel_a_pending_company_membership(
    company_id="company_id",
    membership_id="membership_id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**membership_id:** `str` — UUID of the company membership in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">replace_and_resend_a_pending_setup_token</a>(...) -> MembershipWithSetupUrl</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.replace_and_resend_a_pending_setup_token(
    company_id="company_id",
    membership_id="membership_id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**membership_id:** `str` — UUID of the company membership in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.company_users.<a href="src/paywise/partner/company_users/client.py">revoke_an_active_company_membership</a>(...) -> Membership</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The memberships of one managed company: list, add, and revoke users.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.company_users.revoke_an_active_company_membership(
    company_id="company_id",
    membership_id="membership_id",
    idempotency_key="Idempotency-Key",
    reason="reason",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company_id:** `str` — UUID of the managed company in this request.

</dd>
</dl>

<dl>
<dd>

**membership_id:** `str` — UUID of the company membership in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied key scoped to the Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**reason:** `str` — Reason for revoking the membership.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Events

<details><summary><code>client.partner.events.<a href="src/paywise/partner/events/client.py">list_events</a>(...) -> PartnerPaginatedEventFeed</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return one page of the partner's event feed, oldest first.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.events.list_events()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**company:** `typing.Optional[str]` — Return only events of this managed company.

</dd>
</dl>

<dl>
<dd>

**event_type:** `typing.Optional[typing.Union[ListEventsRequestEventTypeItem, typing.Sequence[ListEventsRequestEventTypeItem]]]` — Return only events of these exact types. Repeat the parameter for several types.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**since:** `typing.Optional[str]` — Opaque cursor taken from the `cursor` (or `next`) field of a previous page. Omit it to start at the oldest retained event (30 days). Entries become visible about 60 seconds after they are recorded, so a cursor never runs ahead of an event that is still being written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Meta

<details><summary><code>client.partner.meta.<a href="src/paywise/partner/meta/client.py">health_check</a>() -> PartnerHealthResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Unauthenticated liveness check for the Partner API.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.meta.health_check()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.meta.<a href="src/paywise/partner/meta/client.py">get_partner_token_info</a>() -> PartnerTokenInfoResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return non-PII metadata about the calling partner token: its id, name, scopes, capabilities and the owning partner. It never returns the owner's email or name.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.meta.get_partner_token_info()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Legal forms

<details><summary><code>client.partner.legal_forms.<a href="src/paywise/partner/legal_forms/client.py">list_legal_forms</a>(...) -> typing.List[LegalFormCatalog]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return the authenticated, tenant-independent public catalog.

`representative_requirements` are the roles company readiness requires
for a company with the legal form, in the `legal_representatives[].type`
vocabulary. They can differ from the Case Management API's debtor catalog.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.legal_forms.list_legal_forms()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Usage

<details><summary><code>client.partner.usage.<a href="src/paywise/partner/usage/client.py">get_rate_limit_headroom</a>() -> UsageResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return an authoritative point-in-time snapshot of all rate-limit buckets applicable to the authenticated Partner credential. The call itself counts against the token and partner buckets. The snapshot also includes the hourly per-partner mail budgets `mail:company-create` (company creates) and `mail:membership-create` (membership invites, inline users included). Those two are charged only by successful commands.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.usage.get_rate_limit_headroom()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Webhook deliveries

<details><summary><code>client.partner.webhook_deliveries.<a href="src/paywise/partner/webhook_deliveries/client.py">list_webhook_deliveries</a>(...) -> PaginatedPartnerWebhookDeliveryList</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhook_deliveries.list_webhook_deliveries()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**event_type:** `typing.Optional[ListWebhookDeliveriesRequestEventType]` — Exact delivered event type: a Partner lifecycle event, or a Case or Mahnservice event sent to a company-scoped subscription.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[ListWebhookDeliveriesRequestStatus]` — Exact delivery state: `pending`, `delivering`, `retrying`, `success`, or `failed`.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**webhook:** `typing.Optional[str]` — Return only deliveries for this webhook subscription's UUID.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhook_deliveries.<a href="src/paywise/partner/webhook_deliveries/client.py">get_webhook_delivery</a>(...) -> PartnerWebhookDelivery</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhook_deliveries.get_webhook_delivery(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook delivery in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhook_deliveries.<a href="src/paywise/partner/webhook_deliveries/client.py">redeliver_webhook_delivery</a>(...) -> PartnerWebhookCommandResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Re-enqueue a settled (`success`/`failed`) delivery as a new
attempt. 409 `conflict` on a disabled endpoint and 409
`delivery_in_progress` while the dispatcher still owns the row.
Deliveries outside current Partner authorization return 404.

</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhook_deliveries.redeliver_webhook_delivery(
    id="id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook delivery in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

## Webhooks

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">list_webhooks</a>(...) -> PaginatedPartnerWebhookList</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.list_webhooks()

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**cursor:** `typing.Optional[str]` — Opaque continuation cursor for incremental synchronization, taken from the `next` URL of a previous page. Only valid together with `updated_since`: with `updated_since` set the list is ordered by change time and then id and pages by this cursor instead of `offset`, so a row that changes while you page is returned again later instead of pushing another row out of the result. Rows changed less than 60 seconds ago are held back until they are settled; use the largest `updated_at` you received as the next `updated_since`.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether the webhook subscription is enabled. Omit to include both enabled and disabled subscriptions.

</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Number of results to return (maximum 100).

</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Zero-based result offset. Cannot be combined with `updated_since`; follow the `next` URL (`cursor`) instead.

</dd>
</dl>

<dl>
<dd>

**updated_since:** `typing.Optional[datetime.datetime]` — Return rows changed at or after this timezone-aware RFC 3339 timestamp. Results are ordered by updated_at and id (a requested `ordering` is ignored), page by `cursor` instead of `offset`, and rows changed less than a minute ago are held back.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">create_webhook</a>(...) -> PartnerWebhookWithSecret</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.create_webhook(
    idempotency_key="Idempotency-Key",
    url="url",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**url:** `str` — Publicly reachable HTTPS URL that receives webhook POST deliveries. The URL must be unique among this partner's v2 webhook endpoints. A Partner can register at most 20 webhook endpoints. Enabled and manually disabled endpoints count toward this limit; automatically disabled endpoints do not. Creating one more returns 409 webhook_limit_reached; delete an unused endpoint to free capacity.

</dd>
</dl>

<dl>
<dd>

**companies:** `typing.Optional[typing.Any]` — Company selector for case and Mahnservice events: the string "\*" includes every company with available partner case access, including companies added later; otherwise a JSON array of 1–500 accessible company UUIDs. Null makes the subscription lifecycle-only: no company case or Mahnservice events are delivered. Required for explicit case event types; omitted on PATCH preserves the selector.

</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — Optional single-line label for this webhook.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether new deliveries can be sent to this endpoint. Defaults to true on creation. The endpoint is automatically disabled after its configured consecutive terminal-failure threshold is reached. Re-enable it after resolving the delivery problem.

</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[PartnerWebhookSubscriptionEventEnum]]` — Event types this endpoint receives. Omitted on creation, defaults to all Partner lifecycle events; omitted on PATCH, preserves the selection. Use ["*"] alone to subscribe to all event types, with case events delivered only when a companies selector is configured. Explicit case event types require companies.

</dd>
</dl>

<dl>
<dd>

**max_consecutive_failures:** `typing.Optional[int]` — Automatically disables the endpoint when this many consecutive deliveries reach terminal failure. Retry attempts within one delivery do not each count. Raising it above the failure count of an automatically disabled endpoint makes that endpoint count toward the endpoint limit again and requires a free slot.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">get_webhook</a>(...) -> PartnerWebhook</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.get_webhook(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_none_match:** `typing.Optional[str]` — Return 304 with an empty body when the current `ETag` matches one of the supplied validators (or `*`).

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">delete_webhook</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.delete_webhook(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">update_webhook</a>(...) -> PartnerWebhook</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.update_webhook(
    id="id",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**if_match:** `typing.Optional[str]` — Apply the change only while the current `ETag` matches one of the supplied validators (or `*`); otherwise the request fails with `412 precondition_failed` and nothing is written.

</dd>
</dl>

<dl>
<dd>

**companies:** `typing.Optional[typing.Any]` — Company selector for case and Mahnservice events: the string "\*" includes every company with available partner case access, including companies added later; otherwise a JSON array of 1–500 accessible company UUIDs. Null makes the subscription lifecycle-only: no company case or Mahnservice events are delivered. Required for explicit case event types; omitted on PATCH preserves the selector.

</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — Optional single-line label for this webhook.

</dd>
</dl>

<dl>
<dd>

**enabled:** `typing.Optional[bool]` — Whether new deliveries can be sent to this endpoint. The endpoint is automatically disabled after its configured consecutive terminal-failure threshold is reached. Re-enable it after resolving the delivery problem. Automatically disabled endpoints do not count toward the endpoint limit, so re-enabling one requires a free slot; otherwise the request returns 409 webhook_limit_reached.

</dd>
</dl>

<dl>
<dd>

**events:** `typing.Optional[typing.List[PartnerWebhookSubscriptionEventEnum]]` — Event types this endpoint receives. Omitted on creation, defaults to all Partner lifecycle events; omitted on PATCH, preserves the selection. Use ["*"] alone to subscribe to all event types, with case events delivered only when a companies selector is configured. Explicit case event types require companies.

</dd>
</dl>

<dl>
<dd>

**max_consecutive_failures:** `typing.Optional[int]` — Automatically disables the endpoint when this many consecutive deliveries reach terminal failure. Retry attempts within one delivery do not each count. Raising it above the failure count of an automatically disabled endpoint makes that endpoint count toward the endpoint limit again and requires a free slot.

</dd>
</dl>

<dl>
<dd>

**url:** `typing.Optional[str]` — Publicly reachable HTTPS URL that receives webhook POST deliveries. The URL must be unique among this partner's v2 webhook endpoints. Manually disabled endpoints still count toward the maximum of 20 endpoints per Partner; automatically disabled endpoints do not.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">rotate_webhook_secret</a>(...) -> PartnerWebhookWithSecret</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.rotate_webhook_secret(
    id="id",
    idempotency_key="Idempotency-Key",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>

<details><summary><code>client.partner.webhooks.<a href="src/paywise/partner/webhooks/client.py">test_webhook</a>(...) -> PartnerWebhookCommandResult</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from paywise import Paywise
from paywise.environment import PaywiseEnvironment

client = Paywise(
    token="<token>",
    environment=PaywiseEnvironment.PRODUCTION,
)

client.partner.webhooks.test_webhook(
    id="id",
    idempotency_key="Idempotency-Key",
    event="company.created",
)

```

</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — UUID of the webhook subscription in this request.

</dd>
</dl>

<dl>
<dd>

**idempotency_key:** `str` — Required client-supplied command key scoped to the selected Case company or Partner owner, method, operation and path. An exact retry replays the original response while it is retained, including after credential rotation or replacement. Current permissions are required.

</dd>
</dl>

<dl>
<dd>

**event:** `PartnerWebhookTestEventEnum`

Partner lifecycle event type to use for the test delivery; must be one the webhook is subscribed to. Case events are tested through the company's Case Management API test route.

- `company.created` - company.created
- `company.case_submission_readiness.changed` - company.case_submission_readiness.changed
- `company.access.confirmed` - company.access.confirmed
- `company.access.revoked` - company.access.revoked
- `company.access.restored` - company.access.restored
- `company.user.added` - company.user.added
- `company.user.revoked` - company.user.revoked
- `company.user.activated` - company.user.activated
- `company.user.invite_expired` - company.user.invite_expired

</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.

</dd>
</dl>
</dd>
</dl>

</dd>
</dl>
</details>
