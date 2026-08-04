# Lead Generation MCP Setup

Covers: Apollo.io, Hunter.io, b2b-enrichment-mcp, Forage MCP, Instantly.ai. See [`MCP_VERIFICATION_REPORT.md`](../../MCP_VERIFICATION_REPORT.md) for what's verified.

## Apollo.io (`apollo-io-mcp-server`)
- Free tier: unlimited company enrichment, limited people credits.
- Env: `APOLLO_API_KEY` from apollo.io → Settings → API.
- Use for: company enrichment, `search_people` (no credits), `enrich_person` (1 credit).

## Hunter.io (official remote MCP)
- Free tier: 50 requests/month.
- Setup: hunter.io/api-documentation#mcp — this is a hosted/remote server, not an npx package. The old local `hunter-io/hunter-mcp` repo is deprecated; don't install it.
- Use for: email pattern verification, domain search.

## b2b-enrichment-mcp (Aleksey-Panf, GitHub, Python)
- Single-maintainer project — read the source (`github.com/Aleksey-Panf/b2b-enrichment-mcp`) before running.
- Requires Python 3.11+, local execution.
- Wraps Hunter.io + Apollo.io under one interface (`enrich_person_by_email`, `bulk_enrich_people`, `enrich_person`).
- Env: `HUNTER_API_KEY`, `APOLLO_API_KEY`.

## Forage MCP (Apify-hosted, ErnestaLabs)
- Pay-per-call, no subscription. $5 free credit for new accounts.
- Approx pricing: `search_web` $0.03, `scrape_page` $0.07, `get_company_info` $0.08, `find_emails` $0.10, `find_leads` $0.25/100.
- Skills: `company_dossier` ($0.50), `prospect_company` ($0.75), `outbound_list` ($3.50/100), `competitor_intel` ($0.80).
- Not wired into `.mcp.json` by default (usage-billed) — enable per client and track spend against their retainer. See `mcp-credentials-management.md`.
- Setup: apify.com/ernesta_labs/forage — requires an Apify API token.

## Instantly.ai (`instantly-mcp` by bcharleson)
- 38 tools across accounts, campaigns, leads, emails, analytics, background_jobs.
- Env: `INSTANTLY_API_KEY`.
- Use for: pushing enriched leads into cold email campaigns, pulling campaign performance.

## What's NOT wired up
The original spec named `@flipfactory-it/mcp-leadgen` and `lead-gen-toolkit` (an Apify+Instantly bundle). Neither exists under those names. If you want a bundled scrape→enrich→campaign pipeline, evaluate Apify's `lead-gen-mcp-server` (samstorm) — $0.05/call flat, requires an Apify Starter plan ($39/mo) — and rewrite this doc against its actual current tool list before using it with a client.

## Recommended pipeline
1. `find_leads` / `search_people` (Forage or Apollo) — build the raw list.
2. `contact_enrich` / `enrich_person` — fill in emails, titles, LinkedIn.
3. `email_find` / Hunter verification — confirm deliverability before sending.
4. Export to the client's `_context` folder or Google Sheets.
5. `push_to_instantly` — load into an outreach campaign.
6. Track cost per client in `reports/mcp_analytics_workflows.md`.
