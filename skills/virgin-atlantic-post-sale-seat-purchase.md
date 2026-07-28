---
name: virgin-atlantic-post-sale-seat-purchase
description: Reserve free or paid seats against an existing Virgin Atlantic order using SeatAvailability and OrderChange on the IATA NDC 21.3 API.
api: Virgin Atlantic NDC (IATA NDC 21.3)
generated: '2026-07-28'
method: generated
source: https://ndc.virginatlantic.com/capability/order/post-sale-seat-purchase-flow
operations:
  - OrderRetrieve
  - SeatAvailability
  - OrderChange
schemas:
  - schemas/IATA_OrderRetrieveRQ.xsd
  - schemas/IATA_SeatAvailabilityRQ.xsd
  - schemas/IATA_SeatAvailabilityRS.xsd
  - schemas/IATA_OrderChangeRQ.xsd
  - schemas/IATA_OrderViewRS.xsd
---

# Buy seats on an existing Virgin Atlantic order

Virgin Atlantic's published "Post Sale Seat Purchase Flow" — reserving free and/or paid seats after
the order already exists. Sample payloads for every step are in `examples/orderretrieve/`,
`examples/seatavailability/` and `examples/orderchange/`.

## Preconditions

- An order already exists in VS NDC, created by your agency.
- Same transport contract as every other message: `POST`, XML in and out, UTF-8,
  `Ocp-Apim-Subscription-Key` header. See `conventions/virgin-atlantic-conventions.yml`.

## Step 1 — OrderRetrieve (optional)

Fetch the current state of the order before you change it. Identify it by `OrderID`, by booking
reference, or by both. The response returns the `OrderID`, booking reference and the current order
content, which is what you will reference in the following steps.

Skip this only if you already hold a fresh copy of the order.

## Step 2 — SeatAvailability

Request the seat map for the order. The response returns the seat map and seat pricing, keyed to the
segments and passengers of the order.

Reference identifiers follow Virgin Atlantic's published syntax — `SEG1`, `SEG2` … for
`PaxSegmentID`, `ADULT_1` style values for `PaxID` — so bind the seat you pick back to the right
`PaxSegmentRefID` and `PaxRefID`. The full ID/RefID table is in
`data-model/virgin-atlantic-data-model.yml`.

## Step 3 — OrderChange

Apply the seat selection as a change to the order, including payment for any paid seats. The
response is an OrderView document with the updated order.

Rules carried over from the order-creation flow:
- only one payment card per transaction
- only free/paid **seat** ancillaries are supported on this path (paid services go through the Post
  Sale Service Purchase flow with ServiceList)
- OrderView does not return fare rules, cabin or PriceClass details

## Errors

OrderChange has the second-largest published error surface of any Virgin Atlantic message (69 rows).
Read them from `errors/virgin-atlantic-error-codes.yml` and branch on the `<TypeCode>` processing
status rather than on the numeric code alone — the same code can carry different descriptions on
different messages.

There is no idempotency key. If an OrderChange call fails ambiguously, re-run OrderRetrieve and
compare the order state before retrying, rather than blindly resending.

## Testing

Use the published test cards and Flying Club numbers in `sandbox/virgin-atlantic-sandbox.yml`. The
airline's own full-flow XML samples for this journey were published 5 July 2025 and cover
AirShopping through OrderChange.
