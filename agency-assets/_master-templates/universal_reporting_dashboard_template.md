# Universal Reporting Dashboard Template

Structure for any client-facing dashboard (Google Sheets export or live doc), so clients get a consistent experience across accounts.

## Section 1: Executive summary
- 3–5 bullet takeaways, plain language, no jargon
- Overall status: on track / at risk / off track, with one-line why

## Section 2: Core KPIs (pick the ones relevant to this client's goals)
| Metric | This period | Last period | Change | Target |
|---|---|---|---|---|
| Website sessions | | | | |
| Leads generated | | | | |
| Cost per lead | | | | |
| Conversion rate | | | | |
| Organic keyword rankings (top 10) | | | | |
| Email open/click rate | | | | |
| Social engagement rate | | | | |
| Ad spend / ROAS | | | | |

## Section 3: Channel breakdown
- Organic / paid / social / email / referral — each with a 2-line summary

## Section 4: What we did this period
- Content shipped, campaigns launched, tests run

## Section 5: What's next
- Planned work for next period, tied back to the client's stated goals in `client_growth_marketing_context.md`

## Data sourcing notes
Pull metrics via the relevant MCP servers (`agency-assets/mcp-configurations/analytics-mcp-setup.md`) — GA4 for traffic, Ahrefs for SEO, HubSpot for CRM/email, Social Neuron for social. Cross-check numbers between tools before presenting; discrepancies usually mean a tracking or attribution-window mismatch, not real change.
