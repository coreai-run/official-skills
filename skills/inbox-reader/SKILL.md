---
name: inbox-reader
description: Fetch news from Gmail alerts and newsletters. USE WHEN user says 'email news', 'inbox', 'newsletters', 'alerts'.
---

# Inbox Reader

Fetches news items from Gmail labels (Google Alerts, newsletters).

## Configuration
!`coreai config show inbox-reader`

## Prerequisites

This skill requires Gmail OAuth authentication:
1. Configure credentials in `~/.core/studio/.env`
2. Run initial auth flow via studio tools

## Instructions

1. **Connect to Gmail** using OAuth credentials
2. **Fetch emails** from configured labels
3. **Parse content** based on source type:
   - `google_alert`: Extract linked articles
   - `newsletter`: Extract article sections
4. **Filter spam** using `spam_patterns`
5. **Format output** grouped by source

### Gmail Label Sources

| Type | Parsing Method |
|------|----------------|
| `google_alert` | Extract URLs and titles from alert emails |
| `newsletter` | Parse newsletter sections for articles |

### Output Format

## Gmail News - Last {days} days

### Google Alerts
- [Article Title](url) - Source Name
- [Article Title](url) - Source Name

### Newsletters
- [Article Title](url) - Newsletter Name

### Spam Filtering

Items matching `spam_patterns` are filtered out:
- Referral/affiliate content
- "Earn $X" promotions
- Friend invite requests

### Error Handling

- If Gmail auth fails, report error with setup instructions
- Skip sources that fail, continue with others
