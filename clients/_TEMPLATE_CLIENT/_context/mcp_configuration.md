# Client MCP Configuration

**Do not put real API keys in this file.** Use this to track *which* tools this client has authorized and which env var names hold their keys elsewhere (secrets manager / local `.env`, git-ignored).

## Enabled for this client
| Tool | Enabled? | Env var name(s) | Billing tier | Notes |
|---|---|---|---|---|
| Apollo.io | | | | |
| Hunter.io | | | | |
| Forage MCP | | | | Pay-per-call — track spend |
| Instantly.ai | | | | |
| Social Neuron | | | | Confirm plan tier |
| Lamina | | | | |
| Canva | | | | OAuth, no static key |
| HubSpot | | | | |
| Google Ads | | | | Confirm write-scope approval |
| Google Analytics | | | | |
| Google Sheets | | | | |
| Ahrefs | | | | Agency subscription — confirm client's retainer covers it |
| Klaviyo | | | | |
| Notion | | | | |
| Slack | | | | Which channel(s) |

## Explicitly NOT enabled
List tools this client hasn't authorized, so nobody accidentally uses agency-wide credentials on their behalf.

## Authorization record
- Who at the client authorized each connected account, and date:
- Scope granted (read-only vs. write):
