# Automation Workflows

Cross-references to the per-function MCP workflow docs, plus general automation principles.

## Where the workflows live
- Lead gen: `agency-assets/mcp-configurations/leadgen-mcp-setup.md` (recommended pipeline section)
- Content: `agency-assets/mcp-configurations/content-mcp-setup.md` (recommended pipeline section)
- Social: `clients/_TEMPLATE_CLIENT/social/mcp_social_workflows.md`
- SEO: `clients/_TEMPLATE_CLIENT/seo/mcp_seo_workflows.md`
- Ads: `clients/_TEMPLATE_CLIENT/ads/mcp_ad_workflows.md`
- Analytics/reporting: `clients/_TEMPLATE_CLIENT/reports/mcp_analytics_workflows.md`

## Principles for any automated workflow in this system
1. **Human-in-the-loop for irreversible actions.** Publishing, sending, spending budget — always a confirmed action, never fully autonomous, regardless of how routine it becomes.
2. **Cost visibility.** Any workflow using a pay-per-call tool (Forage, Apify actors) logs its cost against the client it ran for.
3. **Idempotency where possible.** Re-running a lead enrichment or report-generation step shouldn't duplicate data — check for existing records before writing new ones.
4. **Fail loud, not silent.** If an MCP call fails (bad key, rate limit, service down), surface that immediately rather than silently skipping the step.
