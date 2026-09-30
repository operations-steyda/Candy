# STEYDA — Candy Operating Dashboard + Assistant

A self-contained web dashboard for the STEYDA (Hali Design AB) Amazon FBA candy
business, with **Billy** — a built-in AI assistant that answers questions from
the dashboard's own live data.

## What's here
- **`index.html`** — the full Candy Operating Dashboard (Overview, PPC, Sales &
  Traffic, inventory, production/purchase planners) **plus** a "✨ Ask" assistant
  panel (bottom-right).

## Billy (the assistant)
Tap **Ask Billy** and query in plain English:
- "What needs restocking?" — SKUs sorted by urgency, with order qty + stockout
- "Days of cover for Bubs" / "how much to order for [SKU]"
- "Top sellers last 30 days" / "slowest sellers"
- "Overview" — totals, on-hand, pipeline

It reads the dashboard's embedded `PAYLOAD` data directly — **no API key, no
server, nothing leaves the page.**

## Hybrid AI (optional, later)
The assistant is wired for a real LLM. In `index.html`, find `AGENT_CONFIG`:
```js
var AGENT_CONFIG = { endpoint: "", model: "claude-opus-4-8" };
```
Set `endpoint` to a serverless proxy (Cloudflare Worker / Vercel function) that
holds your API key. When set, every question is answered by a real LLM with the
dashboard data as context; when blank, the free built-in resolver runs. The
`buildContext()` function already packages the data for the model.

> Never put an API key in this file — it's a public web page. Keep the key on the
> serverless side only.

## Refreshing the data
Regenerate the Candy Integrated Dashboard, then replace `index.html` (the
assistant block re-injects on rebuild) and push.
