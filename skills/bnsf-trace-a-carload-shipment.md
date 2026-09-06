---
name: bnsf-trace-a-carload-shipment
description: Trace one or many BNSF railcars from origin to destination and read the planned events for a shipment, using the BNSF Tracing API over mutual TLS.
api: bnsf:bnsf-trace
operations:
  - getV1Cars
  - postV1Cars
  - getV1TripPlanCarload
  - getV1CarloadConsist
  - getV1EventCodes
generated: '2026-09-06'
method: generated
source: openapi/bnsf-trace-openapi.yml, openapi/bnsf-reference-files-openapi.yml
---

# Trace a BNSF carload shipment

Answers "where is my railcar and when will it arrive". Read-only. Nothing here mutates BNSF state.

## Before you start

- Every call needs a mutual-TLS client certificate registered with BNSF. There is no API key and no
  Authorization header. Base URL is `https://api.bnsf.com:6443` (trial: `https://api-trial.bnsf.com:6443`).
- **You only see equipment whose waybill names your company.** An empty result is not an error and not
  a bug — it means your company is not on that waybill. If you should be seeing it, the shipper must
  add you in the ZS monitoring role or issue a Letter of Authorization.
- Rate limits: 1 request/second and 15 requests/minute per partner per service. Batch instead of
  looping.

## Steps

1. **Pull your whole fleet, or ask for specific cars.**
   - `getV1Cars` (`GET /v1/cars`) returns every railcar you can see, 2,000 per page. Walk pages with
     `?page=1`, `?page=2`. There is no total count and no next link — keep going until a page comes
     back short.
   - `postV1Cars` (`POST /v1/cars`) is the one to prefer when you know what you want: up to 300 cars
     per request in one call. This is the difference between one request and 300 against a 15/minute
     ceiling.
   - Cars are identified by reporting marks: `carInitial` + `carNumber` (e.g. `BNSF` + `316324`).

2. **Get the plan, not just the position.** `getV1TripPlanCarload` (`GET /v1/trip-plan-carload`)
   returns the list of significant events planned for one equipment initial and number, origin to
   destination. Position tells you where it is; the trip plan tells you whether it is late.

3. **For unit trains, use the consist.** `getV1CarloadConsist` (`GET /v1/carload-consist`) returns
   tracing details for all railcars on U, J, C, E, G and X unit trains, rather than car by car.

4. **Decode the event codes.** Trace responses carry event codes, not sentences.
   `getV1EventCodes` (`GET /v1/event-codes`, Reference Files API) returns the code list with
   descriptions. Cache it — it changes rarely and it is a separate service against a separate quota.

## Error handling

- `403` — either your registration is still being configured (BNSF says up to five business days
  from registration, confirmed by email) or your certificate is misconfigured. If the body says
  `{"message": "Insufficient privileges"}` the operation is a Restricted Service; none of the
  operations in this skill are restricted, so a 403 here is about the certificate, not the scope.
- `429` — you exceeded 1/second or 15/minute per service, or the shared 100/minute ceiling for the
  service across all partners. No `Retry-After` is returned; back off yourself.
- `504` — BNSF's guidance is to wait about one minute and retry. Safe here: every operation in this
  skill is a read.

## What this API will not do

There is no push for carload position. If you want to be told rather than to poll, register for the
Bad Order and Local Service Notification webhooks — see `asyncapi/bnsf-webhooks.yml`.
