---
name: bnsf-resolve-rail-reference-codes
description: Resolve the rail industry code systems every other BNSF call depends on — event codes, station codes, STCC commodity codes, hazardous materials and Umler equipment characteristics.
api: bnsf:bnsf-reference-files
operations:
  - getV1EventCodes
  - getV1Stations
  - getV1Stcc
  - getV1StccHazardous
  - postV1Umler
generated: '2026-09-06'
method: generated
source: openapi/bnsf-reference-files-openapi.yml
---

# Resolve BNSF rail reference codes

Nothing else on this API is usable without these. BNSF's contracts are written in industry code
systems, not in prose: a trace response gives you an event code, a price gives you an STCC range, a
waybill gives you a 333 station and a 633 party code. This service is where those resolve.

**None of these five operations is a Restricted Service.** Together with `getV1RailMiles`, `getV1Hub`
and the trace surface, they are what a newly registered certificate can call on day one.

## Operations

1. `getV1EventCodes` (`GET /v1/event-codes`) — event codes and their descriptions, describing
   equipment activity. Cache this; it is the decoder for every trace response.
2. `getV1Stations` (`GET /v1/stations`) — station details matching input criteria. Resolves the
   `*333` fields that appear across the trace, hub, pricing and webhook payloads.
3. `getV1Stcc` (`GET /v1/stcc`) — Standard Transportation Commodity Code numbers and descriptions.
   The join between what you are shipping and what it costs.
4. `getV1StccHazardous` (`GET /v1/stcc/hazardous`) — detailed hazardous-materials information for
   matching STCCs. Check this before submitting a BOL for regulated freight; the hub surface will
   reject an ingate against a container flagged as prohibiting hazardous material.
5. `postV1Umler` (`POST /v1/umler`) — the AAR/Railinc Umler registry: internal and external
   dimensions, capacities, weights and other characteristics of freight cars, trailers and
   containers. POST, not GET.

## How to use it well

- **Cache aggressively.** Reference data changes slowly and every call costs you against a
  15-requests-per-minute-per-service ceiling. Pull these once and refresh on a schedule, not inline.
- **Reference Files is its own service for quota purposes.** The per-service limits mean a reference
  lookup does not consume your tracing budget — but the shared 100/minute ceiling on a service is
  across all BNSF partners, so a heavy reference job can be throttled by someone else's traffic.
- These codes are not BNSF-private. STCC, SPLC, SCAC, AAR reporting marks and Umler are industry
  standards, so a record resolved here joins cleanly to any other Class I railroad's data.
