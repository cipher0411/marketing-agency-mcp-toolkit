# MCP Analytics Workflows (Client)

See `agency-assets/mcp-configurations/analytics-mcp-setup.md` for current verification status of each tool.

## Data pull workflow
1. GA4 (`mcp-server-google-analytics`): traffic, source attribution, landing page performance, engagement.
2. Ahrefs (`@ahrefs/mcp` — check current recommended setup, local package is flagged unmaintained by Ahrefs themselves): keyword rankings, backlinks, Brand Radar mentions.
3. HubSpot (`@hubspot/mcp-server`): CRM pipeline, email engagement, deal/ticket status.
4. Social Neuron: social performance, `get_performance_insights`.
5. Google Ads: spend, CPA, ROAS.

## Cross-checking
Before writing numbers into any report, reconcile: does GA4 traffic roughly match what Google Ads reports as clicks (accounting for attribution window differences)? Does HubSpot's lead count roughly match landing page form submissions? A mismatch usually means a tracking gap, not a real anomaly — investigate before reporting either as fact.

## Cost logging (for pay-per-call tools used in analysis, e.g. Forage lookups during research)
| Date | Tool | Calls | Cost | Purpose | Billed to client? |
|---|---|---|---|---|---|

## Output
Feeds `monthly_report_template.md`, `quarterly_report_template.md`, and the live dashboard per `analytics_dashboard_guide.md`.
