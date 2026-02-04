---
name: reddit-reader
description: Fetch trending posts from Reddit subreddits. USE WHEN user says 'reddit news', 'reddit posts', 'check reddit', 'subreddit updates'.
---

# Reddit Reader

Fetches and displays trending posts from configured subreddits.

## Configuration
!`coreai config show reddit-reader`

## Instructions

1. **Fetch posts** from each subreddit in the configuration
2. **Filter by time** using the `hours` setting
3. **Sort by score** (upvotes)
4. **Format output** according to `output.format`

### API Details

- Endpoint: `https://www.reddit.com/r/{subreddit}/hot.json?limit={limit}`
- No authentication required
- Rate limit: ~60 requests/minute (be conservative)

### Implementation

For each subreddit, fetch JSON:
curl -A "{user_agent}" "https://www.reddit.com/r/{subreddit}/hot.json?limit={limit}"

### Output Format

Return markdown list of posts:

## Reddit - Last {hours} hours

### r/MachineLearning
- [Post Title](url) - 523 pts
  > First 200 chars of self text...

### r/LocalLLaMA
- [Post Title](url) - 234 pts

### Error Handling

- If a subreddit returns 404, log warning and continue
- If rate limited (429), wait and retry once
- Return partial results if some subreddits fail
