# Analytics & SEO MCP Setup

Covers: Google Analytics, Ahrefs, HubSpot (analytics side), Google Sheets.

## Google Analytics (`mcp-server-google-analytics` by ruchernchong)
- Community server, not Google-published — this is the most-adopted of several near-identical GA4 MCP servers on npm; re-check before assuming it's still the best-maintained option.
- Requires a GCP service account with GA4 Data API access, plus `GA4_PROPERTY_ID`.
- Env: `GA4_PROPERTY_ID`, `GOOGLE_APPLICATION_CREDENTIALS` (path to service account JSON).
- Use for: source attribution, landing page performance, bounce rate/engagement queries in natural language.

## Ahrefs (`@ahrefs/mcp`)
- Official package, but Ahrefs' own docs say the **local** server is unmaintained, works only with legacy API v3 keys (not MCP keys), and is outdated — they recommend the **remote** MCP instead for new setups.
- Pricing: Ahrefs subscription $129–$449/mo (this is the underlying product cost, not the MCP server itself).
- 80+ tools: keyword research, rank tracking, backlinks, Site Explorer, Brand Radar (AI brand mention tracking).
- Action: before enabling for a client, check ahrefs.com/api for the current recommended MCP setup rather than trusting this doc's snapshot.

## HubSpot analytics (`@hubspot/mcp-server`)
- Official, public beta. Source is closed (compiled JS) — treat it as a black box and review HubSpot's changelog before upgrading versions.
- Use for: email engagement data, campaign results, deal pipeline / ticket status queries.
- Env: `HUBSPOT_ACCESS_TOKEN` (private app token with the scopes your queries need — don't grant write scopes for a read-only reporting workflow).

## Google Sheets (`mcp-gsheets` by freema)
- Community server. Alternative: `google-sheets-mcp` (domdomegg).
- Use for: exporting lead lists, building live reporting dashboards clients can view directly.
- Env: `GOOGLE_SERVICE_ACCOUNT_JSON`.

## Reporting workflow
1. Pull raw metrics via GA/Ahrefs/HubSpot MCP calls.
2. Cross-reference against the client's goals in `_context/client_growth_marketing_context.md`.
3. Write findings into `reports/monthly_report_template.md` or `quarterly_report_template.md`.
4. Push raw data tables to Google Sheets for client self-serve access.
5. Log any anomalies (traffic drop, ranking loss) immediately in Slack rather than waiting for the monthly cycle — see `_global-sops/client_communication_sop.md`.
