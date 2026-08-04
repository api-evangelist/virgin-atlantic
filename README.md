# Virgin Atlantic (virgin-atlantic)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Virgin Atlantic Airways is a United Kingdom long-haul carrier (IATA code VS) based at London Heathrow and Manchester, operating a transatlantic joint venture with Delta Air Lines, Air France-KLM and SkyTeam, and a SkyTeam member since 2023. In the distribution chain it sits as an airline supplier that reaches travel sellers through three routes at once - the legacy GDSs (Amadeus, Sabre, Travelport, all under renewed multi-year content agreements), its own IATA NDC direct connect, and its own consumer channels. Its API posture is distribution-only and honestly gated. Virgin Atlantic publishes no consumer, flight-status or loyalty API, and no OpenAPI or machine-readable API description of any kind. What it does publish, openly and without a login, is the VS NDC Connect portal at ndc.virginatlantic.com - full request and response reference documentation for twelve IATA NDC 21.3 messages, XML samples, workflow diagrams, a certification programme, and downloadable IATA NDC 21.3.3 XSD schema assets. The contract itself is the IATA NDC standard rather than a Virgin-specific shape, but getting a key is not self-serve - production access requires valid IATA accreditation and Virgin Atlantic ticketing authority (or a service-provider connection), a signed Technical User Agreement, Data Processing Agreement and Agency Sales Agreement, and at minimum RED tier certification. There is no bulk export operation and no published base URL - public docs, accreditation required, no exit path.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/virgin-atlantic/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/virgin-atlantic/refs/heads/main/apis.yml)

## Tags

- Travel
- United Kingdom
- Aviation
- Airline
- Distribution
- NDC
- Booking
- GDS

## Timestamps

- **Created:** 2026-07-28
- **Modified:** 2026-07-28

## APIs

### Virgin Atlantic NDC AirShopping API

IATA NDC 21.3 AirShopping message. Flight shopping and availability search returning Virgin Atlantic offers, including calendar and multi-city itineraries. Documented publicly on VS NDC Connect; no base URL is published and a production key requires IATA accreditation plus certification.

