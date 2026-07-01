# FullEnrich (fullenrich)

FullEnrich is a B2B contact enrichment platform that finds verified business emails and mobile phone numbers by running a waterfall across 15+ data vendors. Its API accepts contacts by name plus company (domain or company name) or LinkedIn URL, submits them for bulk enrichment, and returns the most probable work email, personal email, and mobile phone, billing credits only when data is found.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/fullenrich/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/fullenrich/refs/heads/main/apis.yml)

## Tags

- B2B Data
- Contact Enrichment
- Email Finder
- Phone Finder
- Waterfall Enrichment
- Sales Intelligence

## Timestamps

- **Created:** 2026-07-01
- **Modified:** 2026-07-01

## APIs

### FullEnrich Contact Enrichment API

Submit up to 100 contacts per request for bulk waterfall enrichment by first name, last name, and company domain or company name (LinkedIn URL optional), then poll or receive a webhook to retrieve the most probable work email, personal email, and mobile phone plus full enrichment status.

- **Human URL:** [https://docs.fullenrich.com/api/v2/contact/enrich/bulk/post](https://docs.fullenrich.com/api/v2/contact/enrich/bulk/post)
- **Base URL:** `https://app.fullenrich.com/api/v2`

#### Tags

- Contact Enrichment
- Email Finder
- Phone Finder
- Waterfall

#### Properties

- [Documentation](https://docs.fullenrich.com/api/v2/contact/enrich/bulk/post)
- [API Reference](https://docs.fullenrich.com/api/v2/contact/enrich/bulk/post)
- [OpenAPI](openapi/fullenrich-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/fullenrich.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/fullenrich.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### FullEnrich Enrichment Results API

Retrieve the results of a bulk enrichment by its enrichment_id, returning the run status, credits consumed, and per-contact enriched data including emails with deliverability status and phones in E.164 format.

- **Human URL:** [https://docs.fullenrich.com/api/v2/contact/enrich/bulk/get](https://docs.fullenrich.com/api/v2/contact/enrich/bulk/get)
- **Base URL:** `https://app.fullenrich.com/api/v2`

#### Tags

- Results
- Polling
- Enrichment

#### Properties

- [Documentation](https://docs.fullenrich.com/api/v2/contact/enrich/bulk/get)
- [OpenAPI](openapi/fullenrich-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/fullenrich.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/fullenrich.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### FullEnrich Reverse Email Lookup API

Resolve a person and company from an email address in bulk, then retrieve the identified profile and contact information by the reverse lookup's enrichment_id.

- **Human URL:** [https://docs.fullenrich.com/](https://docs.fullenrich.com/)
- **Base URL:** `https://app.fullenrich.com/api/v2`

#### Tags

- Reverse Email
- Identity Resolution
- Enrichment

#### Properties

- [Documentation](https://docs.fullenrich.com/)
- [OpenAPI](openapi/fullenrich-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/fullenrich.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/fullenrich.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### FullEnrich Account Credits API

Check the current credit balance available in your workspace before submitting enrichment jobs, so clients can gate spend against remaining credits.

- **Human URL:** [https://docs.fullenrich.com/](https://docs.fullenrich.com/)
- **Base URL:** `https://app.fullenrich.com/api/v2`

#### Tags

- Account
- Credits
- Billing

#### Properties

- [Documentation](https://docs.fullenrich.com/)
- [OpenAPI](openapi/fullenrich-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/fullenrich.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/fullenrich.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/FullEnrich)
- [LinkedIn](https://www.linkedin.com/company/fullenrich)
- [Website](https://fullenrich.com)
- [Documentation](https://docs.fullenrich.com)
- [Plans](plans/fullenrich-plans-pricing.yml)
- [Rate Limits](rate-limits/fullenrich-rate-limits.yml)
- [Fin Ops](finops/fullenrich-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
