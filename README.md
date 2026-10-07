# GitHub Repo Scraper: Stars, README, License & Releases

Deep metadata for any public GitHub repository: stars, forks, language breakdown, topics, license, README, contributor count, latest release, and commit recency. No token required. MCP-ready for AI agents.

**Run it on Apify:** [apify.com/themineworks/github-repo-intelligence](https://apify.com/themineworks/github-repo-intelligence)
**Docs, FAQ and pricing:** [themineworks.com/actors/github-repo-intelligence](https://themineworks.com/actors/github-repo-intelligence/)

**Price:** From $1.20 per 1,000 repos on Apify's higher plans ($2.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged.

## What it returns

* Stars, forks, watchers, and open issue count
* Language breakdown and repo topics/tags
* Full README content and license
* Contributor count, latest release, and commit recency
* No GitHub token required. Public API only
* MCP-ready for AI agent workflows

## Quick start

You need a free [Apify account](https://console.apify.com/sign-up) and its API token (Settings, API & Integrations).

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("themineworks/github-repo-intelligence").call(run_input={
    "repos": [
        "anthropics/claude-code"
    ]
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });
const run = await client.actor('themineworks/github-repo-intelligence').call({
    "repos": [
        "anthropics/claude-code"
    ]
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL

One request that runs the actor and returns the results in the response (for runs under 5 minutes):

```bash
curl -X POST "https://api.apify.com/v2/acts/themineworks~github-repo-intelligence/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"repos": ["anthropics/claude-code"]}'
```

### Command line

This repo includes ready-made clients that save results to JSON and CSV:

```bash
python3 github_repo_scraper.py --token YOUR_APIFY_TOKEN --repos "anthropics/claude-code"
node github_repo_scraper.mjs --token YOUR_APIFY_TOKEN --repos "anthropics/claude-code"
```

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `repos` (required) | array |  | List of GitHub repos as "owner/repo" or full URLs |
| `includeReadme` | boolean | `true` | Fetch and include the full decoded README content for each repo |

## Output

One row per result, as JSON, CSV, Excel or through the API.

| Field | Type | Description |
|---|---|---|
| `owner` | string | Repository owner/org |
| `repo` | string | Repository name |
| `fullName` | string | owner/repo |
| `url` | string | GitHub repo URL |
| `description` | string | Repo description |
| `stars` | number | Stargazers count |
| `forks` | number | Forks count |
| `openIssues` | number | Open issues + PRs count |
| `primaryLanguage` | string | Primary language |
| `languages` | object | Language -> bytes breakdown |
| `topics` | array | Repo topics/tags |
| `license` | string | License SPDX ID |
| `defaultBranch` | string | Default branch name |
| `createdAt` | string | Repo creation date |
| `updatedAt` | string | Last metadata update |
| `lastCommitAt` | string | Last push/commit date |
| `homepage` | string | Homepage URL |
| `isArchived` | boolean | Whether the repo is archived |
| `isFork` | boolean | Whether this repo is a fork |
| `contributorsCount` | number | Approximate contributor count |
| `latestReleaseTag` | string | Latest release tag |
| `latestReleaseAt` | string | Latest release publish date |
| `readme` | string | Full decoded README text (if includeReadme=true) |
| `scraped_at` | string | ISO timestamp when scraped |

## Use it from an AI agent

The actor works as a tool in Claude, Cursor or any MCP client through Apify's MCP server:

```
https://mcp.apify.com/?tools=themineworks/github-repo-intelligence
```

## FAQ

### Do I need a GitHub token?

No. This actor uses GitHub's public, unauthenticated endpoints, so there's no token to manage or rate-limit against your own account.

### What is the price?

Pay per result: from $1.20 per 1,000 repos on Apify's higher plans, $2.00 on the free plan, plus a $0.005 start fee per run. Failed results are never charged.

### Can I export the results to CSV or Excel?

Yes. Every run saves to an Apify dataset you can download as JSON, CSV, Excel or XML, or read through the API. The Python and Node clients in this repo also write the results to local files.

### Can I run it on a schedule?

Yes. Save your input as a task on Apify and attach a schedule, or call the API from your own cron job. Scheduled runs are billed the same way as manual ones.

## Related scrapers

* [YouTube Transcript Scraper](https://themineworks.com/actors/youtube-transcript-scraper/): Timestamped captions to JSON. No API key, no login
* [RAG Website Crawler](https://themineworks.com/actors/rag-crawler/): Pre-chunked markdown with token counts for RAG pipelines
* [Podcast Episode Scraper](https://themineworks.com/actors/podcast-episode-scraper/): RSS feed to episode metadata, audio URLs, and transcripts

Part of [The Mine Works](https://themineworks.com/): 151 pay-per-result scrapers with no login and no browser setup on your side.

## License

MIT © The Mine Works
