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
| `INSTANTLY_API_KEY` | Instantly.ai — passed as a `--api-key` CLI arg in `.mcp.json`, NOT read as an env var by the package itself; still set the env var so the arg substitution has a value | Subscription |
| `SOCIALNEURON_API_KEY` | Social Neuron — generate from the web dashboard (Developers → API Keys), not via the CLI's `login` command (broken as of v2.0.1/1.9.0) | Subscription (Starter+), Pro Trial does NOT include API access |
| `GOOGLE_ADS_CLIENT_ID` / `_SECRET` / `_DEVELOPER_TOKEN` / `_REFRESH_TOKEN` / `_CUSTOMER_ID` / `_LOGIN_CUSTOMER_ID` (optional) | Google Ads API | Free API, ad spend separate. Developer token requires a Manager (MCC) account, not a standard Ads account |
| `HUBSPOT_ACCESS_TOKEN` | HubSpot | Free tier available |
| `GOOGLE_CLIENT_EMAIL` / `GOOGLE_PRIVATE_KEY` / `GA_PROPERTY_ID` | Google Analytics — exact names required by `mcp-server-google-analytics`, not the Google-standard `GOOGLE_APPLICATION_CREDENTIALS`/`GA4_PROPERTY_ID` | Free |
| `AHREFS_API_KEY` | Ahrefs | Paid subscription only |
| `KLAVIYO_API_KEY` | Klaviyo | Subscription |
| `BREVO_MCP_TOKEN` | Brevo — free-tier alternative to Klaviyo. Generate at Account → SMTP & API → API Keys → enable "MCP option" | Free: ~300 emails/day, unlimited contacts (verify current limits) |
| `NOTION_TOKEN` | Notion | Free tier available |
| `SLACK_BOT_TOKEN` / `SLACK_TEAM_ID` | Slack | Free tier available |
| `GOOGLE_SERVICE_ACCOUNT_KEY` | Google Sheets — raw JSON string required by `mcp-gsheets`, not a file path | Free |

## Cost tracking (per-call and subscription tools)

| Tool | Model | Track how |
|---|---|---|
| Forage MCP | ~$0.03–$3.50 per op/skill | Log every call's cost against the client in `reports/mcp_analytics_workflows.md`; flag if a client's monthly Forage spend exceeds their retainer allowance |
| Apify actors (Lead Gen MCP, etc.) | ~$0.01–$0.05/lead or per call | Same as above |
| Ahrefs / Social Neuron / Klaviyo | Flat subscription | Confirm which clients' retainers actually include these before enabling — don't assume Agency-tier access applies to every account |
| Brevo | Free tier (~300 emails/day) | Free-tier alternative to Klaviyo for clients whose retainer doesn't cover a paid ESP — track if/when they outgrow the free sending limit |

## Onboarding a new client's credentials
1. Copy `_TEMPLATE_CLIENT/_context/mcp_configuration.md`.
2. Fill in only the tools this client is actually paying for or has authorized.
3. Set that client's env vars in your credential store, named distinctly (e.g. `CLIENTNAME_APOLLO_API_KEY`) if keys are per-client.
4. Confirm with the client (or their existing tool admin) before connecting any CRM/ads/analytics account — these are their accounts, not the agency's.
