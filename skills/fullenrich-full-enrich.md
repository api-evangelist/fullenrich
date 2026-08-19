---
name: Full Enrich
description: Use when enriching B2B contact data (emails, phone numbers), performing reverse email lookups to identify people behind email addresses, or searching for contacts and companies by filters. Agents should reach for this skill when building integrations that need to find or verify professional contact information at scale.
metadata:
    mintlify-proj: fullenrich
    version: "1.0"
---

# FullEnrich Skill

## Product Summary

FullEnrich is a B2B contact data API that aggregates data from 20+ providers to find work emails, mobile phone numbers, personal emails, and professional profiles for people and companies. Agents use it to enrich contact lists, identify people from email addresses, and search for prospects by filters. The API is asynchronous (results delivered via webhook) for enrichment and reverse lookup, and synchronous for search. Primary docs: https://docs.fullenrich.com. Key endpoints: `POST /contact/enrich/bulk`, `POST /contact/reverse/email/bulk`, `POST /people/search`, `POST /company/search`. Authentication: Bearer token in `Authorization` header. Rate limit: 60 API calls/minute (up to 6,000 contacts/minute with bulk). Credits consumed only on successful matches.

## When to Use

Reach for this skill when:
- A user needs to find work email or phone number for a B2B contact (provide name + company or LinkedIn URL)
- A user has an email and needs to identify the person and company behind it
- A user needs to search for contacts or companies matching specific criteria (industry, location, company size, job title, etc.)
- Building a workflow that enriches contact lists in bulk (up to 100 contacts per request)
- Integrating contact data into a CRM, sales tool, or prospecting platform
- Testing data enrichment without spending credits (use FullEnrich team test contacts)
- A user asks about credit consumption, rate limits, or webhook setup for production use

Do not use this skill for: personal data enrichment, non-B2B use cases, or when you need synchronous enrichment (use Search API instead for immediate results).

## Quick Reference

### Core Endpoints

| Endpoint | Method | Use Case | Async | Credits |
|----------|--------|----------|-------|---------|
| `/contact/enrich/bulk` | POST | Find email/phone for person | Yes | 1 (email), 10 (phone), 3 (personal email) |
| `/contact/reverse/email/bulk` | POST | Identify person from email | Yes | 1 per match |
| `/people/search` | POST | Search contacts by filters | No | 0.25 per result |
| `/company/search` | POST | Search companies by filters | No | 0.25 per result |
| `/account/credits/get` | GET | Check remaining credits | No | 0 |

### Authentication

```
Authorization: Bearer YOUR_API_KEY
```

Get API key from https://app.fullenrich.com/app/api. Keep it secure; regenerate if compromised.

### Bulk Enrichment Input Requirements

Provide **either**:
1. `first_name` + `last_name` + `company` (domain or company_name)
2. `linkedin_url`

For best results, include LinkedIn URL (+5–20% email improvement, +10–60% phone improvement).

### Rate Limits & Quotas

- **60 API calls per minute** (all endpoints)
- **100 contacts per bulk request** (Enrich/Reverse Lookup)
- **6,000 contacts per minute** possible (60 requests × 100 contacts)
- **100 concurrent enrichments** (default queue size)
- **100 concurrent reverse lookups** (default queue size)
- Search API: synchronous, no queue

### Credit Costs

| Operation | Cost | Condition |
|-----------|------|-----------|
| Work email found | 1 credit | Deliverable, High Probability, or Catch-all |
| Mobile phone found | 10 credits | Valid number |
| Personal email found | 3 credits | Valid email |
| Reverse email lookup | 1 credit | Person identified |
| Search result | 0.25 credit | Per person/company (0 if exported before) |
| Duplicate contact | 0 credits | Re-enriched within 3 months |

### Webhook Signature Verification

Every webhook includes `X-Signature-SHA1` header (HMAC-SHA1 of body using API key as secret). Verify before processing:

```javascript
// Node.js example
const crypto = require('crypto');
const expected = crypto.createHmac('sha1', apiKey).update(rawBody, 'utf8').digest('hex');
const valid = crypto.timingSafeEqual(Buffer.from(expected), Buffer.from(signatureHeader));
```

## Decision Guidance

### When to Use Webhooks vs Polling

| Scenario | Use Webhooks | Use Polling |
|----------|--------------|------------|
| Production integration | ✓ Always | ✗ Never |
| Real-time results needed | ✓ Use `webhook_events.contact_finished` | ✗ Consumes rate limit |
| Batch processing | ✓ Recommended | ✗ Only if must (max every 5-10 min) |
| Testing/debugging | ✓ Use webhook.site | ✓ OK for one-off checks |

### When to Use Enrich vs Search vs Reverse Lookup

| Goal | Endpoint | Input | Speed | Cost |
|------|----------|-------|-------|------|
| Find email/phone for known person | Enrich | Name + company or LinkedIn | Async (30-90s) | 1-10 credits |
| Identify person from email | Reverse Lookup | Email address | Async (30-90s) | 1 credit |
| Find prospects matching criteria | Search | Filters (industry, location, etc.) | Immediate | 0.25 credit |
| Verify single contact now | Search (Lookup) | Name + company or LinkedIn | Immediate | 0.25 credit |

### Bulk vs Single Contact

