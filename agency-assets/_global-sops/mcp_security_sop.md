# MCP Security SOP

**Owner:** Whoever administers `.mcp.json` and credential storage
**Applies to:** Every MCP server used anywhere in this agency's work

## Before adding any MCP server
1. Verify it actually exists — check npm/PyPI and GitHub directly, don't trust a name from a list (including AI-generated lists — see `MCP_VERIFICATION_REPORT.md` for why this matters; four of the seventeen originally requested packages turned out to not exist).
2. Check the publisher: official vendor package > well-known maintainer > small individual project > unknown/unverifiable.
3. For small/individual projects, read the source before running it locally — it executes with your credentials' permissions.
4. Confirm what scopes/permissions it actually needs and don't grant more (e.g. a reporting-only GA4 integration doesn't need write access to anything).

## Credential handling
See `mcp-configurations/mcp-credentials-management.md` for the full policy. Summary: env vars only, per-client isolation for billed/rate-limited tools, immediate rotation on offboarding or suspected exposure.

## Ongoing
- Re-verify a server's maintenance status before bumping its pinned version — abandoned projects and supply-chain compromise both show up as "the same name, different content."
- Any server that can take an irreversible action (send email, publish a post, spend ad budget, delete data) requires human confirmation for each specific action — this is not something an SOP or agent instruction should override, and no client urgency justifies skipping it.
- Log which client engagements use which MCP servers (`_context/mcp_configuration.md` per client) so a compromised/deprecated server's blast radius is knowable at a glance.

## Incident response
If a key is exposed or a server behaves unexpectedly (calls endpoints it shouldn't, requests scopes beyond its stated purpose): disable it in `.mcp.json` immediately, rotate the associated credential, and follow `crisis_communication_sop.md` if any client data was potentially affected.
