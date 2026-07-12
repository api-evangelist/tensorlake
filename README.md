# Tensorlake (tensorlake)

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
