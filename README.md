# Tensorlake (tensorlake)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Tensorlake is a document ingestion and data extraction platform for AI applications. Its Document Ingestion API parses PDFs, images, and other documents into layout-aware Markdown and structured chunks (OCR, tables, figures, signatures), performs schema-guided structured extraction and classification, and manages reusable files and datasets. Tensorlake Cloud also runs serverless workflows and MicroVM sandboxes for agentic document pipelines.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tensorlake/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tensorlake/refs/heads/main/apis.yml)

## Access Model (Honest Summary)

- **Public, key-gated REST API.** The API is live at `https://api.tensorlake.ai` and is REST over HTTPS. An unauthenticated request returns HTTP 401 — Bearer auth is enforced.
- **Authentication:** API key created in the Tensorlake Cloud dashboard (`cloud.tensorlake.ai`), prefixed `tl_apiKey_`, passed as `Authorization: Bearer <token>`.
- **Asynchronous jobs, not sockets.** Parsing and extraction are submitted as jobs that return a `parse_id`; results are read back by polling `GET /documents/v2/parse/{parse_id}` or delivered via webhook. There is **no documented public WebSocket API** — see `review.yml`.
- **Confirmed vs modeled.** The endpoint **paths, HTTP methods, base URL, and Bearer auth are grounded** in Tensorlake's published OpenAPI document and API reference. The **request/response body schemas in `openapi/tensorlake-openapi.yml` are modeled** from the documentation and SDK behavior and are illustrative — verify field names against the live spec before generating client code. Modeled schemas are flagged inline.
- **Pricing is usage-based and not reconciled** in this entry (`reconciled: false`) — figures come from the public pricing page and third-party listings.

## Tags

- Document Extraction
- Data Extraction
- Document Ingestion
- Document Parsing
- OCR
- Data Ingestion
- AI
- Unstructured Data
- Document AI
- RAG

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Tensorlake Document Parse API

Submit a file, URL, or raw text/HTML for document parsing and retrieve layout-aware Markdown, page fragments, tables, and figures. Parsing runs as an asynchronous job — `POST /documents/v2/parse` returns a parse id, and results are read back with `GET /documents/v2/parse/{parse_id}` (or via webhook). Jobs can be listed and deleted.

- **Human URL:** [https://docs.tensorlake.ai/api-reference/parse/parse](https://docs.tensorlake.ai/api-reference/parse/parse)
- **Base URL:** `https://api.tensorlake.ai`

### Tensorlake Structured Extraction API

Extract structured JSON from documents guided by a JSON schema (`POST /documents/v2/extract`), classify documents (`POST /documents/v2/classify`), read/OCR raw content (`POST /documents/v2/read`), and apply edits (`POST /documents/v2/edit`). Turns unstructured documents into schema-conformant data for RAG and agent pipelines.

- **Human URL:** [https://docs.tensorlake.ai/document-ingestion/parsing/structured-extraction](https://docs.tensorlake.ai/document-ingestion/parsing/structured-extraction)
- **Base URL:** `https://api.tensorlake.ai`

### Tensorlake Files API

Upload and manage the files that parse and extraction jobs run against. Upload a file (`PUT /documents/v2/files`), list files (`GET /documents/v2/files`), read file metadata (`GET /documents/v2/files/{file_id}/metadata`), and delete a file (`DELETE /documents/v2/files/{file_id}`).

- **Human URL:** [https://docs.tensorlake.ai/api-reference/introduction](https://docs.tensorlake.ai/api-reference/introduction)
- **Base URL:** `https://api.tensorlake.ai`

### Tensorlake Datasets API

Group documents into datasets that apply a consistent parse and extraction configuration across many files. Create, list, get, update, and delete datasets, submit files to a dataset for processing (`POST /documents/v2/datasets/{dataset_id}/parse`), and read the accumulated structured output (`GET /documents/v2/datasets/{dataset_id}/data`).

- **Human URL:** [https://docs.tensorlake.ai/api-reference/introduction](https://docs.tensorlake.ai/api-reference/introduction)
- **Base URL:** `https://api.tensorlake.ai`

### Tensorlake Sandboxes API

Provision and manage MicroVM sandboxes that run serverless workflows and agent code alongside document ingestion. Create, list, get, update, and delete sandboxes, and snapshot, suspend, or resume them for durable, resumable execution.

- **Human URL:** [https://docs.tensorlake.ai/sandboxes/introduction](https://docs.tensorlake.ai/sandboxes/introduction)
- **Base URL:** `https://api.tensorlake.ai`

## Common Properties

- [Domain Security](security/tensorlake-domain-security.yml)
- [Authentication](authentication/tensorlake-authentication.yml)
- [GitHub Organization](https://github.com/tensorlakeai)
- [LinkedIn](https://www.linkedin.com/company/tensorlake)
- [Website](https://www.tensorlake.ai)
- [Documentation](https://docs.tensorlake.ai)
- [Plans](plans/tensorlake-plans-pricing.yml)
- [Rate Limits](rate-limits/tensorlake-rate-limits.yml)
- [Fin Ops](finops/tensorlake-finops.yml)
- [Blog](https://www.tensorlake.ai/blog)

## Review

See [review.yml](review.yml) for the WebSocket assessment (answer: **no** documented public WebSocket API) and the confirmed-vs-modeled endpoint breakdown.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
