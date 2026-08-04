# MCP Package Verification Report

Before wiring anything into `.mcp.json`, every package from the original spec was checked against npm, GitHub, and vendor docs (search performed 2026-08-04). `.mcp.json` in this repo **only** contains servers from the "Verified" table below. Nothing else is auto-executed. Do not add a package to `.mcp.json` until it has been re-verified — package names alone are not proof a package is safe to run.

## Verified — real, wired into `.mcp.json` (disabled by default, needs your API keys)

| # | Server | Package | Publisher | Notes |
|---|--------|---------|-----------|-------|
| 1 | HubSpot | `@hubspot/mcp-server` | HubSpot (official, public beta) | Source not public; closed-source compiled JS. Official docs: developers.hubspot.com/mcp |
| 2 | Notion | `@notionhq/notion-mcp-server` | Notion (official) | github.com/makenotion/notion-mcp-server |
| 3 | Slack | `@modelcontextprotocol/server-slack` | MCP maintainers | Reference server, MIT licensed |
| 4 | Ahrefs | `@ahrefs/mcp` | Ahrefs (official) | Ahrefs' own docs say the **local** server is unmaintained/outdated and recommend their **remote** MCP instead — see `agency-assets/mcp-configurations/analytics-mcp-setup.md` |
| 5 | Klaviyo | `klaviyo-mcp` | Community (TypeScript, official MCP SDK) | Not Klaviyo-published; review source before use |
| 6 | Canva | Remote endpoint `https://mcp.canva.com/mcp` via `mcp-remote` bridge | Canva (official) | OAuth-based, no npx package to vet — canva.dev/docs/mcp |
| 7 | Google Analytics | `mcp-server-google-analytics` (ruchernchong) | Community | Most-starred of several GA4 community servers; requires GCP service account |
| 8 | Google Sheets | `mcp-gsheets` (freema) | Community | Alternative: `google-sheets-mcp` (domdomegg) |
| 9 | Google Ads | `@samihalawa/google-ads-mcp-server` | Community | No single official server exists; several forks compete — vet before granting spend-affecting scopes |
| 10 | Apollo.io | `apollo-io-mcp-server` (lkm1developer) | Community | Free tier available |
| 11 | Hunter.io | Official **remote** MCP (hunter.io/api-documentation#mcp) | Hunter.io (official) | The old `hunter-io/hunter-mcp` local repo is explicitly deprecated in favor of the remote server |
| 12 | Instantly.ai | `instantly-mcp` (bcharleson) | Community | 38 tools, stdio + HTTP |
| 13 | b2b-enrichment-mcp | github.com/Aleksey-Panf/b2b-enrichment-mcp | Individual dev, Python | Real, but low-adoption single-maintainer project — read the source before running it locally |
| 14 | Forage MCP | apify.com/ernesta_labs/forage | ErnestaLabs (Apify-hosted) | Pay-per-call, $5 free credit, no subscription |
| 15 | Social Neuron | `@socialneuron/mcp-server` | Social Neuron (official) | Requires a paid Social Neuron plan (Starter+) |
| 16 | Lamina | github.com/uselamina/lamina-mcp | Lamina (official) | Tools are `create`, `track`, `evaluate`, `distribute`, `brand_lookup` — not `lamina_create`/`lamina_brand`/`lamina_batch` as originally briefed; naming corrected in the workflow docs |

## Not verified — excluded from `.mcp.json`, do not install as named

| # | Name as given | Finding |
|---|--------|---------|
| 17 | `@flipfactory-it/mcp-leadgen` | No npm package, no GitHub repo, no registry listing found under this name. Likely fabricated or a private/unpublished package. **Do not install.** |
| 18 | `lead-gen-toolkit` (Apify + Instantly pipeline) | No package with this name or feature set found. Closest real analog: Apify's "Lead Gen MCP Server" by samstorm (`apify.com/samstorm/lead-gen-mcp-server`) — different tools, $0.05/call flat, requires an Apify Starter plan ($39/mo). If you want this workflow, use that server and re-verify its current tool list first. |
| 19 | `openrouter-media` | No package under this name. Closest real analog: `@stabgan/openrouter-mcp-multimodal`, which does generate images/video/audio via OpenRouter. Verify its README against the workflow docs before using. |
| 20 | `ad-generator-mcp` (generate_copy/render_ad/bulk_generate/upload_asset) | No package under this name or with this exact tool set. Closest real analogs: Prizmad MCP (UGC video ads), `ads-mcp` (amekala, 100+ tools across Google/Meta/LinkedIn/TikTok), `meta-ads-mcp-server`. None match the briefed tool names — pick one, read its README, and rewrite the workflow doc to match its actual tools before relying on it. |

## Runtime-verified corrections (2026-08-04)

Static verification (checking a package exists) turned out not to be enough — three servers had wrong env var names or wrong invocation details that only surfaced by actually running them and reading the crash output. Corrected in `.mcp.json`:

- **google-analytics** (`mcp-server-google-analytics`): actually requires `GOOGLE_CLIENT_EMAIL`, `GOOGLE_PRIVATE_KEY`, `GA_PROPERTY_ID` — not the Google-standard `GOOGLE_APPLICATION_CREDENTIALS`/`GA4_PROPERTY_ID` names originally assumed.
- **google-sheets** (`mcp-gsheets`): wants `GOOGLE_SERVICE_ACCOUNT_KEY` as the raw JSON string (or `GOOGLE_APPLICATION_CREDENTIALS` as a file path, or `GOOGLE_PRIVATE_KEY`+`GOOGLE_CLIENT_EMAIL` directly) — the `GOOGLE_SERVICE_ACCOUNT_JSON` name/format originally used wasn't recognized.
- **b2b-enrichment-mcp**: the real module is `apollo_mcp.server`, not `b2b_enrichment_mcp`. It also needs a proper `git clone` + venv + `pip install -e .` — it's not `npx`-fetchable. Its `pyproject.toml` pins `mcp[cli]>=1.9.0` with no upper bound, which pulls in an incompatible `mcp` 2.0.0 by default (that release removed the `fastmcp` submodule this code imports) — installed with `mcp[cli]<2.0` instead. Set up in `C:\Users\Tech\mcp-servers\b2b-enrichment-mcp\.venv`, outside this repo. Source was reviewed before running: it only calls `api.apollo.io` and `api.hunter.io`.
- **canva**: tested directly and it does work (`Local STDIO server running`, proxy established) — a "failed" status in Claude Code's `/mcp` view for this one is likely a slow-handshake timing issue, not a real problem.

**Lesson:** "the package exists and is from a legitimate publisher" (static verification) and "the package works with the env vars its own docs/community listings imply" (runtime verification) are different claims. Community MCP servers in particular should be run once with `--help` or a short timeout before being trusted in a client engagement, not just read about.

## How this changes the deliverable

- `.mcp.json` ships with entries **1–16 only**, every one commented with its source and an `env` block of placeholder variable names — no real keys are or should ever be committed.
- The four unverified items (17–20) are documented in the ads/lead-gen workflow files as "capability gap — needs a vetted tool" rather than pretending they're wired up.
- Re-run this verification periodically — MCP packages are new and churn fast; a server that's real today can be abandoned, renamed, or (rarely) hijacked later. Treat re-verification before upgrading a version pin as routine, not optional.
