# Social Media MCP Setup

Covers: Social Neuron (primary), Slack (internal coordination), Canva (asset creation).

## Social Neuron
- See `content-mcp-setup.md` for the full tool list. For social specifically: `schedule_post`, `schedule_content_plan`, `fetch_analytics`, `get_performance_insights`.
- Platforms supported: YouTube, Instagram, TikTok per the official repo — confirm current platform coverage before promising a client a channel it may not support yet (e.g. LinkedIn, X).

## Slack (`@modelcontextprotocol/server-slack`)
- Official MCP reference server, MIT licensed.
- Env: `SLACK_BOT_TOKEN`, `SLACK_TEAM_ID`, optionally `SLACK_CHANNEL_IDS` to scope which channels are visible.
- Use for: posting automated performance alerts to a client or internal channel, searching past campaign discussion threads.
- Scope the bot token to only the channels this integration needs — don't grant workspace-wide access for a single client's automation.

## Posting workflow
1. Draft content using `content-mcp-setup.md` pipeline.
2. Run `quality_check` before scheduling anything (see `_sop/content_creation_sop.md`).
3. `schedule_post` / `schedule_content_plan` via Social Neuron.
4. Post a Slack summary of what went live to the client channel.
5. Pull `fetch_analytics` weekly, log into `social/social_analytics_tracker.md`.

## Rate limits & caching
Cache `fetch_trends` and `fetch_analytics` results locally (e.g. in the client's `reports/` folder) rather than re-querying on every session — most platforms rate-limit aggressively and repeated identical queries burn quota for no new information.
