# Domain Model

> AI-assisted (Claude): Claude coached by offering options for concepts, associations, attributes, invariants and responsibilities; I picked them, and Claude formatted my choices into these tables and looked up the Lab 1 references for "Traces to". I drew the associations; Claude typed the concept boxes into a draw.io starter file and added the multiplicity labels from my association table (see PROMPTS.md).

![Domain model](domain-model.png)

<!--
Concepts of the hotel booking DOMAIN — not software.
No controllers, services, repositories, database tables or screens.
Save the diagram as docs/design/domain-model.png.
-->

## Concepts and responsibilities

| Concept | Knows | Does | Traces to |
|---|---|---|---|
| Hotel | Name, city, address; its owner, rooms and reviews | Offers rooms; collects reviews | UC-06, FR-20 |
| Room | Room number, whether it is wheelchair-accessible; its hotel, room type and bookings | Tells whether it is free for given nights | UC-01, FR-07, FR-08 |
| Room type | Name, maximum number of guests; its rooms and rates | Groups similar rooms; has the rates | UC-07, FR-19 |
| Price/Rate | Amount per night, valid from, valid to | Gives the price per night for a date | UC-07, FR-09, FR-19 |
| Owner | Name, email; the hotels they run | Manages hotels, rooms and prices; can cancel bookings | UC-06, UC-07, FR-17, FR-20 |
| Guest | First name, last name, email, phone (optional); their bookings and reviews | Books, changes and cancels bookings; writes reviews | UC-01, FR-03, FR-10 |
| Booking | Arrival date, departure date, booked price per night, status; its guest, room, payments, invoice and cancellation | Checks its dates and keeps its price; can be confirmed, changed or cancelled, roomNumber | UC-01, UC-02, UC-03, FR-03 to FR-09 |
| Payment | Amount, method, paid at | Records that money was paid | UC-01, UC-03, FR-05, FR-14 |
| Refund | Amount, status | Records money going back to the guest | UC-02, FR-11, FR-18 |
| Cancellation | Cancelled at, cancelled by, reason, fee | Calculates the fee and decides whether the cancellation is allowed | UC-02, FR-11, FR-12, FR-17, FR-25 |
| Invoice | Invoice number, total including taxes and fees, issued at | Shows the total paid including taxes and fees | FR-04 |
| Review | Text, stars, owner's reply | Holds a guest's opinion; accepts an owner's reply; can only be removed by customer support | FR-21 to FR-24 |
| Customer support | Name | Helps guests and owners; removes spam or racist reviews | UC-10, FR-24 |

## Associations

| From | To | Multiplicity | Meaning |
|---|---|---|---|
| Owner | Hotel | 1 — 1..* | An owner runs one or more hotels (D-22) |
| Hotel | Room | 1 — 1..* | A hotel has one or more rooms |
| Room | Room type | 0..* — 1 | Each room is of exactly one room type |
| Room type | Price/Rate | 1 — 1..* | A room type has one or more rates (by season, weekday or event) |
| Guest | Booking | 1 — 0..* | A guest makes zero or more bookings |
| Booking | Room | 0..* — 1 | A booking is for exactly one room (D-21) |
| Booking | Payment | 1 — 1..* | A booking has one or more payments (first payment, price difference after a change, D-19) |
| Booking | Cancellation | 1 — 0..1 | A booking is cancelled at most once |
| Owner | Cancellation | 0..1 — 0..* | An owner makes zero or more cancellations; a cancellation is made by at most one owner, because guests can cancel too (D-04) |
| Guest | Cancellation | 0..1 — 0..* | A guest makes zero or more cancellations; a cancellation is made by at most one guest, because owners can cancel too (D-01) |
| Cancellation | Refund | 1 — 0..1 | A cancellation leads to at most one refund |
| Guest | Review | 1 — 0..* | A guest writes zero or more reviews |
| Review | Hotel | 0..* — 1 | A review is about exactly one hotel |
| Booking | Invoice | 1 — 1 | A booking has one invoice |
| Customer support | Review | 1 — 0..* | Customer support removes zero or more reviews (D-12) |

## Attributes

| Concept | Attributes |
|---|---|
| Hotel | name, city, address |
| Room | room number, wheelchair-accessible |
| Room type | name, maximum guests |
| Price/Rate | amount per night, valid from, valid to |
| Owner | name, email |
| Guest | first name, last name, email, phone (optional) |
| Booking | arrival date, departure date, booked price per night, status |
| Payment | amount, method (credit card / PayPal), paid at |
| Refund | amount, status (done / failed) |
| Cancellation | cancelled at, cancelled by (guest / owner), reason, fee |
| Invoice | invoice number, total including taxes and fees, issued at |
| Review | text, stars, owner's reply |
| Customer support | name |

## Invariants

<!-- Rules that must always hold, and which concept is responsible for each. -->

| Rule | Responsible concept |
|---|---|
| A booking's departure date is after its arrival date. | Booking |
| A room cannot be booked twice for overlapping nights (D-07). | Room |
| Free cancellation is only possible until 48 hours before arrival; after that the first night is charged and the rest refunded (D-01). | Cancellation |
| A booking keeps the price it was booked at, even if the owner changes the rate later (D-09). | Booking |
| A booking is only confirmed after successful payment (D-03). | Booking |
| An owner can only cancel a booking more than 14 days before arrival and must give a reason (D-04). | Cancellation |
| A refund is never more than the amount the guest paid. | Refund |
| A guest has a first name, a last name and an email address (D-08). | Guest |
| Only customer support can remove a review; the owner cannot (D-12). | Review |
