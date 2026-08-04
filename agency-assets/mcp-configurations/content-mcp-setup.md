# Content & Creative MCP Setup

Covers: Social Neuron, Lamina, Canva. openrouter-media and a generic ad-generator are documented separately as capability gaps (see below).

## Social Neuron (`@socialneuron/mcp-server`)
- Requires a paid plan (Starter $49/mo, Team $99/mo, Agency $249/mo).
- 91 tools: ideation (`generate_content`, `fetch_trends`, `adapt_content`), creation (`generate_video`, `generate_image`, `generate_voiceover`, `generate_carousel`), distribution (`schedule_post`, `schedule_content_plan`), analytics (`fetch_analytics`, `get_performance_insights`), brand (`extract_brand`, `get_brand_profile`, `save_brand_profile`), quality (`quality_check`, `quality_check_plan`).
- Env: `SOCIALNEURON_API_KEY`.
- Install: `npm i -g @socialneuron/mcp-server` or run via `npx`.
- Which plan tier a client needs depends on content volume — check their `_context/mcp_configuration.md` before assuming Agency tier.

## Lamina (`github.com/uselamina/lamina-mcp`)
- Real tools per the official repo: `create`, `track`, `evaluate`, `distribute`, `brand_lookup` (the original brief's `lamina_create`/`lamina_brand`/`lamina_batch` names don't match the shipped API — use the real ones).
- Use for: brand-locked product photography, model try-ons, reels, campaign banners from a creative brief + brand kit.
- Requires a Lamina account/API key — see uselamina.ai/developers.
- Load brand rules with `brand_lookup` before generating, so color/font/tone consistency is enforced automatically.

## Canva (official remote MCP)
- Endpoint: `https://mcp.canva.com/mcp`, bridged locally via the `mcp-remote` npm package (already in `.mcp.json`).
- OAuth-based per-user auth — no static API key.
- Enterprise plan unlocks Brand Templates.
- Use for: design generation/editing, library search, asset/folder management, exports.

## Capability gap: image/video generation via OpenRouter
The spec named `openrouter-media`, which doesn't exist. The real equivalent is `@stabgan/openrouter-mcp-multimodal` (chat + image/audio/video generation across Veo, Sora, Seedance, Wan via OpenRouter's unified API). Not wired into `.mcp.json` — verify its current tool list and pricing model against your use case before enabling it for a client.

## Capability gap: standalone ad creative rendering
`ad-generator-mcp` (generate_copy/render_ad/bulk_generate/upload_asset) doesn't exist under that name. See `advertising-mcp-setup.md` for real alternatives.

## Recommended content pipeline
1. `fetch_trends` (Social Neuron) — ideation input.
2. `brand_lookup` (Lamina) or `get_brand_profile` (Social Neuron) — load brand constraints.
3. `generate_image` / `generate_video` / `create` — produce assets.
4. `quality_check` — validate against brand guide before anything goes to a client for approval.
5. `schedule_post` / `schedule_content_plan` — distribute once approved (see `brand_approval_sop.md`).
