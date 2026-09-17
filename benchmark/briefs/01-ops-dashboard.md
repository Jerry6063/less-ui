# Brief 01 - Cross-border e-commerce operations dashboard

Mirrors the "operations dashboard" task family used in timed AI-collaboration assessments. Paste the whole brief as the first message.

## Context
You are the software PM for a consumer-electronics brand selling chargers, power banks and audio
on Amazon (US/DE/JP) and Shopee (SEA). Ops managers currently juggle six spreadsheets.
Build a clickable prototype of the operations dashboard they open every morning.

## Users and jobs
- Channel ops manager: spot yesterday's anomalies in under 60 seconds, then drill into one SKU.
- Ops lead: compare channels week over week and decide where to move ad budget.

## Must have
1. Overview: revenue, orders, ad spend, ROAS, inventory-days-cover, with 7-day trend and delta vs last week.
2. Channel x marketplace table: sortable, filterable, with health status per row.
3. Alerts panel: stockout risk, review-rating drop, ad-cost spike; each alert opens a detail drawer with recommended action.
4. SKU drill-down drawer: sales trend, inventory by warehouse, top negative review themes.
5. Empty, loading and error states for every data region. Realistic mock data, not lorem ipsum.

## Constraints
- One self-contained `index.html` (inline CSS/JS, CDN allowed for charts). Opens by double-click.
- Desktop-first at 1440, still usable at 1024. Keyboard reachable, visible focus.
- UI language: zh-CN, to mirror exam conditions.
- Deliver in one pass, then list what you would verify with a real user.
