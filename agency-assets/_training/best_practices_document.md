# Best Practices

## Content
- Always ground claims in the client's actual product/data — never let an AI-generated stat or feature claim ship unverified.
- Match voice guide precisely; genericness is the most common QA failure for AI-assisted drafts.

## Lead generation
- Respect the source platform's terms of service and rate limits when scraping/enriching — this protects both the agency's and the client's standing with these tools.
- Verify email deliverability before a large send — bounced sends damage the client's domain reputation.

## Advertising
- Never let an automated tool change live budget/bids without a human confirming the specific change.
- A/B test creative before scaling spend on unproven variants.

## Analytics
- Cross-check numbers across tools before presenting — a single-source anomaly is more likely a tracking bug than a real trend.
- Always show trend over time, not just a snapshot — a single period rarely tells the full story.

## Tool adoption
- New MCP tool? Verify it exists and is legitimately maintained before it goes anywhere near `.mcp.json` (see `mcp_security_sop.md`).
- Track pay-per-call tool costs against client retainers — surprises here erode trust fast.
