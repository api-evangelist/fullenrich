# FullEnrich (fullenrich)

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
