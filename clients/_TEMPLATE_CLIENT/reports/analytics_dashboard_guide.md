# Analytics Dashboard Guide

## Purpose
How to read and maintain this client's live reporting dashboard (Google Sheets export or equivalent).

## Data refresh
- Frequency: (e.g. daily automated pull via Google Sheets MCP, or manual weekly)
- Source tools: GA4, Ahrefs, HubSpot, Social Neuron, Google Ads — see `mcp_analytics_workflows.md`

## Metric definitions
Document exactly how each metric is calculated (e.g. is "conversion rate" sessions-to-lead or lead-to-customer?) so nobody misreads the dashboard later — ambiguous metric definitions are a common source of client confusion.

## Access
Who at the client has access, and at what permission level (view-only recommended for most stakeholders).

## Troubleshooting
If a number looks wrong: check the source tool directly before assuming the dashboard is broken — most "dashboard bugs" are actually upstream data or attribution issues.
