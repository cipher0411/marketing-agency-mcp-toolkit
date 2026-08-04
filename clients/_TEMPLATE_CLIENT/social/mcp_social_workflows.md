# MCP Social Workflows (Client)

See `agency-assets/mcp-configurations/social-mcp-setup.md` for current tool verification status.

## Ideation → creation → distribution pipeline
1. `fetch_trends` (Social Neuron) — surface timely angles relevant to this client's content pillars.
2. `generate_content` / `adapt_content` — draft, informed by `_context/client_brand_voice_guide.md`.
3. `generate_image` / `generate_video` / `generate_carousel` (Social Neuron) or Lamina `create` — produce visuals, brand-locked via `get_brand_profile` / `brand_lookup`.
4. `quality_check` — before anything moves to approval.
5. Client approval per `_sop/brand_approval_sop.md`.
6. `schedule_post` / `schedule_content_plan` — only after approval is logged.

## Analytics loop
1. `fetch_analytics` / `get_performance_insights` weekly — log to `social_analytics_tracker.md`.
2. Feed learnings back into content pillar prioritization in `social_media_strategy_template.md`.

## Platform coverage caveat
Confirm which platforms Social Neuron currently supports (YouTube/Instagram/TikTok per its public docs as of last verification) before committing to a client channel it may not cover — LinkedIn/X posting may require a manual workflow instead.
