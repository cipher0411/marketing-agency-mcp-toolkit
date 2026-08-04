# Advertising MCP Setup

Covers: Google Ads, and the ad-creative capability gap left by the non-existent `ad-generator-mcp`.

## Google Ads
- No single official MCP server exists. Community options: `@samihalawa/google-ads-mcp-server` (wired in `.mcp.json`), `@zleventer/google-ads-mcp` (22 tools, geared toward agency-scale diagnostics), `@martechery/mcp-google-ads-ts` (GCloud/ADC auth, MCC support for managing multiple client accounts under one login).
- If you manage several client ad accounts, `@martechery/mcp-google-ads-ts`'s MCC support is worth evaluating over the single-account default — re-verify its current state before switching.
- Env: `GOOGLE_ADS_CLIENT_ID`, `GOOGLE_ADS_CLIENT_SECRET`, `GOOGLE_ADS_DEVELOPER_TOKEN`, `GOOGLE_ADS_REFRESH_TOKEN`.
- **Caution:** these tools can pause campaigns and change budgets. Never grant an MCP server write scope on a live client account without a human confirming each budget/bid change — treat AI-suggested spend changes the same as any other high-blast-radius action.

## Ad creative generation — capability gap
`ad-generator-mcp` (generate_copy, render_ad, bulk_generate, upload_asset) does not exist under that name or tool set. Real alternatives, none verified against the original spec's exact workflow:
- **Prizmad MCP** (`prizmad/Prizmad-MCP-server`) — AI UGC video ads from a product URL, 50+ avatars, ElevenLabs voiceover.
- **ads-mcp** (`amekala/ads-mcp`) — 100+ tools spanning Google/Meta/LinkedIn/TikTok Ads, campaign creation + copy + keyword research + budget optimization.
- **meta-ads-mcp-server** — Meta-specific, npm package.

Before a client engagement depends on automated ad-copy generation or rendering, pick one of these, read its current README, and rewrite `ads/mcp_ad_workflows.md` for that specific client against the real tool names — don't assume the generic workflow in this template matches whichever tool you pick.

## Manual fallback
Until an ad-creative MCP is chosen and verified, ad copy and creative come from Canva (`content-mcp-setup.md`) plus manual copywriting against `ads/ad_copy_variations.md`. This is the safe default — slower, but doesn't depend on an unverified tool.
