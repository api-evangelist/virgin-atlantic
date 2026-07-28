---
name: virgin-atlantic-shop-price-and-book
description: Shop Virgin Atlantic flights, price a selected offer and create a ticketed order (instant payment, no seat selection) over the IATA NDC 21.3 API.
api: Virgin Atlantic NDC (IATA NDC 21.3)
generated: '2026-07-28'
method: generated
source: https://ndc.virginatlantic.com/capability/offer/prime-sale-without-seat
operations:
  - AirShopping
  - OfferPrice
  - OrderCreate
schemas:
  - schemas/IATA_AirShoppingRQ.xsd
  - schemas/IATA_AirShoppingRS.xsd
  - schemas/IATA_OfferPriceRQ.xsd
  - schemas/IATA_OfferPriceRS.xsd
  - schemas/IATA_OrderCreateRQ.xsd
  - schemas/IATA_OrderViewRS.xsd
---

# Shop, price and book a Virgin Atlantic flight

Virgin Atlantic's published "Prime Sale Without Seat (Instant Payment)" flow. Every element name
below comes from the IATA NDC 21.3 schema assets in `schemas/`; every rule comes from the airline's
own workflow page.

## Before you start

- **Transport.** Every message is an HTTP `POST` with an IATA NDC 21.3 XML body. Virgin Atlantic
  publishes no base URL — the endpoint is issued with your API key.
- **Headers.** `Ocp-Apim-Subscription-Key: <your VS NDC API key>`, `Accept: application/xml`,
  `Content-Type: application/xml`. Requests and responses must be UTF-8.
- **Environments.** A test key is self-serve after portal registration; a production key needs RED
  tier certification plus IATA accreditation. See `sandbox/virgin-atlantic-sandbox.yml`.
- **Validate locally first.** Parse your request against the XSD in `schemas/` before sending — a
  missing mandatory element returns error `912`, not a helpful parse message.
- **Working payloads.** `examples/airshopping/`, `examples/offerprice/` and `examples/ordercreate/`
  hold Virgin Atlantic's own request and response samples for this flow.

## Step 1 — AirShopping

Search by origin/destination for a date. One way, return, open jaw and multi-city are supported;
airport or city codes; multiple cabins per itinerary; passenger types ADT, CHD, GBE and infant.

Send in `DistributionChain` the agency and aggregator identifiers (IATA or TIDS number) — missing or
invalid values return `717`.

The response is a list of offers, each with total price by passenger type, baggage allowance, change
and refund rules, the fare product (e.g. Economy Classic) and a `PaymentTimeLimit`.

Hard limits worth coding against:
- maximum 9 non-infant passengers (`68`)
- maximum 6 origin/destination pairs (`724`)
- infants may not outnumber adults (`324`)
- only homogeneous offers are returned (same fare product outbound and inbound)
- calendar search, group bookings, brand attributes, infant-with-seat and unaccompanied minors are
  not supported on AirShopping

To target a specific product, use Airline Taxonomy codes at itinerary level with `IncludeInd`:
`13EC` (checked bag), `189C` (preferred seat). If no fare product matches, you get an error rather
than an empty list.

## Step 2 — OfferPrice

Send the `OfferID` and the `OfferItemID`s of the offer you selected, with **the same number and
types of passengers** you sent to AirShopping.

You get back the firm price with tax breakdown per passenger, baggage allowance, fare rules, brand
attributes and `PaymentTimeLimit` — plus **upsell offers** in the "Other Offers" section (the next
higher fare products in the same cabin and all products in higher cabins).

Offers expire. `913` with StatusText `Unavailable` means the offer, priced offer or `OfferID` timed
out — the documented remedy is to call AirShopping again. There is no idempotency key on this API;
the single-use `OfferID` is what protects you from duplicate orders.

## Step 3 — OrderCreate

Send the `OfferID` and `OfferItemID`s from the OfferPrice response, passenger details, any Flying
Club (FQTV) details, and payment.

Payment rules:
- card only on this flow, and **one card per transaction**
- online travel agents complete 3DS2 authentication **upfront** and then call OrderCreate with the
  authenticated details
- offline travel agents send card details without 3DS2 authentication
- IATA BSP Cash and BSP EasyPay are documented as separate forms of payment

The OrderView response returns the `OrderID`, booking reference, flight segments, total order price,
per-passenger fare and tax breakdown, ticket details and ticketed baggage allowance. Note what it
does **not** return: fare rules, cabin and PriceClass details. Hold bookings are not supported on
this flow (see the Hold Booking Creation Flow instead), and there is no price guarantee.

## Errors

Errors come back as repeating `<Error>` elements carrying a PADIS 9321 `<Code>`, `<DescText>` and a
`<TypeCode>` processing status (`NotProcessed`, `Processed`, `Unavailable`, `Unknown`, `Retry`).
Treat `Unavailable` as "restart from AirShopping" and `NotProcessed` as "fix the request".

The full published registry — 258 error rows and 38 warning rows across 71 distinct codes — is in
`errors/virgin-atlantic-error-codes.yml`. The two you will hit first: `111` (invalid API key) and
`912` (mandatory element missing).

## Testing

Use the published test cards in `sandbox/virgin-atlantic-sandbox.yml`. For 3DS you must send the
exact `AuthenticationValue` and `DirectoryServerTrxID` Virgin Atlantic publishes together with a
3DS-supported test card — any other value fails authentication by design, which is how you test the
negative path. Test Flying Club numbers are published per tier for loyalty accrual.
