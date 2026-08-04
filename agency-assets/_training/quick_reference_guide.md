# Quick Reference Guide

## "Where do I find..."
| Need | Location |
|---|---|
| A client's brand voice | `clients/<client>/_context/client_brand_voice_guide.md` |
| Which MCP tools a client has | `clients/<client>/_context/mcp_configuration.md` |
| How to set up a specific MCP server | `agency-assets/mcp-configurations/` |
| Whether a tool is actually real/verified | `MCP_VERIFICATION_REPORT.md` |
| A content template | `clients/<client>/_templates/` |
| SOP for a specific process | `clients/<client>/_sop/` (client-specific) or `agency-assets/_global-sops/` (agency-wide) |
| API key policy | `agency-assets/mcp-configurations/mcp-credentials-management.md` |

## "Who do I ask..."
- Brand/voice question → account lead for that client
- Tool access/credentials → whoever administers `.mcp.json`
- Scope/budget question → account lead
- Security concern → immediately, per `mcp_security_sop.md`

## Golden rules
1. Never send/publish/spend without explicit confirmation on that specific action.
2. Never hardcode a credential anywhere.
3. Never assume an MCP package name from a list is real — verify first.
4. When in doubt, it goes through QA before a client sees it.
