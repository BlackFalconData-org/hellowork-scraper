# Hellowork Scraper

Extract structured job data from [hellowork.com](https://hellowork.com) — France's major job board. Salary ranges, location data, and incremental change tracking across runs.

**[Hellowork Scraper on Apify →](https://apify.com/blackfalcondata/hellowork-scraper?fpr=1h3gvi)**

---

## Key features

**Search with filters** — Search by keyword and location. Filter by country, posted within, and more.

**Detail enrichment** — Fetch full job descriptions, salary data for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from hellowork.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from hellowork.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "développeur",
  "location": "Paris",
  "maxResults": 10
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. Use JSON array for multi-query. |
| `country` | enum | `"FR"` | Which hellowork.com market to search. |
| `location` | string | — | City, state, or region. Use JSON array for multi-location. |
| `startUrls` | array | — | Direct search or job detail URLs. |
| `maxResults` | integer | `25` | Maximum total job listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. |
| `daysPosted` | enum | `"all"` | Filter jobs by recency. Use '1' for incremental daily runs (only jobs posted in last 24h). |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, salary data, and company info. |
| `includeCompanyProfile` | boolean | `false` | Fetch company overview pages for industry, headcount, and more. |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. "us-software-nyc"). |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |
| `skipReposts` | boolean | `false` | When incremental, skip jobs whose content matches an expired job from a prior run (cross-run repost detection). |

---

## Output fields

Every listing returns the same 51-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyUrl`
- `companyLogo`
- `location`
- `locationRegion`
- `locationPostalCode`
- `locationCountry`
- `description`
- `descriptionText`
- `descriptionHtml`
- `descriptionMarkdown`
- `descriptionLength`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryUnit`
- `contractType`
- `employmentType`
- `industry`
- `occupationalCategory`
- `educationLevel`
- `experienceMonths`
- `directApply`
- `publishedAge`
- `postedAt`
- `validThrough`
- `canonicalUrl`
- `applyUrl`
- `sourceUrl`
- `sourceDomain`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `fetchedAt`
- `detailFetched`
- `contentQuality`
- `extractedEmails`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`
- `changeType`
- `trackedHash`
- `firstSeenAt`
- `lastSeenAt`
- `previousSeenAt`
- `expiredAt`
- `stateKey`

---

## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "10676b1b4dadad8cb24dbeab3ac5635a1ac3cce27c694a0bbb758fc2b4afbf0a",
  "jobKey": "75605607",
  "title": "Developpeur H/F",
  "company": "W Hunt",
  "companyUrl": "https://www.hellowork.com/fr-fr/entreprises/w-hunt-154580.html",
  "companyLogo": "https://f.hellowork.com/img/entreprises/160_160/154580.png",
  "location": "Paris",
  "locationRegion": "Île-de-France",
  "locationPostalCode": "75000",
  "locationCountry": "FR",
  "description": "Détail du posteW Hunt, marque de W Executive, recherche pour son client, un Analyste Programmeur/Développeur.NET F/H.Il s'agit d'un poste à pourvoir en CDI, situé en région Parisie…",
  "descriptionText": "Détail du posteW Hunt, marque de W Executive, recherche pour son client, un Analyste Programmeur/Développeur.NET F/H.Il s'agit d'un poste à pourvoir en CDI, situé en région Parisie…"
}
```

*Truncated — full records contain 51 fields. See Output fields for the complete schema.*

**[Try Hellowork Jobs Scraper now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/hellowork-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.008 |
| Result | $0.001 |

See the [actor on Apify](https://apify.com/blackfalcondata/hellowork-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape hellowork.com?**
Use this actor on Apify to extract structured data from hellowork.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get hellowork.com data as JSON, CSV, or Excel?**
The actor writes each listing to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape hellowork.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check hellowork.com's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for listings extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage. Expired listings can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Hellowork Jobs Scraper](https://apify.com/blackfalcondata/hellowork-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 04*
