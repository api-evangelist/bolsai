---
name: bolsai-macro-context
description: Pull Brazilian macro series (SELIC, IPCA, CDI, IGP-M) from the Central Bank to contextualize an equity or FII analysis.
api: Bolsai Financial Data API
generated: '2026-09-03'
method: generated
source: openapi/bolsai-openapi.json
operations:
  - list_series_api_v1_macro__get
  - get_series_api_v1_macro__series_name__get
  - get_series_stats_api_v1_macro__series_name__stats_get
---

# Macro context for B3 analysis

Base URL `https://api.usebolsai.com`, auth header `X-API-Key`. Historical macro series need the Pro plan; series update daily at 20:30 BRT.

1. **Discover series** — `GET /api/v1/macro/` (`list_series_api_v1_macro__get`) lists available BCB series (SELIC, IPCA, CDI, IGP-M, USD/BRL).
2. **Fetch a series** — `GET /api/v1/macro/{series_name}` (`get_series_api_v1_macro__series_name__get`), paginated with `limit`/`offset`.
3. **Summary stats** — `GET /api/v1/macro/{series_name}/stats` (`get_series_stats_api_v1_macro__series_name__stats_get`) for current value and historical aggregates.

Typical uses: compare a stock's `dividend_yield` against CDI; deflate long price histories with IPCA; frame FII distribution yields against SELIC. Data comes from the BCB's official series.
