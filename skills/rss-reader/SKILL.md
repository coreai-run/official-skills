---
name: rss-reader
description: Fetch articles from RSS feeds. USE WHEN user says 'rss', 'feeds', 'blog updates', 'news feeds'.
---

# RSS Reader

Fetches and displays articles from configured RSS/Atom feeds.

## Configuration
!`coreai config show rss-reader`

## Instructions

1. **Fetch feeds** from each URL in the configuration
2. **Parse RSS/Atom** format (handle both)
3. **Filter by pubDate** using the `hours` setting
4. **Sort by date** (newest first)
5. **Format output** with title, link, and description snippet

### Implementation

Parse RSS XML:
- Look for `<item>` elements (RSS 2.0) or `<entry>` elements (Atom)
- Extract: `<title>`, `<link>`, `<pubDate>` or `<published>`, `<description>` or `<summary>`

### Output Format

## RSS Feeds - Last {hours} hours

### Feed Name
- [Article Title](url) - 2h ago
  > Description snippet...

### Error Handling

- Skip feeds that return non-2xx status
- Skip items without valid pubDate
- Handle CDATA sections in content
