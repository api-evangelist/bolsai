---
name: bolsai-screen-stocks
description: Screen B3 stocks by fundamentalist metrics with the Bolsai API, then deep-dive the shortlist.
api: Bolsai Financial Data API
generated: '2026-09-03'
method: generated
source: openapi/bolsai-openapi.json
operations:
  - screen_stocks_api_v1_screener__get
  - get_fundamentals_api_v1_fundamentals__ticker__get
  - stock_quote_api_v1_stocks__ticker__quote_get
  - list_sectors_api_v1_companies_sectors_get
---

# Screen B3 stocks by fundamentals

Base URL `https://api.usebolsai.com` — send your key in the `X-API-Key` header on every call. Free tier: 200 requests/day, reset at midnight UTC; watch `X-RateLimit-Remaining` and stop on `429`.

1. **(Optional) list sectors** — `GET /api/v1/companies/sectors` (`list_sectors_api_v1_companies_sectors_get`) to see available sectors with company counts before filtering.
2. **Screen** — `GET /api/v1/screener/` (`screen_stocks_api_v1_screener__get`) with fundamentals filters (dividend yield, P/L, ROE, etc.). Fundamentals fields use Portuguese snake_case abbreviations: `pl`, `pvp`, `lpa`, `vpa`, `p_sr`, `dividend_yield`, `roe`, `roic`. Paginate with `limit`/`offset`; the response carries `count`, `total`, `offset`, `limit`.
3. **Deep-dive each shortlisted ticker** — `GET /api/v1/fundamentals/{ticker}` (`get_fundamentals_api_v1_fundamentals__ticker__get`) for the full 27+ indicator set.
4. **Get the current quote** — `GET /api/v1/stocks/{ticker}/quote` (`stock_quote_api_v1_stocks__ticker__quote_get`) for price, daily change, 52-week range, YTD return. Prices are end-of-day, updated 20:30 BRT.

Errors: `422` returns FastAPI `{"detail": [{"loc", "msg", "type"}]}` — fix the named parameter. `401` means the `X-API-Key` header is missing or invalid.
