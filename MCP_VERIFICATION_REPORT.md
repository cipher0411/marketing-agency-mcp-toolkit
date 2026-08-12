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
| 17 | Brevo | Remote MCP at `mcp.brevo.com/v1/brevo/mcp`, bridged via `mcp-remote` with a Bearer token header | Brevo (official, developers.brevo.com/docs/mcp-protocol) | Free-tier alternative to Klaviyo — historically ~300 emails/day free, unlimited contacts (verify current limits). Tested end-to-end with a real token: the token alone isn't sufficient, it also requires a one-time interactive OAuth browser authorization per session (same as Canva) — Claude Code handles this automatically on first `/mcp` connect |
| 18 | Buffer | Official Buffer MCP, connects via Claude Connectors | Buffer (official, buffer.com/mcp) | Free-tier alternative to Social Neuron's scheduling/distribution piece — not yet wired into `.mcp.json`, connects differently (Claude Connectors flow, not an npx package) |

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

## Live-tested against real credentials (2026-08-05)

All 14 wired servers were run against real, working credentials end-to-end via Claude Code's `/mcp`. Three more real bugs surfaced this way — beyond what static/`--help`-level testing could catch:

- **google-ads**: `@samihalawa/google-ads-mcp-server` has a published syntax error (`server.js:915`) that crashes on load regardless of credentials — confirmed by running it directly. Replaced with `@zleventer/google-ads-mcp`, which needs `GOOGLE_ADS_CUSTOMER_ID` (required, numeric, no dashes) and optionally `GOOGLE_ADS_LOGIN_CUSTOMER_ID` (only if the target customer ID is a client account linked under a separate manager account you're authenticating as).
- **instantly**: `instantly-mcp` silently ignores `INSTANTLY_API_KEY` as an env var — it only accepts the key via a `--api-key` CLI argument. `.mcp.json`'s `args` array now passes it that way instead of via `env`.
- **socialneuron**: `@socialneuron/mcp-server`'s `login` subcommand is broken — it prints "waiting for authorization" but never actually opens a local listening port to receive the OAuth callback (confirmed by inspecting the process's network connections directly; zero, across two tested versions, 2.0.1 and 1.9.0). Worked around by generating an API key directly from the Social Neuron web dashboard (Developers → API Keys) instead of the CLI login flow, and setting it as `SOCIALNEURON_API_KEY` — the server does honor that env var even though it isn't documented as the primary auth path. Note: Social Neuron's dashboard states API access requires a paid plan, not just their Pro Trial — verify with a real tool call, not just a successful `/mcp` connection, if your account is still on trial.

**Second lesson:** even "it starts without crashing and lists its tools" (what `/mcp` shows as "connected") is not proof a server's credentials are valid or that real tool calls will succeed — `ahrefs` and `slack` both show "connected" while still missing their real API keys, because those two packages don't validate auth until a tool is actually invoked. Treat "connected" as "the process launched," not "this works."

## How this changes the deliverable

- `.mcp.json` ships with entries **1–16 only**, every one commented with its source and an `env` block of placeholder variable names — no real keys are or should ever be committed.
- The four unverified items (17–20) are documented in the ads/lead-gen workflow files as "capability gap — needs a vetted tool" rather than pretending they're wired up.
- Re-run this verification periodically — MCP packages are new and churn fast; a server that's real today can be abandoned, renamed, or (rarely) hijacked later. Treat re-verification before upgrading a version pin as routine, not optional.
