---
name: bnsf-intermodal-gate-flow
description: Move an intermodal unit through a BNSF hub gate — validate first, pre-gate ahead of arrival, gate in, gate out, and cancel a pre-gate that is no longer needed.
api: bnsf:bnsf-intermodal-hub-operations
operations:
  - postV2StreetEnRoute
  - postV2IngateValidate
  - postV2Ingate
  - postV1PregateIn
  - deleteV1PregateIn
  - postV2OutgateValidate
  - postV2Outgate
  - postV1PregateOut
  - deleteV1PregateOut
  - getV1Hub
  - postV1PickupNumber
generated: '2026-09-06'
method: generated
source: openapi/bnsf-intermodal-hub-operations-openapi.yml
---

# Move a unit through a BNSF intermodal gate

This skill mutates real facility state. Read the warnings before the steps.

## Warnings

- **Almost every operation here is a Restricted Service.** 21 of the 23 intermodal hub operations
  declare the `Restricted` requirement. A registered certificate is not enough: BNSF must separately
  authorise it, via the Customer Portal Message Us box (Business Segment → Web Support → Reason
  "Application Programming Interface (API)" → Sub Reason "Restricted Services"). Restricted Services
  run in **Production only**, and BNSF requires at least one unrestricted service working first.
  An unauthorised call returns `403` with `{"message": "Insufficient privileges"}`.
- **There is no idempotency key on this API.** If `postV2Ingate` times out you do not know whether
  the gate movement was recorded. Do not blind-retry a gate write; read state back first.
- **Ingate and outgate have no reversal.** `postV1PregateIn` and `postV1PregateOut` can be cancelled;
  `postV2Ingate` and `postV2Outgate` cannot. Treat those two as terminal.

## Steps

1. **Rehearse before you write.** This API gives you a real dry run, and it is the only safety net
   available:
   - `postV2IngateValidate` (`POST /v2/ingate/validate`) returns the required and missing information
     for an ingate without performing it.
   - `postV2OutgateValidate` (`POST /v2/outgate/validate`) does the same for an outgate.
   - `postV2StreetEnRoute` (`POST /v2/street-en-route`) reports pre-arrival at the hub and returns a
     rail-waybill ingate completeness check plus any missing elements.
   Run one of these first. A validate call that comes back clean is the closest thing to a safe
   retry this API offers.

2. **Pre-gate ahead of arrival, if you can.** `postV1PregateIn` (`POST /v1/pregate/in`) creates an
   ingate before the truck reaches the facility; `postV1PregateOut` (`POST /v1/pregate/out`) does the
   same for an exit. Both take `equipmentInitial` and `equipmentNumber`.

3. **Cancel a pre-gate you no longer need.** `deleteV1PregateIn` (`DELETE /v1/pregate/in`) and
   `deleteV1PregateOut` (`DELETE /v1/pregate/out`) are the documented reversals. BNSF states no time
   window for either — do not assume one exists, and cancel as soon as the plan changes.

4. **Perform the movement.** `postV2Ingate` (`POST /v2/ingate`) registers way-billed units prior to
   arrival; `postV2Outgate` (`POST /v2/outgate`) registers them prior to exit. No reversal.

5. **Supporting lookups.** `getV1Hub` (`GET /v1/hub`) lists valid lot locations at a facility — this
   one is NOT restricted. `postV1PickupNumber` (`POST /v1/pickup-number`) validates or retrieves a
   pickup number before the driver is dispatched.

## Errors

| Code | What it means here |
| --- | --- |
| 403 | Certificate not yet configured, or the operation is a Restricted Service you are not authorised for |
| 405 | Wrong method — most of this surface is POST even where a GET would read naturally |
| 429 | 1/sec, 15/min per partner per service; 100/min shared across all partners on the service |
| 504 | Wait about a minute — but read state back before retrying a write, because there is no idempotency key |
