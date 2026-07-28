---
name: virgin-atlantic-receive-order-change-notifications
description: Subscribe to and process Virgin Atlantic OrderChangeNotif push messages so airline-initiated schedule changes, cancellations and IROP events reach your system.
api: Virgin Atlantic NDC (IATA NDC 21.3)
generated: '2026-07-28'
method: generated
source: https://ndc.virginatlantic.com/docs/orderchangenotif
operations:
  - OrderChangeNotif
  - OrderRetrieve
schemas:
  - schemas/IATA_OrderChangeNotifRQ.xsd
  - schemas/IATA_OrderRetrieveRQ.xsd
  - schemas/IATA_OrderViewRS.xsd
---

# Receive Virgin Atlantic order change notifications

OrderChangeNotif is the only asynchronous surface Virgin Atlantic publishes. The airline pushes an
`OrderChangeNotifRQ` to **your** endpoint when an order changes without you asking — schedule
changes, cancellations and IROP (irregular operations). It is inbound to you; there is no polling
equivalent.

## Register first — you will not receive anything otherwise

Verbatim from the documentation: *"The seller or aggregator must support receiving and processing
OrderChangeNotifRQ messages asynchronously by subscribing to the service."*

Registration is an application on VS NDC Connect. Have ready:

- API details — username and key, **specific to the environment**
- IATA number / Aggregator ID
- your **endpoint URL**
- the **SOAP Action**
- API login credentials — UserID and Password

Note that Virgin Atlantic authenticates *into* your endpoint with credentials you supply. No
signature header, HMAC scheme or replay-protection contract is published, so enforce your own
allow-listing and duplicate detection.

## Handle the message

The request carries two things:

- **`ChangeGroup`** — the type of change (schedule change, cancellation …), the reason and the time.
  `ChangeTypeCode` and `ReasonCode` are in scope.
- **`CurrentOrder`** — the updated order: order ID, flight segments, passengers and services.

There is **no response**: the documentation states `Response: N/A`. Acknowledge at the HTTP layer
and process asynchronously. Follow-up action is explicitly out of scope of the message, so decide
your own remediation (rebook, notify the traveller, refund) from the change type.

Because there is no delivery guarantee, retry policy or replay contract published, reconcile
periodically with `OrderRetrieve` rather than treating the push as the sole source of truth.

## Preconditions Virgin Atlantic states

1. The order was created in VS NDC by the authorised agent.
2. An involuntary change occurred (schedule change, cancellation, IROP).
3. You have subscribed and can process the message asynchronously.

## What is not live yet

Phase 2 — notifications for **voluntary** changes made within the NDC channel — is "Selected for
Development" on the Q2 2026 roadmap with PreLive and Live dates still TBC. Today the surface covers
involuntary change only.

## Samples and schema

`examples/orderchangenotif/` holds Virgin Atlantic's published request samples;
`schemas/IATA_OrderChangeNotifRQ.xsd` is the contract. No Error Response page is published for this
message — it is fire-and-forget.
