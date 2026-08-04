# Lead Generation SOP (Client)

## Trigger
New lead gen campaign or ongoing pipeline-filling retainer work.

## Steps
1. Confirm ICP against `_context/client_growth_marketing_context.md`.
2. Source leads: `business_search`/`find_leads` (Forage) or `search_people` (Apollo) — see `agency-assets/mcp-configurations/leadgen-mcp-setup.md` for current tool status.
3. Enrich: `contact_enrich`/`enrich_person`, cross-verify emails via Hunter before use.
4. De-duplicate against existing CRM records (HubSpot) before adding new contacts.
5. Export to Google Sheets or push directly to HubSpot, tagged by campaign/source.
6. If using cold outreach: push to Instantly campaign only after the client has approved messaging (see `brand_approval_sop.md`) — cold email at scale is effectively a send action and needs the same confirmation discipline as any other outbound send.
7. Track cost per lead against the tool's per-call pricing (Forage/Apify) and log in `reports/mcp_analytics_workflows.md`.

## Compliance
Respect CAN-SPAM/GDPR/CASL as applicable to the client's target geography — unsubscribe mechanisms, no purchased lists misrepresented as opt-in, accurate sender identification.
