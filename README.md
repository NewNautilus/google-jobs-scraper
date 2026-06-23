[Google Jobs Scraper](https://apify.com/bluelightco/google-jobs-scraper?fpr=data)

**Google Jobs Scraper** is a powerful Apify actor designed to extract structured job posting data directly from Google Jobs. Whether you're a job seeker, market researcher, or developer, this actor allows you to efficiently search and collect listings based on role, location, and posting date.

---

## 🔍 Main Features

- **Smart Search Input:** Search for any job title or keyword using Google's native job search engine.
- **Location Targeting:** Filter results by specific cities, states, or countries.
- **Date Range Control:** Set the number of days to look back for recent job postings.
- **Result Limiting:** Specify how many job posts you want per search.
- **Rich Output:** Includes company name, title, job description, salary, schedule, work model, and source URLs.

---

## 🧾 Input Parameters

Configure the following input fields to customize your job search:

- **`query_input`** *(string)*:

The job title or keywords you want to search for (e.g., "Software Developer", "Marketing Manager").

**Default:** `"Software Developer"`
- **`location`** *(string)*:

The location to filter job results by. This can be a city, state, country, or use `"Remote"` to find remote jobs.

**Default:** `"United States"`
- **`days_to_search`** *(integer)*:

How many days back from today to look for job postings. Set to `7` to get jobs from the past week.

**Default:** `7`
- **`result_limit`** *(integer)*:

The maximum number of job listings to retrieve. Use this to control the amount of data returned.

**Default:** `10`

---

## 🚀 How to Use

1. **Configure Input:**

- Enter a job search term in `query_input` (e.g., "Data Scientist").
- Specify a `location` like "New York" or "Remote".
- Adjust `days_to_search` to control the recency of results.
- Optionally, set a `result_limit` for pagination control.
2. **Run the Actor:**

- Run it via the Apify console or API.
3. **Get the Data:**

- Output will be in structured JSON. You can export to CSV or integrate with other workflows.

---

## 📦 Output Example

**Example Output:**

```
{
  "title": "Software Developer (IC2) (Python)",
  "company_name": "Classlink",
  "location": "Anywhere",
  "google_url": "https://www.google.com/search?...",
  "details": [
    "2 days ago",
    "85K–100K a year",
    "Work from home",
    "Full-time"
  ],
  "extended_details": {
    "posted_at": "2 days ago",
    "salary": "85K–100K a year",
    "work_from_home": true,
    "schedule_type": "Full-time"
  },
  "description": "Software Developer (IC2) (Python)
Fully Remote • Development
Job Type
Full-time

Description
Would you like to join a rapidly growing and successful company?...",
  "urls": [
    {
      "title": "Edtech.com",
      "link": "https://www.edtech.com/jobs/software-developer..."
    },
    {
      "title": "SimplyHired",
      "link": "https://www.simplyhired.co.in/job/hk2tlBGeH68f..."
    },
    {
      "title": "Jobs4BW",
      "link": "https://www.jobs4bw.com/job/rowville-consulting..."
    }
  ]
}
```

---

## 🧠 Use Cases

- **Job Seekers:** Get detailed, fresh listings across industries and locations.
- **Recruiters:** Monitor job trends and employer demand.
- **Researchers & Analysts:** Analyze the job market programmatically.

---

## 📝 Notes

- Results are limited by Google Jobs' search interface and may vary based on availability and indexing.
- To ensure high accuracy, avoid overly broad queries and large result limits in one run.

---

## ❓ Need Help?

If you run into any issues or have feature requests, feel free to open an issue in the Apify platform or contact the actor maintainer.