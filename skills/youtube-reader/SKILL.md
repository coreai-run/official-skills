---
name: youtube-reader
description: Fetch recent videos from YouTube channels. USE WHEN user says 'youtube updates', 'new videos', 'channel videos'.
---

# YouTube Reader

Fetches recent videos from configured YouTube channels.

## Configuration
!`coreai config show youtube-reader`

## Before Proceeding

Verify the configuration above:
- If `api_key` shows `${YOUTUBE_API_KEY}`, set the environment variable
- If any channel shows `REQUIRED`, configure channels in your profile

## Instructions

1. **Verify API key** is available
2. **Fetch videos** from each channel
3. **Filter by publishedAfter** within `hours`
4. **Sort by date** (newest first)

### API Details

- Endpoint: `https://www.googleapis.com/youtube/v3/search`
- Parameters: `part=snippet`, `channelId`, `order=date`, `maxResults`, `type=video`, `publishedAfter`, `key`
- Requires API key (quota: 10,000 units/day)

### Example

curl "https://www.googleapis.com/youtube/v3/search?part=snippet&channelId=UC...&order=date&maxResults=5&type=video&publishedAfter=2024-01-20T00:00:00Z&key={api_key}"

### Output Format

## YouTube - Last {hours} hours

### Channel Name
- [Video Title](https://youtube.com/watch?v=...) - 2h ago
  > Video description snippet...

### Error Handling

- If API key missing, report error and skip
- If quota exceeded, report and skip
- Continue with other channels if one fails
