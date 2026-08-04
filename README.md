# Marketing Agency System

A multi-client agency operating structure: per-client folders, reusable SOPs/templates, and MCP-server-backed workflows for lead generation, content creation, advertising, and analytics.

## Start here

1. Read [`MCP_VERIFICATION_REPORT.md`](MCP_VERIFICATION_REPORT.md) — which MCP servers in this system are real and verified vs. unverified/hallucinated, and why. Do this before enabling anything.
2. Copy `clients/_TEMPLATE_CLIENT/` to `clients/<client-name>/` for each new client. Never edit the template in place once clients exist — it's the source of truth for onboarding new accounts.
3. Fill in `_context/mcp_configuration.md` for the client with which MCP tools they're actually licensed/paying for. Not every client needs every tool.
4. Set required environment variables (see `.mcp.json` and `agency-assets/mcp-configurations/mcp-credentials-management.md`) before enabling a server for that client's work.

## Folder map

```
marketing-agency/
├── .mcp.json                        # Verified MCP servers only (env vars are placeholders)
├── MCP_VERIFICATION_REPORT.md       # What's real, what's not, and why
├── clients/
│   └── _TEMPLATE_CLIENT/            # Copy this per client — do not edit in place
│       ├── _context/                # Brand, voice, product, MCP config for this client
│       ├── _sop/                    # Client-specific process docs
│       ├── _templates/              # Content templates (blog, case study, etc.)
│       ├── ads/                     # Ad copy, creative briefs, MCP ad workflows
│       ├── pages/                   # Website page blueprints
│       ├── presentations/           # Sales decks, board reports, workshops
│       ├── reports/                 # Monthly/quarterly reporting + analytics workflows
│       ├── research/                # Market/competitor research, lead research
│       ├── seo/                     # SEO strategy + MCP SEO workflows
│       └── social/                  # Social strategy, calendar, MCP social workflows
└── agency-assets/
    ├── mcp-configurations/          # Setup guides per MCP category
    ├── _master-templates/           # Cross-client universal templates
    ├── _global-sops/                # Agency-wide process (onboarding, QA, security, crisis)
    ├── _brand-assets/               # The agency's own brand (not a client's)
    ├── _tools/                      # Tool stack reference and automation notes
    └── _training/                   # New hire onboarding and reference material
```

## Cost model (see `agency-assets/mcp-configurations/mcp-credentials-management.md` for full detail)

| Tier | Tools | Notes |
|------|-------|-------|
| Free / near-free | Apollo.io (free tier), Google Sheets, Hunter.io (50 free/mo) | Good default for early-stage or low-volume clients |
| Pay-per-call | Forage MCP (~$0.03–$0.75/op) | Track spend per client — see cost tracking template |
| Subscription | Ahrefs ($129+/mo), Social Neuron ($49+/mo), Klaviyo | Only enable per-client if the retainer covers it |
| Volume-based | Apollo/Apify-style lead sourcing, Instantly sending limits | Watch for per-client caps, not just agency-wide caps |

## Security

- API keys live in environment variables only — never hardcoded in `.mcp.json`, client docs, or committed anywhere. See `agency-assets/_global-sops/mcp_security_sop.md`.
- Each client's MCP config is isolated (`_context/mcp_configuration.md` per client) so a leaked key or a scope mistake can't cross client accounts.
- Before adding any new MCP package to `.mcp.json`, re-verify it the way `MCP_VERIFICATION_REPORT.md` was built: check it actually exists on npm/GitHub, check the publisher, check current maintenance status. AI-generated tool lists (including the one this system started from) can include names that don't exist.
