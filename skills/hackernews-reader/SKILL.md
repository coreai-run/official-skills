---
name: hackernews-reader
description: Fetch stories from Hacker News. USE WHEN user says 'hacker news', 'HN', 'hn news', 'tech news'.
---

# Hacker News Reader

Fetches trending stories from Hacker News via the Algolia API.

## Configuration
!`coreai config show hackernews-reader`

## Instructions

1. **Search stories** for each term in `search_terms`
2. **Filter by time** using `numericFilters=created_at_i>{timestamp}`
3. **Filter by points** using `min_points`
4. **Deduplicate** across search terms by objectID
5. **Sort by points** (highest first)

### API Details

- Endpoint: `https://hn.algolia.com/api/v1/search_by_date`
- Parameters: `query`, `tags=story`, `hitsPerPage`, `numericFilters`
- No authentication required

### Example Query

curl "https://hn.algolia.com/api/v1/search_by_date?query=AI&tags=story&hitsPerPage=20&numericFilters=created_at_i>1706900000"

### Output Format

## Hacker News - Last {hours} hours

- [Story Title](url) - 234 pts, 45 comments
- [Story Title](url) - 189 pts, 23 comments

### Notes

- `story_url` may be null for "Ask HN" posts; use HN link instead
- Deduplicate results across search terms
