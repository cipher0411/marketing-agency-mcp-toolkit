# MCP Ad Workflows (Client)

See `agency-assets/mcp-configurations/advertising-mcp-setup.md` for current tool verification status before following this workflow — the original spec's `ad-generator-mcp` doesn't exist; this workflow uses only verified tools plus manual steps.

## Copy generation
1. Fill `ad_creative_brief.md`.
2. Draft copy manually against `_context/client_brand_voice_guide.md`, or via a verified ad-copy tool once one is selected per `advertising-mcp-setup.md`.
3. Log variations in `ad_copy_variations.md`.

## Creative rendering
1. Static/display creative: Canva (`https://mcp.canva.com/mcp`) — brand templates if this client's plan includes them.
2. Video creative: evaluate Prizmad or another verified video-ad tool per `advertising-mcp-setup.md`; not pre-wired.

## Campaign setup & management
1. Google Ads MCP tools for campaign creation, keyword research, budget/bid management (`advertising-mcp-setup.md`).
2. **Every live-spend-affecting action (new campaign launch, budget change, bid strategy change) requires a human to confirm that specific action** — no exceptions for "the AI is confident."

## Performance tracking
1. Pull performance via Google Ads MCP.
2. Cross-check against GA4/HubSpot conversion data.
3. Log into `ad_performance_tracker.md`.
