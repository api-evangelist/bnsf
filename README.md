# BNSF (bnsf)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

BNSF Railway, a subsidiary of Berkshire Hathaway Inc., operates one of the largest freight rail networks in North America — more than 32,000 route miles across 28 states and three Canadian provinces, connecting to Mexico through rail lines in Texas. BNSF publishes a genuine customer-facing API programme: eight OpenAPI 3.0 documents totalling 59 operations covering shipment tracing, intermodal and automotive hub gate operations, freight pricing and invoices, intermodal schedules, waybill management, rail reference data and diagnostics, plus a six-event webhook push surface. Every call is authenticated with certificate-based mutual TLS on port 6443; there is no API key and no OAuth, and 27 of the 59 operations are Restricted Services requiring separate authorisation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/bnsf/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/bnsf/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Producing

## Tags

- Freight
- Railroad
- Shipping
- Trains
- Intermodal
- Logistics
- Supply Chain
- Transportation

## Timestamps

- **Created:** 2025-02-06
- **Modified:** 2026-09-06

## APIs

### BNSF Tracing API

The BNSF Tracing API provides real-time shipment tracing from origin to destination for automotive VINs, carload railcars, intermodal units and unit trains. Fifteen operations cover position, trip plans and significant-event history. Bulk POST forms accept up to 300 VINs, cars or units per request and up to 25 unit trains; list endpoints page at a default and maximum of 2,000 records. None of the fifteen is a Restricted Service, which makes this the surface a newly registered caller can use first.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Railroad
- Tracking
- Tracing
- Shipping
- Intermodal

#### Properties

- **OpenAPI:** [openapi/bnsf-trace-openapi.yml](openapi/bnsf-trace-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-trace-openapi.json](openapi/_original/bnsf-trace-openapi.json)
- **Overlay:** [overlays/bnsf-trace-overlay.yaml](overlays/bnsf-trace-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/trace.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/trace.json)

### BNSF Intermodal Hub Operations API

The BNSF Intermodal Hub Operations API covers facility operations across the BNSF intermodal hub network: dray bookings and dray plans, driver vehicle inspection reports, authorized flips, hub lot locations, ingate and outgate registration with dedicated validation operations, pre-gate creation and cancellation, J1 gate receipts, pickup numbers, street en-route reporting, unit details, domestic empties and parking updates. Twenty-three operations, twenty-one of them Restricted Services requiring separate BNSF authorisation and available in Production only.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Intermodal
- Hub
- Logistics
- Gate Operations
- Drayage

#### Properties

- **OpenAPI:** [openapi/bnsf-intermodal-hub-operations-openapi.yml](openapi/bnsf-intermodal-hub-operations-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-intermodal-hub-operations-openapi.json](openapi/_original/bnsf-intermodal-hub-operations-openapi.json)
- **Overlay:** [overlays/bnsf-intermodal-hub-operations-overlay.yaml](overlays/bnsf-intermodal-hub-operations-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/intermodal-hub-operations.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/intermodal-hub-operations.json)

### BNSF Automotive Hub Operations API

The BNSF Automotive Hub Operations API covers haul-away gate operations at BNSF automotive ramps: gate entry requests submitted before an ingate, gate exit and pre-exit requests, holds placed on and released from a VIN at origin or destination, and gate-pass lookups by AAR ramp code and VIN. Seven operations, keyed on NMFTA SCAC and AAR ramp code, serving truckers, dispatchers and vehicle OEMs.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Automotive
- Hub
- Gate Operations
- VIN
- Logistics

#### Properties

- **OpenAPI:** [openapi/bnsf-automotive-hub-operations-openapi.yml](openapi/bnsf-automotive-hub-operations-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-automotive-hub-operations-openapi.json](openapi/_original/bnsf-automotive-hub-operations-openapi.json)
- **Overlay:** [overlays/bnsf-automotive-hub-operations-overlay.yaml](overlays/bnsf-automotive-hub-operations-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/automotive-hub-operations.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/automotive-hub-operations.json)

### BNSF Prices and Rates API

The BNSF Prices and Rates API returns freight shipping prices for carload and intermodal moves within a BNSF Price Authority, open invoices for up to five patron codes per request, and rail mileage for BNSF local and AAR Accounting Rule 11 shipments up to 1,000 at a time. Commodity ranges are expressed as STCC bounds and geography accepts SPLC, OPSL, FIPS county, state, ZIP3 and ZIP5 selectors. Three of the four operations are Restricted Services; the rail-mile inquiry is not.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Pricing
- Rates
- Invoices
- Shipping
- STCC

#### Properties

- **OpenAPI:** [openapi/bnsf-prices-openapi.yml](openapi/bnsf-prices-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-prices-openapi.json](openapi/_original/bnsf-prices-openapi.json)
- **Overlay:** [overlays/bnsf-prices-overlay.yaml](overlays/bnsf-prices-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/prices.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/prices.json)

### BNSF Schedules API

The BNSF Schedules API returns published intermodal transit schedules for the BNSF network, so a shipper can plan departure and arrival timing before booking freight. A single operation, declared as a Restricted Service requiring separate BNSF authorisation.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Schedules
- Transit
- Intermodal

#### Properties

- **OpenAPI:** [openapi/bnsf-schedules-openapi.yml](openapi/bnsf-schedules-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-schedules-openapi.json](openapi/_original/bnsf-schedules-openapi.json)
- **Overlay:** [overlays/bnsf-schedules-overlay.yaml](overlays/bnsf-schedules-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/schedules.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/schedules.json)

### BNSF Waybill Management API

