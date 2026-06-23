[Google Jobs Scraper](https://apify.com/scrape.badger/google-jobs-scraper?fpr=data)

## What does Google Jobs Scraper do?

Scrape [Google for Jobs](https://www.google.com/search?q=jobs) — the aggregator that pulls from LinkedIn, Indeed, company career pages and more. Keyword + location search with date-posted, job-type, remote, and radius filters.

## Why use Google Jobs Scraper?

- **Aggregated source.** LinkedIn, Indeed, Glassdoor, Monster, company careers — Google de-duplicates across them.
- **Filter set.** `date_posted`, `job_type`, `ltype` (remote), `lrad` (radius).
- **200+ country domains.** Local job markets with `gl` + `hl`.
- **Per-job apply link.** Direct-to-apply URL when Google surfaces it.
- **Two modes.** `rpc` (fast API) or `serp` (full SERP context).

## What data can Google Jobs Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| title | string | Job title |
| company | string | Employer name |
| location | string | Job location |
| via | string | Source site |
| description | string | Full job description |
| posted_at | string | Human-readable (e.g. '3 days ago') or ISO |
| schedule | string | Full-time / part-time / contract / internship |
| job_type | string | Remote / hybrid / on-site |
| thumbnail | string | Company logo URL |
| apply_link | string | Direct apply URL |

## How to scrape Google Jobs (Google for Jobs)

1. Click **Try for free**.
2. Enter your query in `q` (e.g. `senior backend engineer python`).
3. Optional: set `location`, `date_posted` (past day/week/month), `job_type`, `ltype` (remote only).
4. Set `gl` / `hl` for country + language.
5. Set `max_pages` — each page is ≈ 10 jobs.
6. Click **Start** — jobs stream into the dataset.

## How much will it cost?

**$0.008 per page (≈ $8 per 1,000 pages).** One call per page. A 3-page run pushes ≈ 30 jobs for $0.024.

### Competitor benchmark

| Actor | Author | Price | Notes |
| --- | --- | --- | --- |
| bebity/indeed-scraper | bebity | $29 /mo subscription | Indeed-only |
| curious_coder/linkedin-jobs-scraper | curious_coder | ~$12 / 1k | LinkedIn-only |
| community/google-jobs-scraper | community | ~$10 / 1k | Google-aggregated |
| **scrape-badger/google-jobs-scraper** | **ScrapeBadger** | **$8 / 1k pages** | **20% below closest competitor** |

## Input

Configure the run in the **Input** tab above, or pass a JSON object matching the fields below when calling the Actor via the Apify API.

| Field | Required | Description |
| --- | --- | --- |
| q | ✅ | Job search query. |
| mode | — | `rpc` (default, fast) or `serp` (rich SERP context). |
| location | — | City / region string. |
| date_posted | — | Google enum: `today` / `3days` / `week` / `month`. |
| job_type | — | Full-time / part-time / contract / internship. |
| ltype | — | Remote filter. |
| lrad | — | Radius in km / miles. |
| gl / hl | — | Country + language. |
| max_pages | — | Pagination budget. |

## Output

Every successful run streams records into the run's dataset. Download as JSON, CSV, XML, Excel, or HTML from the **Dataset** tab; consume programmatically via the Apify API or webhooks.

Example record:

```
{
  "title": "Senior Backend Engineer (Python)",
  "company": "Acme Corp",
  "location": "New York, NY (Remote)",
  "via": "LinkedIn",
  "description": "We're looking for\u2026",
  "posted_at": "3 days ago",
  "schedule": "Full-time",
  "job_type": "Remote",
  "thumbnail": "https://\u2026",
  "apply_link": "https://linkedin.com/jobs/view/\u2026"
}
```

## Tips / Advanced options

- **Use `date_posted: today` for real-time sourcing.** Recruiters win by speed — hit Google Jobs with a cron every hour for fresh postings.
- **SERP mode adds context.** `mode: serp` returns richer results (featured snippets, related searches). Slower but better for market intelligence.
- **Dedupe by `apply_link`.** Google aggregates from multiple sources — same job may appear under different `via`. `apply_link` is the canonical dedupe key.
- **`ltype` filters remote-only.** Essential for distributed-team recruiters.

## FAQ, Disclaimers, Support

### Can I filter by salary?

Not at the query level — Google doesn't consistently surface salary. Post-filter on `description` if the posting includes it.

### Why are some jobs missing `apply_link`?

Google doesn't always expose it. When absent, the full description typically includes contact info.

### What's the difference between `mode: rpc` and `mode: serp`?

`rpc` is Google's internal API (fast, cheap, jobs-only). `serp` is the full SERP rendering (more context, slower). Default `rpc` is what most users want.

### Can I scrape LinkedIn directly?

This actor proxies Google's LinkedIn aggregation. For direct LinkedIn scraping, use a dedicated LinkedIn actor (outside this suite).

### Disclaimer

This Actor scrapes public Google data only. You're responsible for compliance with Google's Terms of Service and any applicable data-protection laws (GDPR, CCPA, etc.) in your jurisdiction. ScrapeBadger does not store the scraped results — they are delivered directly to your Apify dataset.

### Support

Something not working? Open a ticket in the **Issues** tab above — we triage within one business day. Full API reference: [docs.scrapebadger.com](https://docs.scrapebadger.com).

### Powered by

[ScrapeBadger](https://scrapebadger.com) — Google-optimised residential proxy pool + browser-farm fallback, 99.7% uptime, unmetered bandwidth. No CAPTCHAs reach you.