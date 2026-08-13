# Lead Generation MCP Setup

Covers: Apollo.io, Hunter.io, b2b-enrichment-mcp, Forage MCP, Instantly.ai, Saleshandy, Smartlead. See [`MCP_VERIFICATION_REPORT.md`](../../MCP_VERIFICATION_REPORT.md) for what's verified.

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

## Cheaper alternatives to Instantly.ai

Both verified working end-to-end and wired into `.mcp.json`.

### Saleshandy
- ~$25/mo (Outreach Starter: 2,000 active prospects, 6,000 emails/mo), 7-day free trial (100 emails, no card required). Notably offers **unlimited clients on one plan** — relevant if you're running this for multiple client accounts, not just your own.
- **Preferred path: Saleshandy's own official Claude Connector.** Connect via claude.ai → Settings → Connectors (same mechanism as Buffer) rather than the local `.mcp.json` wrapper below. Verified live: 60+ tools covering sequences, email accounts (with health scores), enrichment, DNC lists, task management, even domain purchasing for cold-email infrastructure — far more complete than the community GitHub repo. This wasn't found during initial research because Connectors aren't indexed by npm/GitHub search the way community MCP servers are.
- **Fallback (if Connector access isn't available):** `.mcp.json`'s `saleshandy` entry runs a locally-patched version of the published repo (`ftaxats/SHMCP`), which is NOT runnable as-is — it's packaged for Smithery's cloud hosting, and its compiled output had a real bug (missing `.js` extensions on ESM imports). Both fixed; wrapper lives at `C:\Users\Tech\mcp-servers\SHMCP\stdio-entry.mjs`. Only 9 tools this way (profile, campaigns, templates, contacts) — no sequences, no lead sourcing.
- Env (fallback path only): `SALESHANDY_API_KEY`, from Saleshandy → account settings.

### Smartlead
- $39/mo (Base: 2,000 active leads, 6,000 emails/mo, unlimited mailboxes+warmup), 14-day free trial with 2,500 email credits.
- Built by LeadMagic, an official SmartLead partner — worked correctly on the first runtime test, no fixes needed.
- Env: `SMARTLEAD_API_KEY`. Optionally `SMARTLEAD_ADVANCED_TOOLS=true` / `SMARTLEAD_ADMIN_TOOLS=true` to unlock more of its 113+ tool set (49 load by default: campaigns, leads, email accounts, statistics).
- More comprehensive than Saleshandy out of the box — includes analytics, deliverability/spam testing, domain/mailbox management, webhooks.

**Either way**, cold email still needs the same groundwork regardless of tool: a connected mailbox (Google Workspace/Microsoft 365), SPF/DKIM/DMARC set up on the sending domain, and a warmup period before real volume — skipping this gets flagged as spam fast, whichever platform you use.

## What's NOT wired up
The original spec named `@flipfactory-it/mcp-leadgen` and `lead-gen-toolkit` (an Apify+Instantly bundle). Neither exists under those names. If you want a bundled scrape→enrich→campaign pipeline, evaluate Apify's `lead-gen-mcp-server` (samstorm) — $0.05/call flat, requires an Apify Starter plan ($39/mo) — and rewrite this doc against its actual current tool list before using it with a client.

## Recommended pipeline
1. `find_leads` / `search_people` (Forage or Apollo) — build the raw list.
2. `contact_enrich` / `enrich_person` — fill in emails, titles, LinkedIn.
3. `email_find` / Hunter verification — confirm deliverability before sending.
4. Export to the client's `_context` folder or Google Sheets.
5. `push_to_instantly` — load into an outreach campaign.
6. Track cost per client in `reports/mcp_analytics_workflows.md`.
