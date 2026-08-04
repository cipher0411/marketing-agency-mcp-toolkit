# New Client Onboarding SOP

**Owner:** Account lead
**Applies to:** Every new client engagement

## Trigger
Signed contract / statement of work.

## Steps
1. Copy `clients/_TEMPLATE_CLIENT/` to `clients/<client-name>/`.
2. Kickoff call — gather brand assets, access credentials, goals. Use `_master-templates/universal_project_brief_template.md` as the intake structure.
3. Fill in `_context/` folder: brand context, style guide, voice guide, growth marketing context, product offerings.
4. Determine which MCP tools this client's retainer covers. Fill in `_context/mcp_configuration.md` accordingly — do not enable tools they're not paying for.
5. Set up client-specific API keys/env vars per `agency-assets/mcp-configurations/mcp-credentials-management.md`.
6. Connect accounts the client owns (GA4, HubSpot, Ads, Search Console) — get explicit written authorization before connecting anything, and use the access level they grant, not more.
7. Run a baseline report (`reports/monthly_report_template.md`) using current data before any work starts, so "improvement" has a real before/after.
8. Schedule recurring check-ins; add client to relevant Slack channel.
9. Deliver onboarding summary + first 30/60/90 plan to client.

## Outputs
- Populated client folder
- Baseline report
- Signed-off 30/60/90 plan

## Escalation
If the client can't/won't grant needed account access within 5 business days of kickoff, flag to account lead — don't proceed on assumptions about their data.