| Scenario | Approach |
|----------|----------|
| 1-100 contacts at once | Use bulk endpoint (1 request) |
| 1 contact | Pass array with 1 item to bulk endpoint |
| Thousands of contacts | Split into batches of 100, send sequentially |
| Real-time single enrichment | Use Search Lookup endpoint (synchronous) |

## Workflow

### Enriching a Contact List

1. **Prepare input data**: Gather first_name, last_name, company (domain or name) for each contact. Include linkedin_url if available for better results.

2. **Check credits**: Call `GET /account/credits/get` to verify sufficient credits for your batch size.

3. **Build request**: Create JSON payload with up to 100 contacts. Include `webhook_url` for results. Add `custom` field with CRM ID or user ID for tracking.

4. **Send enrichment**: POST to `/contact/enrich/bulk` with Bearer token in Authorization header.

5. **Receive enrichment_id**: API returns immediately with `enrichment_id`. Store this for reference.

6. **Receive webhook**: When enrichment completes (typically 30-90 seconds), FullEnrich POSTs results to your webhook URL. Verify `X-Signature-SHA1` header before processing.

7. **Parse results**: Extract contact_info (emails, phones) and profile (job title, location, etc.) from webhook payload. Use `custom` field to match results to your internal records.

8. **Handle failures**: Check `status` field in response. If contact not found, `contact_info` will be empty but no credits consumed.

### Reverse Email Lookup

1. **Collect emails**: Gather work or personal email addresses.

2. **Send request**: POST to `/contact/reverse/email/bulk` with email array and webhook_url.

3. **Receive results**: Webhook delivers full person profile (name, job title, location, work history) and company details.

4. **Match to records**: Use `custom` field to link results back to your system.

### Searching for Prospects

1. **Define filters**: Build filter object (industry, company_size, location, job_title, etc.). See docs for predefined values.

2. **Send search**: POST to `/people/search` or `/company/search` with filters, offset, and limit.

3. **Receive results immediately**: API returns matching contacts/companies synchronously.

4. **Paginate**: Use offset/limit to loop through larger result sets.

5. **Export**: Results cost 0.25 credit each (0 if previously exported).

## Common Gotchas

- **Custom field must be string**: Pass numbers as strings in `custom` object, or request will fail with error.

- **Webhook signature verification is critical**: Always verify `X-Signature-SHA1` before processing webhook data. Use raw request body (before JSON parsing) for verification.

- **Polling consumes rate limit**: Each GET request to check status counts against 60 calls/minute. Use webhooks instead.

- **Duplicate contacts within same bulk**: Deduplication does not work within a single bulk request. If you send the same contact twice in one batch, both will be enriched and charged.

- **Data retention is 3 months**: Enrichment results stored for 3 months only (GDPR). After 3 months, re-enriching the same contact costs credits again.

- **LinkedIn URL improves results significantly**: Including LinkedIn URL can improve email discovery by 5–20% and phone by 10–60%. Always ask users for it if available.

- **silentFail parameter for production**: Use `?silentFail=true` query parameter to skip invalid contacts instead of failing the entire batch.

- **Search API is synchronous, not async**: Search endpoints return immediately; no webhook needed. Enrich and Reverse Lookup are async only.

- **Queue size limits concurrent operations**: Default 100 concurrent enrichments. If you exceed this, contacts wait in queue. For high volume, contact FullEnrich to increase.

- **Webhook retries are automatic**: If your server returns non-2xx, FullEnrich retries every minute for 5 attempts. Ensure your webhook endpoint is stable.

- **Test with zero-credit contacts**: Use exact FullEnrich team contact data (Grégoire Démogé, fullenrich.com) for testing without spending credits.

## Verification Checklist

Before submitting work with FullEnrich integration:

- [ ] API key is stored securely (environment variable, not hardcoded)
- [ ] Authorization header format is correct: `Authorization: Bearer YOUR_API_KEY`
- [ ] Webhook URL is publicly accessible and returns 2xx status
- [ ] Webhook signature verification implemented (X-Signature-SHA1 check)
- [ ] Custom field values are strings (not numbers)
- [ ] Bulk requests contain 1-100 contacts (not more)
- [ ] Input data includes first_name + last_name + company OR linkedin_url
- [ ] Webhook handler uses raw request body for signature verification (not parsed JSON)
- [ ] Rate limit handling in place (60 calls/minute, batch up to 100 contacts)
- [ ] Credit balance checked before large enrichment runs
- [ ] Error handling for 401 (invalid key), 400 (bad input), 429 (rate limit)
- [ ] Tested with webhook.site or similar to inspect actual webhook payload
- [ ] Production uses silentFail=true to skip invalid contacts
- [ ] Low-credit alerts configured in dashboard

## Resources

- **Comprehensive page navigation**: https://docs.fullenrich.com/llms.txt
- **API Introduction & Overview**: https://docs.fullenrich.com/api/v2/general/introduction
- **Authentication Setup**: https://docs.fullenrich.com/api/v2/general/authentication
- **Webhooks & Result Delivery**: https://docs.fullenrich.com/api/v2/general/webhooks
- **Credits & Testing**: https://docs.fullenrich.com/api/v2/general/credit
- **Rate Limits & Volume**: https://docs.fullenrich.com/api/v2/implement-in-product/volume
- **Production Deployment**: https://docs.fullenrich.com/api/v2/implement-in-product/production

---

> For additional documentation and navigation, see: https://docs.fullenrich.com/llms.txt