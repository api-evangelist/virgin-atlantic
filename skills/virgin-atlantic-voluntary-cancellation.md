---
name: virgin-atlantic-voluntary-cancellation
description: Cancel a Virgin Atlantic order voluntarily - risk-free (RFC) inside the free-cancellation window or non-risk-free with penalties - using OrderRetrieve, OrderReshop and OrderChange.
api: Virgin Atlantic NDC (IATA NDC 21.3)
generated: '2026-07-28'
method: generated
source: https://ndc.virginatlantic.com/capability/order/voluntary-cancellation-flow
operations:
  - OrderRetrieve
  - OrderReshop
  - OrderChange
schemas:
  - schemas/IATA_OrderRetrieveRQ.xsd
  - schemas/IATA_OrderReshopRQ.xsd
  - schemas/IATA_OrderReshopRS.xsd
  - schemas/IATA_OrderChangeRQ.xsd
  - schemas/IATA_OrderViewRS.xsd
---

# Cancel a Virgin Atlantic order

Virgin Atlantic's published "Voluntary Cancellation Flow". The airline publishes two sample sets for
it — **Risk-Free Cancellation (RFC)**, inside the window where no penalty applies, and **Non
Risk-Free Cancellation**, where penalties do. Both run the same three messages. Samples are in
`examples/orderretrieve/`, `examples/orderreshop/` and `examples/orderchange/` (published
11 April 2025).

## Step 1 — OrderRetrieve

Identify the order by `OrderID`, by booking reference, or by both. Read back the current order,
including the segments and passengers you intend to cancel.

## Step 2 — OrderReshop (eligibility and quote)

OrderReshop is the eligibility check: it returns what the cancellation would cost. Use it to
determine whether the order is inside the risk-free window or whether penalties apply, and to read
the penalty amounts published under `PenaltyList`.

Do not assume RFC eligibility from your own clock — take it from the reshop response.

## Step 3 — OrderChange (confirm the cancellation)

Apply the cancellation. The OrderView response confirms the resulting order state.

The 2026 roadmap adds "Residual value in NDC", which will return the remaining monetary value of a
partly used order after cancellation or refund — it is not available yet, so do not code against it.

## Errors

Cancellation errors sit inside the OrderReshop (22 rows) and OrderChange (69 rows) registries in
`errors/virgin-atlantic-error-codes.yml`. Branch on the `<TypeCode>` processing status:
`NotProcessed` means the request was rejected and the order is unchanged; `Unavailable` generally
means a reference (offer or reshop result) has expired and you should restart from OrderRetrieve.

There is no idempotency key on this API. Because a cancellation is destructive and not replay-safe,
always re-run OrderRetrieve to establish the true order state before retrying a failed OrderChange.

## Related flows

- **Voluntary date/time change** — OrderReshop then OrderQuote then OrderChange
  (https://ndc.virginatlantic.com/capability/order/voluntary-change-itinerary).
- **Involuntary change and disruption handling** — accept, cancel-and-refund and rebook flows for
  disrupted bookings are on the roadmap, not yet live. Until then, airline-initiated changes arrive
  via OrderChangeNotif (`asyncapi/virgin-atlantic-orderchangenotif-webhooks.yml`).