- **Human URL:** [https://ndc.virginatlantic.com/docs/airshopping](https://ndc.virginatlantic.com/docs/airshopping)

#### Tags

- NDC
- Shopping
- Offers

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/airshopping)
- [API Reference](https://ndc.virginatlantic.com/docs/airshopping/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/airshopping/rs)
- [Examples](https://ndc.virginatlantic.com/docs/airshopping/samples)
- [XML Schema](schemas/IATA_AirShoppingRQ.xsd)
- [XML Schema](schemas/IATA_AirShoppingRS.xsd)

### Virgin Atlantic NDC OfferPrice API

IATA NDC 21.3 OfferPrice message. Prices a selected offer and returns the firm, bookable price with applicable rules before an order is created.

- **Human URL:** [https://ndc.virginatlantic.com/docs/offerprice](https://ndc.virginatlantic.com/docs/offerprice)

#### Tags

- NDC
- Pricing
- Offers

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/offerprice)
- [API Reference](https://ndc.virginatlantic.com/docs/offerprice/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/offerprice/rs)
- [Examples](https://ndc.virginatlantic.com/docs/offerprice/samples)
- [XML Schema](schemas/IATA_OfferPriceRQ.xsd)
- [XML Schema](schemas/IATA_OfferPriceRS.xsd)

### Virgin Atlantic NDC OrderCreate API

IATA NDC 21.3 OrderCreate message. Creates the Virgin Atlantic Order and PNR from a priced offer, including passenger details and form of payment, and returns an OrderView response.

- **Human URL:** [https://ndc.virginatlantic.com/docs/ordercreate](https://ndc.virginatlantic.com/docs/ordercreate)

#### Tags

- NDC
- Orders
- Booking

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/ordercreate)
- [API Reference](https://ndc.virginatlantic.com/docs/ordercreate/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/ordercreate/rs)
- [Examples](https://ndc.virginatlantic.com/docs/ordercreate/samples)
- [XML Schema](schemas/IATA_OrderCreateRQ.xsd)
- [XML Schema](schemas/IATA_OrderViewRS.xsd)

### Virgin Atlantic NDC SeatAvailability API

IATA NDC 21.3 SeatAvailability message. Returns the seat map and seat pricing for an offer or an existing order.

- **Human URL:** [https://ndc.virginatlantic.com/docs/seatavailability](https://ndc.virginatlantic.com/docs/seatavailability)

#### Tags

- NDC
- Seats
- Ancillaries

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/seatavailability)
- [API Reference](https://ndc.virginatlantic.com/docs/seatavailability/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/seatavailability/rs)
- [Examples](https://ndc.virginatlantic.com/docs/seatavailability/samples)
- [XML Schema](schemas/IATA_SeatAvailabilityRQ.xsd)
- [XML Schema](schemas/IATA_SeatAvailabilityRS.xsd)

### Virgin Atlantic NDC ServiceList API

IATA NDC 21.3 ServiceList message. Returns the ancillary services available against an offer or an order, such as bags and paid services.

- **Human URL:** [https://ndc.virginatlantic.com/docs/servicelist](https://ndc.virginatlantic.com/docs/servicelist)

#### Tags

- NDC
- Ancillaries
- Services

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/servicelist)
- [API Reference](https://ndc.virginatlantic.com/docs/servicelist/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/servicelist/rs)
- [Examples](https://ndc.virginatlantic.com/docs/servicelist/samples)

### Virgin Atlantic NDC OrderRetrieve API

IATA NDC 21.3 OrderRetrieve message. Retrieves a single Virgin Atlantic Order by order identifier or PNR record locator and returns an OrderView response.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderretrieve](https://ndc.virginatlantic.com/docs/orderretrieve)

#### Tags

- NDC
- Orders
- Servicing

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderretrieve)
- [API Reference](https://ndc.virginatlantic.com/docs/orderretrieve/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/orderretrieve/rs)
- [Examples](https://ndc.virginatlantic.com/docs/orderretrieve/samples)
- [XML Schema](schemas/IATA_OrderRetrieveRQ.xsd)
- [XML Schema](schemas/IATA_OrderViewRS.xsd)

### Virgin Atlantic NDC OrderReshop API

IATA NDC 21.3 OrderReshop message. Searches for alternative offers against an existing order, used for voluntary date and time changes and passenger servicing.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderreshop](https://ndc.virginatlantic.com/docs/orderreshop)

#### Tags

- NDC
- Servicing
- Changes

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderreshop)
- [API Reference](https://ndc.virginatlantic.com/docs/orderreshop/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/orderreshop/rs)
- [Examples](https://ndc.virginatlantic.com/docs/orderreshop/samples)
- [XML Schema](schemas/IATA_OrderReshopRQ.xsd)
- [XML Schema](schemas/IATA_OrderReshopRS.xsd)

### Virgin Atlantic NDC OrderQuote API

IATA NDC 21.3 OrderQuote message. Quotes the price of a proposed change to an existing order, including requote and confirm of a held booking.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderquote](https://ndc.virginatlantic.com/docs/orderquote)

#### Tags

- NDC
- Pricing
- Changes

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderquote)
- [API Reference](https://ndc.virginatlantic.com/docs/orderquote/rq)
- [Examples](https://ndc.virginatlantic.com/docs/orderquote/samples)
- [XML Schema](schemas/IATA_OrderQuoteRQ.xsd)

### Virgin Atlantic NDC OrderChange API

IATA NDC 21.3 OrderChange message. Applies changes to an existing order - APIS information amendment, name correction, split order, post-sale seat and service purchase, and voluntary cancellation.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderchange](https://ndc.virginatlantic.com/docs/orderchange)

#### Tags

- NDC
- Orders
- Servicing

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderchange)
- [API Reference](https://ndc.virginatlantic.com/docs/orderchange/rq)
- [Examples](https://ndc.virginatlantic.com/docs/orderchange/samples)
- [XML Schema](schemas/IATA_OrderChangeRQ.xsd)
- [XML Schema](schemas/IATA_OrderViewRS.xsd)

### Virgin Atlantic NDC OrderChangeNotif API

IATA NDC 21.3 OrderChangeNotif message. Notifies the seller of airline-initiated changes to an order, such as schedule changes.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderchangenotif](https://ndc.virginatlantic.com/docs/orderchangenotif)

#### Tags

- NDC
- Notifications
- Schedule Changes

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderchangenotif)
- [API Reference](https://ndc.virginatlantic.com/docs/orderchangenotif/rq)
- [Examples](https://ndc.virginatlantic.com/docs/orderchangenotif/samples)
- [XML Schema](schemas/IATA_OrderChangeNotifRQ.xsd)

### Virgin Atlantic NDC OrderList API

IATA NDC 21.3 OrderList message. Returns a list of orders matching search criteria for the authenticated seller.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderlist](https://ndc.virginatlantic.com/docs/orderlist)

#### Tags

- NDC
- Orders
- Reporting

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderlist)
- [API Reference](https://ndc.virginatlantic.com/docs/orderlist/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/orderlist/rs)
- [Examples](https://ndc.virginatlantic.com/docs/orderlist/samples)
- [XML Schema](schemas/IATA_OrderListRQ.xsd)
- [XML Schema](schemas/IATA_OrderListRS.xsd)

### Virgin Atlantic NDC OrderHistory API

IATA NDC 21.3 OrderHistory message. Returns the change history of an order. This is the closest thing Virgin Atlantic publishes to a data-retrieval operation; it is per-order and is not a bulk export.

- **Human URL:** [https://ndc.virginatlantic.com/docs/orderhistory](https://ndc.virginatlantic.com/docs/orderhistory)

#### Tags

- NDC
- Orders
- History

#### Properties

- [Documentation](https://ndc.virginatlantic.com/docs/orderhistory)
- [API Reference](https://ndc.virginatlantic.com/docs/orderhistory/rq)
- [API Reference](https://ndc.virginatlantic.com/docs/orderhistory/rs)
- [Examples](https://ndc.virginatlantic.com/docs/orderhistory/samples)

## Common Properties

- [Website](https://www.virginatlantic.com/)
- [Portal](https://ndc.virginatlantic.com/)
- [Documentation](https://ndc.virginatlantic.com/docs)
- [Sign Up](https://ndc.virginatlantic.com/account/register)
- [Authentication](https://ndc.virginatlantic.com/help/how-to-start-your-build)
- [Getting Started](https://ndc.virginatlantic.com/help/how-to-access-ndc-apis)
- [Certification](https://ndc.virginatlantic.com/certification)
- [Roadmap](https://ndc.virginatlantic.com/capability/ndc-roadmap)
- [Change Log](https://ndc.virginatlantic.com/product-release)
- [Support](https://ndc.virginatlantic.com/support)
- [Blog](https://ndc.virginatlantic.com/news)
- [XML Schema](schemas/21_3_3_NDC_Schema.zip)
- [Terms of Service](https://flywith.virginatlantic.com/gb/en/partner-hub/policies.html)
- [Policy](https://flywith.virginatlantic.com/gb/en/partner-hub/policies/distribution-policy.html)
- [Policy](https://flywith.virginatlantic.com/gb/en/partner-hub/policies/NDC_Novation_Policy.html)
- [Policy](https://flywith.virginatlantic.com/gb/en/partner-hub/policies/booking-policy.html)
- [Privacy](https://www.virginatlantic.com/policies/virgin-atlantic-airways-and-virgin-atlantic-holidays-privacy-notice)

## Switching Cost

Recorded in full in [review.yml](review.yml). Summary:

- **Interface shape:** standard-plus-proprietary. The messages are IATA NDC 21.3 (schema release 21.3.3, XSD version 9.001, id `IATA2021.3`); the wrapper is Virgin-specific - an Azure API Management subscription key header (`Ocp-Apim-Subscription-Key`), an unpublished base URL, and a Virgin certification programme.
- **Second source:** no-alternative. Amadeus, Sabre, Travelport and NDC aggregators such as Duffel are alternative *routes* to Virgin Atlantic inventory, not alternative *suppliers* of it.
- **Exit path:** no-export-published. No export, dump or bulk operation exists in the twelve documented messages. The NDC Novation Policy runs the other way - "Access Parties must securely return or delete Virgin Data in accordance with the DPA."
- **Identifier portability:** shared IATA identifiers (VS designator, airport codes, PNR record locators, IATA/TIDS numbers, BSP ticket numbers, NDC OrderID) - but "Virgin Atlantic remains the system of record for Orders and PNRs" and "Access Parties must not maintain any authoritative servicing or lifecycle state outside Virgin Atlantic systems."
- **Contractual lock-in:** Technical User Agreement (TUA), Data Processing Agreement (DPA) and Agency Sales Agreement (ASA). Access is "personal to the approved Access Party and does not automatically transfer as part of: a merger; acquisition; outsourcing arrangement; insolvency process; sale of assets; restructuring; or platform migration."
- **Access gate:** accredited-or-licensed. Valid IATA accreditation plus Virgin Atlantic ticketing authority, or an approved service-provider connection; RED tier certification minimum for a production key.
- **Distribution model:** gds-intermediated, hybridising toward NDC direct. IATA Airline Retailing Maturity certified on the 21.3 schema (21 April 2023, 18 capabilities); previously the first airline to reach NDC Level 3 on 18.1.

## Schemas

18 IATA NDC 21.3.3 XSD files plus the official zip, harvested verbatim on 2026-07-28 from
[https://ndc.virginatlantic.com/file-lists/schema-assets](https://ndc.virginatlantic.com/file-lists/schema-assets)
(all HTTP 200). See [schemas/](schemas/). No OpenAPI exists for this API and none was invented.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
