---
name: bolsai-dividend-portfolio
description: Build a dividend-income view for a set of B3 tickers — history, yield, and payment calendar.
api: Bolsai Financial Data API
generated: '2026-09-03'
method: generated
source: openapi/bolsai-openapi.json
operations:
  - get_dividends_api_v1_dividends__ticker__get
  - get_fundamentals_api_v1_fundamentals__ticker__get
  - stock_quote_api_v1_stocks__ticker__quote_get
  - stock_corporate_events_api_v1_stocks__ticker__corporate_events_get
---

# Dividend portfolio analysis

Base URL `https://api.usebolsai.com`, auth header `X-API-Key`. Full dividend history needs the Pro plan.

1. **Per ticker, pull the dividend history** — `GET /api/v1/dividends/{ticker}` (`get_dividends_api_v1_dividends__ticker__get`). Each row carries `ex_date`, payment date, and `type` — distinguish **JCP** (juros sobre capital próprio, taxed 15% at source) from regular **dividends** (tax-exempt for individuals) when projecting net income.
2. **Current yield check** — `GET /api/v1/fundamentals/{ticker}` (`get_fundamentals_api_v1_fundamentals__ticker__get`) reads `dividend_yield` alongside payout-relevant indicators (`lpa`, `roe`).
3. **Price for yield-on-cost** — `GET /api/v1/stocks/{ticker}/quote` (`stock_quote_api_v1_stocks__ticker__quote_get`).
4. **Watch for splits/events** — `GET /api/v1/stocks/{ticker}/corporate-events` (`stock_corporate_events_api_v1_stocks__ticker__corporate_events_get`) so per-share dividend series are compared on a consistent share basis.

Budget requests: a 20-ticker portfolio costs ~80 calls per full refresh against the 200/day free quota; check `X-RateLimit-Remaining`.
