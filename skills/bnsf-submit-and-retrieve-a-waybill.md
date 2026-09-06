---
name: bnsf-submit-and-retrieve-a-waybill
description: Submit a bill of lading to BNSF to create a waybill, and retrieve the current active waybill for a piece of equipment.
api: bnsf:bnsf-waybill
operations:
  - postV1Bol
  - getV1Waybill
generated: '2026-09-06'
method: generated
source: openapi/bnsf-waybill-openapi.yml
---

# Submit and retrieve a BNSF waybill

The highest-consequence flow on the BNSF Customer API. Two operations, one of which cannot be undone.

## Read this first

- `postV1Bol` (`POST /v1/bol`) submits a bill of lading and creates a waybill. **BNSF publishes no
  void, no cancel, no amend and no delete for it, and no idempotency key.** A duplicate submission is
  a duplicate shipment document. An agent should treat this operation as terminal and require a human
  confirmation before firing it.
- `postV1Bol` is a **Restricted Service**: the certificate must be separately authorised by BNSF and
  the call runs in Production only. `getV1Waybill` is not restricted.
- There is no dry-run for the BOL. The validate operations that exist on this API belong to the
  intermodal gate flow, not to waybilling.

## Steps

1. **Build the BOL body against the EDI vocabulary.** BNSF's own waybill schema carries 90 explicit
   `**EDI Mapping:**` annotations binding its JSON fields to ANSI X12 data elements — for example
   `billOfLadingEdiTransactionSetPurposeCode` → `DE353/BX01` (values `00` Original, `04` Change),
   `billOfLadingPaymentMethodCode` → `DE146/BX03`, `transactionSetAssignedNumber` → `DE554/LX01`.
   If you already produce X12 404 shipment information, map field to field from those annotations
   rather than inventing a translation.

2. **Resolve your codes before you submit, not during.** Commodity is an STCC (`getV1Stcc`,
   `getV1StccHazardous` on the Reference Files API); locations are 333 station codes
   (`getV1Stations`); equipment characteristics come from Umler (`postV1Umler`). A BOL rejected for a
   bad code costs you a request against a 15-per-minute ceiling and, if it is accepted with a wrong
   code, there is no amend operation.

3. **Submit.** `postV1Bol` (`POST /v1/bol`). Record whatever you send, locally, before you send it —
   without a request-id header there is no way to quote the submission back to BNSF API Support
   except by describing it.

4. **Read it back.** `getV1Waybill` (`GET /v1/waybill`) retrieves the current active
   waybill/bill-of-lading information for a given piece of equipment. Because there is no
   idempotency key, a read-back is the only way to establish whether a timed-out submission landed.
   **Do this before any retry.**

## Errors

- `403` with `{"message": "Insufficient privileges"}` — `postV1Bol` is restricted; request access
  through the Customer Portal before assuming a data problem.
- `413` — payload too large; split the submission.
- `504` — BNSF says wait about a minute and retry. Do not retry `postV1Bol` on this advice without
  calling `getV1Waybill` first.
