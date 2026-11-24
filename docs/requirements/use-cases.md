# Use Cases

> AI-assisted (Claude): Claude coached by asking questions and offering multiple-choice options; it formatted my chosen answers into the template. Actors, use cases, flows and choices decided by Krish.
>
> AI-assisted (Claude): after the stakeholder session, Claude updated the use cases with the decisions from the decision log, replaced UC-03 (owner approval was dropped by D-06) with "Change a booking", and filled in the related requirements. Reviewed by Urbee — checked every change against the decision log.
>
> AI-assisted (Claude): on 24.11 Claude entered the corrections from our lecturer's feedback (late-cancellation cost, owner's reason and support call, payment methods, booked price) with the decision numbers.

![Use case diagram](use-case-diagram.png)

## UC-01 — Book a room

| Field | |
|---|---|
| Related requirements | FR-03, FR-04, FR-05, FR-06, FR-07, FR-08, FR-09, FR-10 |
| Initiating actor | Guest |
| Actor's goal | Secure a room in a hotel for the chosen dates |
| Participating actors | Payment Provider |
| Preconditions | The hotel and its rooms are offered on the platform. The guest has found a room (UC Search for a room). |
| Postconditions | A confirmed booking with a fixed room number exists for the guest's dates (D-06, D-21). The booking keeps the price it was booked at, even if the owner changes the price later (D-09). The guest has paid online (D-03). The room is no longer available to others for these dates (D-07). |

**Main success scenario**

1. → Guest selects a suitable room and the stay dates (arrival and departure).
2. ← System shows the room details (Wi-Fi, parking, …) and the total price including all taxes and fees.
3. → Guest enters first name, last name and email address, and optionally a phone number (D-08).
4. → Guest chooses to pay online by credit card or PayPal and enters payment data (D-03).
5. ← System sends the payment to the Payment Provider, which confirms it.
6. ← System confirms the booking immediately and assigns a fixed room number (D-06, D-21).
7. ← System shows the confirmation and sends a receipt to the guest.

**Alternate flow A — Payment fails** (branches at step 5)

- 5a. ← Payment Provider declines the payment; system informs the guest. No booking is made and the room is not reserved (D-03).
- 5b. → Guest chooses another payment method; continue at step 4.

**Alternate flow B — Room no longer available** (branches at step 4)

- 4a. ← Before payment, system finds the room was booked by someone else meanwhile and informs the guest. Nothing is charged (D-07).
- 4b. → Guest selects another room; continue at step 1.

**Alternate flow C — Dates in the past** (branches at step 1)

- 1a. ← System rejects the arrival date because it is in the past and asks for valid dates.
- 1b. → Guest enters new dates; continue at step 1.

## UC-02 — Cancel a booking

| Field | |
|---|---|
| Related requirements | FR-11, FR-12, FR-17, FR-18, FR-25 |
| Initiating actor | Guest |
| Actor's goal | Call off the booking and get back as much money as the rules allow |
| Participating actors | Payment Provider, Owner |
| Preconditions | The guest has a confirmed booking whose stay has not yet started. |
| Postconditions | The booking is cancelled. The room is available for other guests again for these dates. The full amount is refunded, or for a late cancellation the amount minus the first night (D-01). |

**Main success scenario**

1. → Guest opens his booking and chooses to cancel it.
2. ← System shows that the cancellation is free because it is more than 48 hours before the arrival date, and shows the full refund amount (D-01).
3. → Guest confirms the cancellation.
4. ← System sets the booking to cancelled and makes the room available again for these dates.
5. ← System asks the Payment Provider to refund the full amount.
6. ← System informs the Owner about the cancellation.
7. ← System sends the guest a cancellation confirmation.

**Alternate flow A — Late cancellation** (branches at step 2)

- 2a. ← System shows that free cancellation is no longer possible because the arrival is less than 48 hours away (D-01). No exception is made, not even for illness (D-02). System shows that the first night is charged and the rest is refunded (D-01).
- 2b. → Guest confirms anyway (continue at step 3; at step 5 the system refunds the amount minus the first night) or aborts; the booking stays confirmed.

**Alternate flow B — Refund fails** (branches at step 5)

- 5a. ← Payment Provider reports an error.
- 5b. ← System keeps the booking cancelled and flags the refund for Kojenwerk Staff to handle.

**Alternate flow C — Owner cancels the booking** (initiated by Owner)

- C1. → Owner chooses to cancel a guest's booking more than 14 days before the arrival date and enters a reason (D-04).
- C2. ← System sets the booking to cancelled, informs the guest automatically and refunds the full amount, without any upper limit (D-05, D-10).
- C3. ← If the arrival is 14 days or less away, the system does not let the owner cancel and tells the owner to call Kojenwerk support; the booking stays confirmed (D-04).

## UC-03 — Change a booking

| Field | |
|---|---|
| Related requirements | FR-07, FR-13, FR-14 |
| Initiating actor | Guest |
| Actor's goal | Move the booking to other dates or another room without cancelling it |
| Participating actors | Payment Provider |
| Preconditions | The guest has a confirmed booking, and the arrival date is more than 48 hours away (D-19). |
| Postconditions | The booking has the new dates or room. The price difference has been charged or refunded (D-19). The old dates or room are available to others again. |

**Main success scenario**

1. → Guest opens his booking and chooses to change it.
2. → Guest selects new dates or another room.
3. ← System checks that the new room is free for the new dates (D-07) and shows the new price and the difference to the old price.
4. → Guest confirms the change.
5. ← The new price is higher: system asks the Payment Provider to charge the difference, which confirms it (D-19).
6. ← System updates the booking with the new dates or room and the room number, and makes the old dates or room available again.
7. ← System sends the guest a confirmation of the change.

**Alternate flow A — New price is lower** (branches at step 5)

- 5a. ← System asks the Payment Provider to refund the difference to the guest (D-19).
- 5b. Continue at step 6.

**Alternate flow B — New room or dates not available** (branches at step 3)

- 3a. ← System informs the guest that the room is not free for the new dates.
- 3b. → Guest selects other dates or another room (continue at step 3) or aborts; the booking stays unchanged.

**Alternate flow C — Too late to change** (branches at step 1)

- 1a. ← The arrival is less than 48 hours away; system informs the guest that the booking can no longer be changed (D-19).
- 1b. The booking stays unchanged.

**Alternate flow D — Payment of the difference fails** (branches at step 5)

- 5a. ← Payment Provider declines the payment; system informs the guest.
- 5b. → Guest chooses another payment method (continue at step 5) or aborts; the booking stays unchanged.
