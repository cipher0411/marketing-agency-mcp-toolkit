# MCP Tool Reference

Full status table — the canonical list is `MCP_VERIFICATION_REPORT.md` at the repo root; this is a quick-reference summary pointing back to it.

| Category | Verified tools | Setup doc |
|---|---|---|
| Lead gen | Apollo.io, Hunter.io, b2b-enrichment-mcp, Forage MCP, Instantly.ai | `mcp-configurations/leadgen-mcp-setup.md` |
| Content/creative | Social Neuron, Lamina, Canva | `mcp-configurations/content-mcp-setup.md` |
| Analytics/SEO | Google Analytics, Ahrefs, Google Sheets, HubSpot | `mcp-configurations/analytics-mcp-setup.md` |
| Advertising | Google Ads (community) | `mcp-configurations/advertising-mcp-setup.md` |
| Social | Social Neuron, Slack | `mcp-configurations/social-mcp-setup.md` |
| CRM/automation | HubSpot, Klaviyo | `mcp-configurations/analytics-mcp-setup.md`, `content-mcp-setup.md` |
| Collaboration | Notion, Slack | n/a — standard official servers |

## Excluded (not real / unverified as originally specified)
`@flipfactory-it/mcp-leadgen`, `lead-gen-toolkit`, `openrouter-media`, `ad-generator-mcp` — see `MCP_VERIFICATION_REPORT.md` for what was checked and the closest real alternatives.

## Standard for adding a new tool to this reference
1. Confirm it exists (npm/PyPI registry page or GitHub repo with real commit history).
2. Confirm the publisher (official vendor, known maintainer, or read-the-source-yourself individual project).
3. Add it to `MCP_VERIFICATION_REPORT.md` first, then mirror the summary here.
4. Only after both of those, add it to `.mcp.json`.
