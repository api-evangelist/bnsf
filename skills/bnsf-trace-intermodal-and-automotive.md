---
name: bnsf-trace-intermodal-and-automotive
description: Trace intermodal units and automotive VINs on the BNSF network, including trip plans, VIN detail and inspection records.
api: bnsf:bnsf-trace
operations:
  - getV1Units
  - postV1Units
  - getV1TripPlanIntermodal
  - postV1Vins
  - getV1VinDetails
  - getV1VinInspections
  - getV1TripPlanAutomotive
generated: '2026-09-06'
method: generated
source: openapi/bnsf-trace-openapi.yml
---

# Trace intermodal units and automotive VINs

Two shipment identities live on the same BNSF Tracing API. Intermodal moves are keyed on equipment
initial and number; automotive moves are keyed on VIN. Read-only.

## Intermodal

1. `postV1Units` (`POST /v1/units`) — up to 300 units per request. Use this, not the list endpoint,
   when you know your units.
2. `getV1Units` (`GET /v1/units`) — every unit you can see, 2,000 per page, `?page=N`.
3. `getV1TripPlanIntermodal` (`GET /v1/trip-plan-intermodal`) — the planned significant events for
   one intermodal equipment initial and number, origin to destination.

## Automotive

1. `postV1Vins` (`POST /v1/vins`) — tracing detail for up to 300 VINs at a time.
2. `getV1VinDetails` (`GET /v1/vin-details`) — the detail record behind a VIN shipment.
3. `getV1VinInspections` (`GET /v1/vin-inspections`) — inspection records for your VIN shipments.
   This is the damage-claim trail; pull it before disputing condition at delivery.
4. `getV1TripPlanAutomotive` (`GET /v1/trip-plan-automotive`) — planned events for a VIN.

## Rules that apply to all of it

- Mutual TLS on `https://api.bnsf.com:6443`. No key, no token.
- Visibility follows the waybill: your company must be named on it, or hold a Letter of Authorization,
  or be added in the ZS monitoring role.
- 1 request/second, 15/minute per partner per service. Prefer the bulk POST forms.
- Responses wrap collections as `{"elements": [...]}`. Dates on the trace surface are `MM/DD/YYYY`
  strings, not ISO 8601 — do not assume a parseable timestamp.
- Every operation here is a read, so a retry after `429` or `504` is safe. That is not true of the
  gate and waybill skills.
