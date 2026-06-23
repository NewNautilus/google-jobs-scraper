[Google Jobs Scraper](https://apify.com/khadinakbar/google-jobs-scraper?fpr=data)

# 🔍 Google Jobs Scraper — Fast, Cheap & MCP-Ready

Extract structured job listings from Google Jobs at **$3.00 per 1,000 results** — the most affordable Google Jobs scraper on Apify. Get job titles, companies, locations, full descriptions, parsed salary ranges (min/max numbers), apply links, and more in one clean JSON dataset.

Designed for recruiters, HR tech platforms, job board builders, and AI agents that need reliable, structured employment data at scale.

---

## Why This Scraper?

Most Google Jobs scrapers on Apify charge $150 per 1,000 results and still earn 1-2 star ratings from frustrated users. This actor is built differently:

- **50× cheaper** — $3/1,000 jobs vs $150/1,000 from the leading competitor
- **Salary parsing built-in** — raw strings like `"$120,000–$180,000 a year"` become `salary_min: 120000`, `salary_max: 180000`, `salary_period: "YEAR"` — ready for direct filtering and sorting
- **Multi-query batch runs** — search 10 job titles across 5 cities in a single actor run
- **Full descriptions** — clicks into each job's detail panel to get the complete description, qualifications, responsibilities, and benefits
- **Lightweight** — runs in 1GB RAM and finishes typical searches in under 5 minutes (competitors require 4GB RAM and 1-hour timeouts)
- **MCP-optimized** — complete dataset schema with field-level descriptions, so Claude, ChatGPT, and other AI agents understand your output immediately

---

## What Data You Get

Each job listing returns a consistent JSON object:

```
{
    "job_title": "Senior Software Engineer",
    "company_name": "Stripe",
    "location": "San Francisco, CA",
    "is_remote": false,
    "employment_type": "FULLTIME",
    "salary_range": "$160,000–$220,000 a year",
    "salary_min": 160000,
    "salary_max": 220000,
    "salary_period": "YEAR",
    "date_posted": "2 days ago",
    "job_description": "We are looking for a Senior Software Engineer to help build...",
    "highlights": {
        "qualifications": ["5+ years of backend experience", "Strong Python/Go skills"],
        "responsibilities": ["Design and own core payment infrastructure", "Mentor junior engineers"],
        "benefits": ["Competitive equity", "Health, dental, vision", "Remote-friendly"]
    },
    "apply_link": "https://stripe.com/jobs/listing/senior-software-engineer/12345",
    "via_platform": "LinkedIn",
    "search_query": "software engineer San Francisco",
    "source_url": "https://www.google.com/search?q=software+engineer+San+Francisco&ibp=htl%3Bjobs",
    "scraped_at": "2026-03-31T14:23:45.123Z"
}
```

---

## Input Parameters

### `searchQueries` (array of strings) — recommended

The job titles, skills, or keyword phrases to search on Google Jobs. Pass multiple queries to run batch searches in one actor run.

```
{
    "searchQueries": [
        "software engineer New York",
        "product manager remote",
        "data scientist Chicago"
    ],
    "maxResults": 150
}
```

### `startUrls` (array of URLs) — optional

Paste specific Google Jobs search URLs if you have them. Useful for repeating a search you've already configured in your browser.

```
{
    "startUrls": [
        { "url": "https://www.google.com/search?q=nurse+practitioner&ibp=htl;jobs" }
    ]
}
```

### `maxResults` (integer, 1–500, default: 50)

Maximum total job listings to extract across all queries. Each result costs $0.003. 100 results = $0.30.

### `datePosted` (string, default: "any")

Filter jobs by posting recency: `any`, `today`, `3days`, `week`, `month`.

### `employmentType` (string, default: "any")

Filter by contract type: `any`, `FULLTIME`, `PARTTIME`, `CONTRACTOR`, `INTERN`.

### `remoteOnly` (boolean, default: false)

When enabled, appends "remote" to all queries and marks all results `is_remote: true`.

### `proxyCountry` (string, default: "US")

2-letter country code for the residential proxy location. Controls which regional Google Jobs index is scraped (e.g. `"GB"` for UK jobs, `"CA"` for Canadian jobs).

---

## Use Cases

**Job board builders** — Pull fresh listings from Google Jobs daily and populate your own platform. Filter by location, type, and recency with a single API call.

**Recruitment & HR tech** — Track competitor hiring activity, monitor which companies are scaling in a given market, and identify salary benchmarks by role.

**Labour market research** — Map hiring trends across geographies. The `salary_min`/`salary_max` fields allow you to build salary distribution charts without writing any parsing code.

**AI agent pipelines** — This actor is MCP-compatible. Tell Claude or GPT "find 50 remote data science jobs posted this week" and it will call this actor and return structured results you can immediately use.

**Talent sourcing** — Use multi-query batch runs to search for 20 different roles across 10 cities in one single actor run. Cross-reference results to find companies actively hiring across multiple departments.

---

## Cost & Performance

| Scenario | Jobs | Estimated Cost | Est. Run Time |
| --- | --- | --- | --- |
| Quick spot check | 10 | $0.03 | ~1 min |
| Standard search | 50 | $0.15 | ~3 min |
| Batch (5 queries) | 200 | $0.60 | ~8 min |
| Large batch (10 queries) | 500 | $1.50 | ~15 min |

All costs include Apify compute. Your actor plan determines the platform base charge — see [Apify pricing](https://apify.com/pricing) for details.

---

## Pricing

This actor uses **Pay-Per-Event** pricing: you only pay for the jobs you actually extract.

**$0.003 per job result** ($3.00 per 1,000 jobs)

There are no monthly fees, no minimum spend, and no charge for failed runs or empty results. Your Apify subscription tier may apply volume discounts automatically.

---

## Technical Notes

**Why residential proxies?** Google aggressively blocks datacenter IP ranges on SERP pages. This actor uses residential proxies by default to ensure reliable results. Proxy costs are included in the per-result price.

**Selector resilience** — The actor uses multiple CSS selector fallbacks at every extraction step. If Google updates a class name, the actor attempts alternative selectors before failing. The most likely point of breakage after a Google UI change is the card-level extraction; if you notice zero results, open an issue and it will be patched within 24–48 hours.

**CAPTCHA handling** — If Google serves a CAPTCHA (rare with residential proxies), the actor skips that request and logs a warning. It will not crash; it continues processing other queries.

**Memory requirement** — 1,024 MB. This is significantly lower than competing actors that require 4,096 MB.

---

## Integration Examples

### Apify API (Node.js)

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('khadinakbar/google-jobs-scraper').call({
    searchQueries: ['frontend developer London', 'react developer remote'],
    maxResults: 100,
    datePosted: 'week',
    employmentType: 'FULLTIME',
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### Apify API (Python)

```
from apify_client import ApifyClient

client = ApifyClient(token="YOUR_API_TOKEN")

run = client.actor("khadinakbar/google-jobs-scraper").call(run_input={
    "searchQueries": ["data engineer New York"],
    "maxResults": 50,
    "remoteOnly": False,
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item["job_title"], item["salary_min"], item["salary_max"])
```

### Make (Integromat) / Zapier

Use the **Apify** module to call this actor with your search queries. Map the output fields to any downstream service — Google Sheets, Airtable, Notion, Slack, or a CRM.

---

## Limitations

- Google does not always display salary data. The `salary_range`, `salary_min`, and `salary_max` fields will be `null` for listings where the employer did not disclose pay.
- Google Jobs is limited to ~100 results per query by design. For more results, use multiple specific queries (e.g. split by city or role level).
- This actor does not bypass authentication — it only accesses the public Google Jobs search, no login required.
- If Google implements a new anti-bot challenge, success rate may temporarily dip. Issues are typically resolved within 48 hours.

---

## Support & Feedback

Found a bug or want a new feature? Open an issue directly in the actor's **Issues** tab — responses within 24 hours.

If this actor saved you time or money, please ⭐ leave a review — it helps other users find it and keeps this actor maintained.

---

## Changelog

**v0.1** — Initial release. Multi-query batch runs, salary parsing, full description extraction, MCP dataset schema, PAY_PER_EVENT pricing at $0.003/job.