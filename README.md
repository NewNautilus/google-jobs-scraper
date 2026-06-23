[Google Jobs Scraper](https://apify.com/sovereigntaylor/google-jobs-scraper?fpr=data)

# Google Jobs Scraper

Scrape job listings from **Google for Jobs** — the job search widget that appears directly in Google search results. Extract structured data including job titles, companies, salaries, descriptions, qualifications, benefits, apply links, and more.

## What is Google for Jobs?

Google for Jobs is a job search aggregator that pulls listings from hundreds of job boards (Indeed, LinkedIn, Glassdoor, ZipRecruiter, etc.) and displays them directly in Google search results. This actor scrapes that aggregated data, giving you a single unified view across all job sources.

## Features

- **Comprehensive extraction**: Job title, company, location, salary, description, qualifications, benefits, job type, schedule, remote status, and apply URLs
- **Multiple extraction strategies**: Parses Google's embedded JSON-LD (JobPosting schema), structured data attributes, and falls back to HTML parsing
- **Smart filtering**: Filter by date posted, job type, remote-only, and location
- **Pagination support**: Automatically follows Google's job listing pages to collect more results
- **Anti-blocking**: 12 rotating user agents, proxy support, request throttling, and retry logic
- **Pay-per-event pricing**: Only pay for successfully scraped job listings ($0.004/job)
- **Structured output**: Clean JSON output ready for analysis, databases, or spreadsheets

## Use Cases

### Job Market Research

- Track hiring trends across industries, roles, and locations
- Monitor which companies are expanding or contracting
- Analyze seasonal hiring patterns over time
- Compare job market health across different cities or regions

### Salary Benchmarking

- Collect salary data for specific roles across companies and locations
- Build salary databases for compensation analysis
- Track salary trends over time for specific positions
- Compare compensation packages across industries

### Recruitment Intelligence

- Monitor competitor hiring activity to understand their strategic direction
- Track new role types emerging in your industry
- Identify which skills and qualifications are in highest demand
- Find companies hiring for roles that match your recruitment pipeline

### Competitor Hiring Analysis

- Track which companies are hiring aggressively in your space
- Analyze the skills and qualifications competitors are seeking
- Monitor new teams or departments being built at competing firms
- Understand technology stack adoption through job requirements

### Academic Research

- Collect job market data for labor economics research
- Study the impact of remote work on job postings
- Analyze qualification inflation trends over time
- Track diversity and inclusion language in job postings

### Career Planning

- Research which skills are most in demand for your target role
- Understand salary ranges across different locations
- Track emerging job titles and career paths
- Compare job requirements across seniority levels

## Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `query` | String | Yes | - | Job search query (e.g., "software engineer", "marketing manager") |
| `location` | String | No | - | Geographic location filter (e.g., "New York, NY", "Remote") |
| `datePosted` | Enum | No | `any` | Filter by posting date: `any`, `today`, `3days`, `week`, `month` |
| `jobType` | Enum | No | `any` | Employment type: `any`, `fulltime`, `parttime`, `contractor`, `internship` |
| `remote` | Boolean | No | `false` | Only show remote/work-from-home positions |
| `maxResults` | Integer | No | `50` | Maximum job listings to scrape (0 = unlimited, max 500) |
| `languageCode` | String | No | `en` | Language for search results (ISO 639-1) |
| `countryCode` | String | No | `us` | Country for search results (ISO 3166-1 alpha-2) |
| `proxyConfiguration` | Object | No | - | Proxy settings (residential recommended) |

## Example Input

```
{
  "query": "software engineer",
  "location": "San Francisco, CA",
  "datePosted": "week",
  "jobType": "fulltime",
  "remote": false,
  "maxResults": 100,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Output Format

Each scraped job listing is stored as a JSON object with the following fields:

```
{
  "jobTitle": "Senior Software Engineer",
  "company": "Google",
  "location": "Mountain View, CA",
  "salary": "$150,000 - $200,000 a year",
  "salaryMin": 150000,
  "salaryMax": 200000,
  "salaryPeriod": "YEAR",
  "salaryCurrency": "USD",
  "description": "We are looking for a Senior Software Engineer to join our Cloud team...",
  "descriptionHtml": "<p>We are looking for...</p>",
  "datePosted": "2 days ago",
  "datePostedParsed": "2026-02-28T00:00:00.000Z",
  "via": "LinkedIn",
  "applyUrl": "https://www.linkedin.com/jobs/view/...",
  "applyUrls": [
    { "source": "LinkedIn", "url": "https://linkedin.com/..." },
    { "source": "Indeed", "url": "https://indeed.com/..." }
  ],
  "qualifications": [
    "Bachelor's degree in Computer Science or equivalent",
    "5+ years of software development experience",
    "Proficiency in Python, Java, or Go"
  ],
  "benefits": [
    "Health insurance",
    "401(k) matching",
    "Remote work flexibility"
  ],
  "responsibilities": [
    "Design and implement scalable backend services",
    "Mentor junior engineers",
    "Participate in code reviews"
  ],
  "jobType": "Full-time",
  "schedule": "Monday to Friday",
  "isRemote": false,
  "companyLogo": "https://encrypted-tbn0.gstatic.com/...",
  "companyRating": 4.3,
  "companyReviewCount": 12500,
  "jobId": "abc123def456",
  "sourceUrl": "https://www.google.com/search?q=software+engineer+jobs",
  "scrapedAt": "2026-03-02T12:00:00.000Z"
}
```

## Output Fields Reference

| Field | Type | Description |
| --- | --- | --- |
| `jobTitle` | String | Job position title |
| `company` | String | Hiring company name |
| `location` | String | Job location |
| `salary` | String | Salary as displayed by Google |
| `salaryMin` | Number | Parsed minimum salary (annual) |
| `salaryMax` | Number | Parsed maximum salary (annual) |
| `salaryPeriod` | String | Salary period: YEAR, MONTH, HOUR |
| `salaryCurrency` | String | Salary currency code (e.g., USD) |
| `description` | String | Full job description (plain text) |
| `descriptionHtml` | String | Job description with HTML formatting |
| `datePosted` | String | Relative posting date ("2 days ago") |
| `datePostedParsed` | String | Parsed ISO 8601 date |
| `via` | String | Source job board (Indeed, LinkedIn, etc.) |
| `applyUrl` | String | Primary application URL |
| `applyUrls` | Array | All application URLs with source names |
| `qualifications` | Array | Required qualifications |
| `benefits` | Array | Listed benefits and perks |
| `responsibilities` | Array | Job responsibilities |
| `jobType` | String | Employment type (Full-time, Part-time, etc.) |
| `schedule` | String | Work schedule if specified |
| `isRemote` | Boolean | Whether the job is remote |
| `companyLogo` | String | URL of the company logo |
| `companyRating` | Number | Company rating (e.g., 4.3 out of 5) |
| `companyReviewCount` | Number | Number of company reviews |
| `jobId` | String | Unique job identifier |
| `sourceUrl` | String | Google search URL used |
| `scrapedAt` | String | ISO 8601 timestamp of when the job was scraped |

## Tips for Best Results

1. **Use specific queries**: "senior python developer" works better than "developer"
2. **Add location**: Always specify a location for more targeted results
3. **Use residential proxies**: Google blocks datacenter IPs aggressively
4. **Start small**: Test with `maxResults: 10` before running large scrapes
5. **Combine filters**: Use `datePosted: "week"` + `jobType: "fulltime"` for focused results

## Proxy Configuration

Google is aggressive about blocking automated requests. For reliable results:

- **Residential proxies** are strongly recommended
- **Datacenter proxies** may work for small volumes but will get blocked quickly
- Set proxy groups to `["RESIDENTIAL"]` in the Apify proxy configuration

## Rate Limits and Fair Use

- The actor automatically throttles requests to avoid triggering Google's anti-bot measures
- Each search page returns approximately 10 job listings
- Large scrapes (500+ jobs) may take several minutes due to rate limiting
- The actor respects Google's robots.txt and rate limits

## Pricing

This actor uses **Pay-Per-Event (PPE)** pricing:

| Event | Price | Description |
| --- | --- | --- |
| `job-scraped` | $0.004 | Charged per job listing successfully scraped |

Example: Scraping 100 job listings costs approximately $0.40.

## Integration Examples

### Export to CSV

Use the Apify dataset export feature to download results as CSV for spreadsheet analysis.

### Webhook to Database

Set up an Apify webhook to POST results to your API endpoint after each run.

### Schedule Regular Runs

Use Apify schedules to run the actor daily/weekly for ongoing job market monitoring.

## Changelog

### v1.0.0 (2026-03-02)

- Initial release
- Google for Jobs widget scraping with multiple extraction strategies
- Support for all Google Jobs filters (date, type, remote, location)
- JSON-LD schema.org/JobPosting parsing
- HTML fallback extraction
- Pay-per-event pricing
- 12 rotating user agents
- Comprehensive proxy support

## Support

If you have questions or issues, please open an issue on the actor's page or contact the author.

## License

MIT License. This actor is provided as-is for legitimate job market research purposes. Please respect Google's Terms of Service and the job boards' terms when using scraped data.

## Related Actors

- [Indeed Scraper](https://apify.com/sovereigntaylor/indeed-scraper) — Indeed job listings
- [LinkedIn Jobs Scraper](https://apify.com/sovereigntaylor/linkedin-jobs-scraper) — LinkedIn job data
- [Indeed Salary Scraper](https://apify.com/sovereigntaylor/indeed-salary-scraper) — Salary benchmarks
- [Glassdoor Scraper](https://apify.com/sovereigntaylor/glassdoor-scraper) — Company reviews
- [Job Market Analyzer](https://apify.com/sovereigntaylor/job-market-analyzer) — Multi-source job intelligence