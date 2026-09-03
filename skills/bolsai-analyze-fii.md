---
name: bolsai-analyze-fii
description: Analyze a Brazilian real-estate fund (FII) — fundamentals, price history, monthly distributions, tenant concentration.
api: Bolsai Financial Data API
generated: '2026-09-03'
method: generated
source: openapi/bolsai-openapi.json
operations:
  - screen_fiis_api_v1_fiis_screener_get
  - get_fii_fundamentals_api_v1_fiis__ticker__get
  - get_fii_history_api_v1_fiis__ticker__history_get
  - get_fii_distributions_api_v1_fiis__ticker__distributions_get
  - get_fii_tenants_api_v1_fiis__ticker__tenants_get
---

# Analyze a Brazilian FII

Base URL `https://api.usebolsai.com`, auth header `X-API-Key`. Historical endpoints need the Pro plan; the free tier serves current data only.

1. **Find candidates** — `GET /api/v1/fiis/screener` (`screen_fiis_api_v1_fiis_screener_get`) filtering by P/VP, dividend yield, vacancy, `fund_type` (Tijolo/Papel/Híbrido/Fundo de Fundos), segment, mandate, or administrator.
2. **Fund fundamentals** — `GET /api/v1/fiis/{ticker}` (`get_fii_fundamentals_api_v1_fiis__ticker__get`): administrator, mandate, asset composition, vacancy, delinquency, top properties.
3. **Distributions** — `GET /api/v1/fiis/{ticker}/distributions` (`get_fii_distributions_api_v1_fiis__ticker__distributions_get`) for the monthly income history (`reference_date` keys the reporting month).
4. **Price history** — `GET /api/v1/fiis/{ticker}/history` (`get_fii_history_api_v1_fiis__ticker__history_get`), rows keyed by `trade_date`.
5. **Tenant risk** — `GET /api/v1/fiis/{ticker}/tenants` (`get_fii_tenants_api_v1_fiis__ticker__tenants_get`) for tenant sector concentration (revenue % per sector).

Combine 3 and 4 to compute distribution yield on cost; use 5 to flag single-sector concentration. FII reports originate from CVM filings, updated weekly on Saturdays.
