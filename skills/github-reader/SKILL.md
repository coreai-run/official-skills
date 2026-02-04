---
name: github-reader
description: Fetch trending GitHub repositories. USE WHEN user says 'github trending', 'new repos', 'github projects', 'open source'.
---

# GitHub Reader

Fetches trending repositories from GitHub based on keywords.

## Configuration
!`coreai config show github-reader`

## Instructions

1. **Search repositories** for each keyword
2. **Filter by language** if configured
3. **Filter by pushed date** within `hours`
4. **Sort by stars** (descending)
5. **Deduplicate** by repo ID across keywords

### API Details

- Endpoint: `https://api.github.com/search/repositories`
- Parameters: `q`, `sort=stars`, `order=desc`, `per_page`
- Rate limit: 10 requests/minute (unauthenticated)

### Query Construction

q={keyword} in:name,description,topics language:{language} pushed:>={date}

### Example

curl -H "Accept: application/vnd.github.v3+json" \
  "https://api.github.com/search/repositories?q=langchain+language:python+pushed:>=2024-01-20&sort=stars&order=desc&per_page=5"

### Output Format

## GitHub Trending - Last {hours} hours

- [owner/repo](url) - Python - 1,234 stars
  > Repository description...

### Rate Limiting

- Add 100ms delay between keyword searches
- If rate limited, wait and retry