The BNSF Waybill Management API submits a bill of lading with the required transit information to create a waybill, and retrieves the current active waybill for a given piece of equipment. Its request schema carries ninety explicit EDI Mapping annotations binding JSON fields to ANSI X12 data elements, so a shipper already exchanging X12 404 rail shipment information can map field to field. The submission operation is a Restricted Service and has no published void, cancel or amend.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Waybill
- Bill of Lading
- Carload
- EDI
- Documentation

#### Properties

- **OpenAPI:** [openapi/bnsf-waybill-openapi.yml](openapi/bnsf-waybill-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-waybill-openapi.json](openapi/_original/bnsf-waybill-openapi.json)
- **Overlay:** [overlays/bnsf-waybill-overlay.yaml](overlays/bnsf-waybill-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/waybill.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/waybill.json)

### BNSF Reference Files API

The BNSF Reference Files API resolves the rail industry code systems the rest of the BNSF surface is written in: event codes describing equipment activity, station details behind the 333 location codes, STCC commodity codes and their hazardous-materials detail, and Umler equipment characteristics covering dimensions, capacities and weights for freight cars, trailers and containers. Five operations, none of them restricted.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Freight
- Reference
- Data
- STCC
- Stations
- Umler
- Hazardous Materials

#### Properties

- **OpenAPI:** [openapi/bnsf-reference-files-openapi.yml](openapi/bnsf-reference-files-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-reference-files-openapi.json](openapi/_original/bnsf-reference-files-openapi.json)
- **Overlay:** [overlays/bnsf-reference-files-overlay.yaml](overlays/bnsf-reference-files-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/reference-files.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/reference-files.json)

### BNSF Diagnostics API

The BNSF Diagnostics API exposes an unauthenticated gateway health check that answers 200 with the body <status>ok</status> on both the production and trial hosts, and a Restricted analytic-event operation for submitting usage telemetry. The health check is the only operation on the whole BNSF Customer API reachable without a registered client certificate.

- **Human URL:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Base URL:** `https://api.bnsf.com:6443`

#### Tags

- Diagnostics
- Health Check
- Monitoring
- Telemetry

#### Properties

- **OpenAPI:** [openapi/bnsf-diagnostics-openapi.yml](openapi/bnsf-diagnostics-openapi.yml)
- **OpenAPISource:** [openapi/_original/bnsf-diagnostics-openapi.json](openapi/_original/bnsf-diagnostics-openapi.json)
- **Overlay:** [overlays/bnsf-diagnostics-overlay.yaml](overlays/bnsf-diagnostics-overlay.yaml)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Specification:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/diagnostics.json](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/diagnostics.json)

## Common Properties

- **OpenAPI:** [openapi/bnsf-trace-openapi.yml](openapi/bnsf-trace-openapi.yml)
- **Authentication:** [authentication/bnsf-authentication.yml](authentication/bnsf-authentication.yml)
- **Conventions:** [conventions/bnsf-conventions.yml](conventions/bnsf-conventions.yml)
- **ErrorCatalog:** [errors/bnsf-problem-types.yml](errors/bnsf-problem-types.yml)
- **Lifecycle:** [lifecycle/bnsf-lifecycle.yml](lifecycle/bnsf-lifecycle.yml)
- **Conformance:** [conformance/bnsf-conformance.yml](conformance/bnsf-conformance.yml)
- **DataModel:** [data-model/bnsf-data-model.yml](data-model/bnsf-data-model.yml)
- **RateLimits:** [rate-limits/bnsf-rate-limits.yml](rate-limits/bnsf-rate-limits.yml)
- **Plans:** [plans/bnsf-plans-pricing.yml](plans/bnsf-plans-pricing.yml)
- **Sandbox:** [sandbox/bnsf-sandbox.yml](sandbox/bnsf-sandbox.yml)
- **Webhooks:** [asyncapi/bnsf-webhooks.yml](asyncapi/bnsf-webhooks.yml)
- **AgentSkill:** [skills/_index.yml](skills/_index.yml)
- **LLMsTxt:** [llms/bnsf-llms.txt](llms/bnsf-llms.txt)
- **X-MCPServerCandidate:** [mcp/bnsf-mcp.yml](mcp/bnsf-mcp.yml)
- **Packages:** [packages/bnsf-packages.yml](packages/bnsf-packages.yml)
- **DomainSecurity:** [security/bnsf-domain-security.yml](security/bnsf-domain-security.yml)
- **AgenticAccess:** [agentic-access/bnsf-agentic-access.yml](agentic-access/bnsf-agentic-access.yml)
- **FinOps:** [finops/bnsf-finops.yml](finops/bnsf-finops.yml)
- **Website:** [https://www.bnsf.com](https://www.bnsf.com)
- **Portal:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **DeveloperPortal:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/)
- **Documentation:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/catalog/)
- **APIReference:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **Console:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/developers-console/)
- **GettingStarted:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/getting-started/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/getting-started/)
- **SignUp:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/registration/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/registration/)
- **Support:** [https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/support/](https://www.bnsf.com/ship-with-bnsf/support-services/customer-api/support/)
- **Login:** [https://customer2.bnsf.com/](https://customer2.bnsf.com/)
- **Blog:** [https://www.bnsf.com/news-media/railtalk/](https://www.bnsf.com/news-media/railtalk/)
- **TermsOfService:** [https://www.bnsf.com/site-terms-of-use.html](https://www.bnsf.com/site-terms-of-use.html)
- **PrivacyPolicy:** [https://www.bnsf.com/privacy-policy.html](https://www.bnsf.com/privacy-policy.html)
- **LinkedIn:** [https://www.linkedin.com/company/bnsf-railway](https://www.linkedin.com/company/bnsf-railway)

## Maintainers

- Kin Lane <kinlane@gmail.com>
