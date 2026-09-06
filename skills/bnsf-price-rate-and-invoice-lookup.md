---
name: bnsf-price-rate-and-invoice-lookup
description: Look up BNSF carload and intermodal prices within a Price Authority, retrieve open invoices, and calculate rail miles for local and Rule 11 shipments.
api: bnsf:bnsf-prices
operations:
  - postV1CarloadRates
  - postV1IntermodalRates
  - postV1Invoices
  - postV1RailMiles
  - getV1Stcc
generated: '2026-09-06'
method: generated
source: openapi/bnsf-prices-openapi.yml
---

# Look up BNSF prices, invoices and rail miles

Four operations. Three are Restricted Services; one is not.

## Operations

- `postV1CarloadRates` (`POST /v1/carload-rates`) — **Restricted.** Returns the prices inside a BNSF
  Carload Price Authority.
- `postV1IntermodalRates` (`POST /v1/intermodal-rates`) — **Restricted.** Same, for intermodal.
- `postV1Invoices` (`POST /v1/invoices`) — **Restricted.** Open invoices for up to 5 patron codes per
  request.
- `postV1RailMiles` (`POST /v1/rail-miles`) — **not restricted.** Mileage for BNSF local and/or AAR
  Accounting Rule 11 shipments, up to 1,000 at a time. This is the one operation in the pricing
  service a newly registered caller can use immediately, which makes it a good first Production call.

Note that all four are POST, including the ones that read. `GET` returns `405`.

## Getting access

The three restricted operations need a separate authorisation on your certificate. Request it via
the Customer Portal Message Us box: Business Segment → Web Support → Reason "Application Programming
Interface (API)" → Sub Reason "Restricted Services". BNSF asks you to explain the intended use, and
it will not move you to Production for restricted work until at least one unrestricted service is
demonstrably working.

## Working with the pricing vocabulary

- Commodity ranges are expressed as STCC bounds: `servicePackageCommodityLowStcc` and
  `servicePackageCommodityHighStcc`. Resolve codes first with `getV1Stcc` on the Reference Files API.
- Geography selectors accept several code systems in one field — `S2`/`S4`/`S6` for two-, four- and
  six-digit SPLC, `FS` for freight stations, `PQ`/`PS` for ZIP3/ZIP5, `SP` for states and provinces,
  `OL` for OPSL number ranges. Read the code type before reading the value.
- Intermodal service level is a single letter: `E` Expedited, `P` Premium, `V` Value, `Y` Empty.

## Staying current without polling

Prices change. Rather than re-pulling a Price Authority on a schedule against a 15-per-minute limit,
register for the **Price Update** webhook (see `asyncapi/bnsf-webhooks.yml`): BNSF POSTs the changed
`priceAuthorityNumber`, a note explaining why it was reissued, and a `priceDocumentURL`. Re-pull only
the authority named in the event.
