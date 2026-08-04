# MCP Credentials Management

## Rules
1. **No key ever gets committed.** Not in `.mcp.json`, not in a client's `_context/mcp_configuration.md`, not in a chat log that gets pasted into a doc. Placeholders only (`${VAR_NAME}`).
2. Real values live in environment variables, set per machine/session — or in a secrets manager if the agency has one. If you don't have one yet, at minimum use a local `.env` file that's git-ignored and never shared over Slack/email.
3. Each client gets **its own** set of keys for tools billed per-client (Apollo, Hunter, Instantly, Forage, Ahrefs seat if multi-seat). Do not reuse one agency-wide key across clients for anything that has per-account rate limits or cost attribution — you'll lose the ability to bill accurately or to revoke one client's access without breaking others.
4. Shared agency-wide keys (Slack, Notion, internal Google Sheets) are fine to reuse, but scope their permissions to only what the integration needs.
5. Rotate any key immediately if a client offboards, a contractor's engagement ends, or a key is suspected exposed.

## Required environment variables

| Variable | Service | Tier |
|---|---|---|
| `HUNTER_API_KEY` | Hunter.io | Free: 50 req/mo |
| `APOLLO_API_KEY` | Apollo.io | Free tier available |
| `APIFY_API_TOKEN` | Apify (Forage, Lead Gen MCP) | Pay-as-you-go |
| `INSTANTLY_API_KEY` | Instantly.ai | Subscription |
| `SOCIALNEURON_API_KEY` | Social Neuron | Subscription (Starter+) |
| `GOOGLE_ADS_CLIENT_ID` / `_SECRET` / `_DEVELOPER_TOKEN` / `_REFRESH_TOKEN` | Google Ads API | Free API, ad spend separate |
| `HUBSPOT_ACCESS_TOKEN` | HubSpot | Free tier available |
| `GA4_PROPERTY_ID` / `GOOGLE_APPLICATION_CREDENTIALS` | Google Analytics | Free |
| `AHREFS_API_KEY` | Ahrefs | Paid subscription only |
| `KLAVIYO_API_KEY` | Klaviyo | Subscription |
| `NOTION_TOKEN` | Notion | Free tier available |
| `SLACK_BOT_TOKEN` / `SLACK_TEAM_ID` | Slack | Free tier available |
| `GOOGLE_SERVICE_ACCOUNT_JSON` | Google Sheets | Free |

## Cost tracking (per-call and subscription tools)

| Tool | Model | Track how |
|---|---|---|
| Forage MCP | ~$0.03–$3.50 per op/skill | Log every call's cost against the client in `reports/mcp_analytics_workflows.md`; flag if a client's monthly Forage spend exceeds their retainer allowance |
| Apify actors (Lead Gen MCP, etc.) | ~$0.01–$0.05/lead or per call | Same as above |
| Ahrefs / Social Neuron / Klaviyo | Flat subscription | Confirm which clients' retainers actually include these before enabling — don't assume Agency-tier access applies to every account |

## Onboarding a new client's credentials
1. Copy `_TEMPLATE_CLIENT/_context/mcp_configuration.md`.
2. Fill in only the tools this client is actually paying for or has authorized.
3. Set that client's env vars in your credential store, named distinctly (e.g. `CLIENTNAME_APOLLO_API_KEY`) if keys are per-client.
4. Confirm with the client (or their existing tool admin) before connecting any CRM/ads/analytics account — these are their accounts, not the agency's.
