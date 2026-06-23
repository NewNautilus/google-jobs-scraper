[Google Jobs Scraper](https://apify.com/thirdwatch/google-jobs-scraper?fpr=data)

# Google Jobs Scraper

> Scrape Google Jobs (Google for Jobs) aggregated listings — one search covers Indeed, LinkedIn, Glassdoor, ZipRecruiter, and dozens more.

## What you get

Google Jobs aggregates listings from 20+ job boards into a single search. This actor returns job titles, hiring companies, locations, salary ranges, full descriptions, employment types, original source boards, direct apply URLs, and posting dates — all from one query. Works for any country and any role.

## Output fields

| Field | Description |
| --- | --- |
| `title` | Job title |
| `company_name` | Hiring company |
| `location` | Job location |
| `salary` | Salary range (when available) |
| `description` | Full job description |
| `job_type` | Employment type (full-time, part-time, contract, etc.) |
| `source` | Original job board (Indeed, LinkedIn, Glassdoor, etc.) |
| `apply_url` | Direct apply URL |
| `posted_date` | Posting date |

## Example output

```
{
    "title": "Data Analyst",
    "company_name": "Amazon",
    "location": "Seattle, WA",
    "salary": "$85,000 - $120,000",
    "description": "We are looking for a Data Analyst to join our team and drive decisions across supply chain operations...",
    "job_type": "Full-time",
    "source": "LinkedIn",
    "apply_url": "https://www.linkedin.com/jobs/view/123456789",
    "posted_date": "2 days ago"
}
```

## Input parameters

| Parameter | Required | Description |
| --- | --- | --- |
| `queries` | Yes | Job search queries (e.g., `["software engineer new york", "data scientist remote"]`). Each query runs a separate Google Jobs search. |
| `maxResults` | No | Maximum number of jobs per query. Google Jobs shows ~10 initially and loads more on scroll. Default `5`. |
| `country` | No | Two-letter country code for localized results (e.g., `us`, `uk`, `in`, `de`). Default `us`. |
| `location` | No | Optional location to append to queries (e.g., `"San Francisco, CA"`). Leave blank to use location from the query text itself. |
| `proxyConfiguration` | No | Apify proxy settings. Leave default for best results. |

## Use cases

- **Job aggregators**: Pull listings from 20+ boards in one scrape instead of integrating each source separately.
- **Market researchers**: Compare job volume across sources for a given role and region.
- **HR analytics**: Track which boards dominate for specific roles in specific metros.
- **Job seekers**: Get a single merged view across Indeed, LinkedIn, Glassdoor, and more.

 

## Use cases & recipes

Step-by-step guides on [thirdwatch.dev/blog](https://thirdwatch.dev/blog):

- [Build a Multi-Source Jobs Feed with Google Jobs (2026)](https://thirdwatch.dev/blog/build-multi-source-jobs-feed-with-google-jobs)
- [Find Jobs with Direct Apply URLs (2026 Google Jobs Guide)](https://thirdwatch.dev/blog/find-jobs-with-direct-apply-urls)
- [Scrape Google Jobs Aggregated Listings (2026 Guide)](https://thirdwatch.dev/blog/scrape-google-jobs-aggregated-listings)
- [Track Job Posting Velocity on Google Jobs (2026)](https://thirdwatch.dev/blog/track-job-posting-velocity-on-google-jobs)

 -end

## Pricing

Pay-per-result pricing. Tiered discounts apply automatically based on usage volume.

| Tier | Price per result |
| --- | --- |
| FREE | $0.008 |
| BRONZE | $0.006 |
| SILVER | $0.005 |
| GOLD | $0.004 |

## Limitations

- Coverage depends on Google's own aggregation — not every job on every board appears in Google Jobs.
- Salary is not always present; it depends on whether the original source publishes it.
- Very broad queries (e.g., a single word) may return fewer results than a targeted `role + location` query.
- Results are localized by country code; runs using a different country code can return different listings for the same query.

## Compared to alternatives

- **vs. orgupdate/google-jobs** ($0.03 per result, ~800 users): This actor is roughly 3.75× cheaper at base price and supports the same aggregated output with direct apply URLs from each source.

Pairs well with [Indeed Scraper](https://apify.com/thirdwatch/indeed-scraper), [LinkedIn Jobs Scraper](https://apify.com/thirdwatch/linkedin-jobs-scraper), and [Monster Scraper](https://apify.com/thirdwatch/monster-scraper) when you want full descriptions from the original boards after discovery via Google.

## FAQ

**Which job boards does Google Jobs include?**
Indeed, LinkedIn, Glassdoor, ZipRecruiter, Monster, CareerBuilder, and many smaller specialist boards. Google decides the exact set per query.

**Can I scrape jobs outside the US?**
Yes. Set the `country` parameter (`uk`, `in`, `de`, `au`, etc.) and include a city in your query.

**Do results include direct apply links?**
Yes — the `apply_url` field points straight at the source board's apply page.

**How fresh is the data?**
Pulled live at run time.

Last verified: 2026-04

More scrapers at [thirdwatch.dev](https://thirdwatch.dev).