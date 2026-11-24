# Requirements — Hotel Booking Platform

> AI-assisted (Claude): drafted the requirement tables, acceptance criteria and traceability matrix from our use cases, our open questions and our decision log from the stakeholder session.
>
> Reviewed by Urbee — checked every requirement against our use cases and our session notes.
>
> AI-assisted (Claude): on 24.11 Claude entered the corrections from our lecturer's feedback (use case IDs as sources, decided numbers in NFR-01, NFR-03, NFR-04, NFR-07, late-cancellation cost in AC-11.2, support call in AC-17.2, FR-25). The new non-happy-path criteria AC-04.3, AC-16.3, AC-18.3 and the criteria of FR-25 were written by Krish.

## 1. Introduction

Kojenwerk GmbH, a Hamburg start-up, runs a booking platform for about 40 small partner hotels, guesthouses and hostels in Hamburg and northern Germany. Today most bookings arrive by phone and email. This document specifies what the new platform must do (functional requirements) and how well it must do it (non-functional requirements).

The requirements are based on our use cases, the two stakeholder emails, the domain brief and the decisions Jan Petersen (CEO) made in the stakeholder session on 05.11.2026.

## 2. Stakeholders and users

| Stakeholder / user | Role | Main interest |
|---|---|---|
| Jan Petersen | CEO of Kojenwerk | Decides between conflicting wishes |
| Malte Hansen | Head of Partner Hotels | Speaks for the hotel owners: full rooms, control over bookings and prices |
| Selin Aydın | Head of Guest Experience | Speaks for guests and customer service: reliable bookings, little data, accessibility |
| Guest | User | Finds, books, pays for, changes and cancels rooms; writes reviews |
| Owner | User | Manages hotels, rooms and prices; sees and cancels bookings; replies to reviews |
| Customer support | User | Helps guests and owners, e.g. removes spam or racist reviews |

## 3. Use cases

See [use cases](use-cases.md) and the [decision log](decision-log.md).

## 4. Functional requirements

| ID | Requirement | Source | Acceptance criteria |
|---|---|---|---|
| FR-01 | A guest shall be able to search for available rooms by city and date range. | UC-04 | **AC-01.1** Given a room in Hamburg that is free from 10.03 to 12.03, when a guest searches Hamburg for 10.03–12.03, then the room is in the result. <br>**AC-01.2** Given the same room is booked on 11.03, when a guest searches Hamburg for 10.03–12.03, then the room is not in the result. |
| FR-02 | A guest shall be able to limit the search result to wheelchair-accessible rooms. | UC-04 | **AC-02.1** Given hotel A has a wheelchair-accessible room free from 10.03 to 12.03, when a guest searches Hamburg for 10.03–12.03 with the filter "wheelchair-accessible", then the room is in the result. <br>**AC-02.2** Given hotel B has only rooms that are not wheelchair-accessible, when the guest uses the same search with the filter, then no room of hotel B is in the result. |
| FR-03 | A guest shall be able to book an available room for a chosen date range. | UC-01 | **AC-03.1** Given room 12 is free from 10.03 to 12.03, when a guest books it for 10.03–12.03 and pays, then the booking exists for 2 nights. <br>**AC-03.2** Given a guest enters arrival 12.03 and departure 10.03, when they try to book, then the booking is rejected with a message that departure must be after arrival. |
| FR-04 | Before payment, the system shall show the guest the total price of the stay including all taxes and fees. | UC-01 | **AC-04.1** Given a room costs 100 € per night plus Hamburg tourism tax, when a guest selects 2 nights, then the price shown before payment includes both nights and the tourism tax. <br>**AC-04.2** Given the guest has paid the shown price, when the stay ends, then the guest is not asked to pay any additional fee for that booking. <br>**AC-04.3** *(to be written by Krish — not the happy path)* |
| FR-05 | The system shall create a booking only after the guest has paid online successfully. | UC-01, D-03 | **AC-05.1** Given a guest has chosen a free room, when the online payment succeeds, then the booking is created. <br>**AC-05.2** Given a guest has chosen a free room, when the online payment is declined, then no booking is created and the room stays free. |
| FR-06 | The system shall confirm a booking immediately after successful payment, without approval by the owner. | UC-01, D-06 | **AC-06.1** Given a free room, when the guest's payment succeeds, then the booking status is "confirmed" without any action by the owner. <br>**AC-06.2** Given the owner has not logged in for a week, when a guest books and pays, then the booking is still confirmed immediately. |
| FR-07 | The system shall reject a booking or a booking change for a room that is already booked for at least one of the requested nights. | UC-01, UC-03, D-07 | **AC-07.1** Given room 12 is booked for 11.03, when a second guest tries to book room 12 for 10.03–12.03, then the booking is rejected. <br>**AC-07.2** Given room 12 is booked for 10.03–12.03, when a second guest books room 12 for 12.03–14.03, then the booking is accepted (the first guest checks out on 12.03). |
| FR-08 | The system shall assign a fixed room number to a booking immediately after successful payment. | UC-01, D-21 | **AC-08.1** Given a guest books a double room, when the payment succeeds, then the booking confirmation shows one room number. <br>**AC-08.2** Given the payment is declined, when the guest looks at the booking page, then no room number is shown or reserved. |
| FR-09 | The system shall calculate the price of a booking with the room price valid at the moment of booking. | UC-01, D-09 | **AC-09.1** Given the owner changes the price of room 12 from 100 € to 120 € per night at 10:00, when a guest books 1 night at 10:05, then the guest pays 120 €. <br>**AC-09.2** Given a guest opened the room page at 09:55 when the price was 100 €, when the owner changes the price to 120 € at 10:00 and the guest books at 10:05, then the guest is shown 120 € before paying. |
| FR-10 | To book, the system shall require first name, last name and email address, and shall accept the phone number as optional. | UC-01, D-08 | **AC-10.1** Given a guest enters first name, last name and email but no phone number, when they book, then the booking is accepted. <br>**AC-10.2** Given a guest leaves the email address empty, when they try to book, then the booking is rejected with a message that the email address is required. |
| FR-11 | A guest shall be able to cancel a booking free of charge up to 48 hours before the arrival date; a later cancellation shall cost the first night. | UC-02, D-01 | **AC-11.1** Given a confirmed booking with arrival on 20.03, when the guest cancels on 17.03, then the guest gets the full amount back. <br>**AC-11.2** Given a confirmed booking with arrival on 20.03, when the guest cancels on 19.03, then the free cancellation is not offered, the first night is charged and the rest of the amount is refunded. |
| FR-12 | The system shall apply the cancellation deadline to every guest without exceptions. | UC-02, D-02 | **AC-12.1** Given a booking with arrival on 20.03, when the guest cancels on 19.03 and gives illness as the reason, then the result is the same as without a reason. <br>**AC-12.2** Given the same booking, when customer support is asked to make an exception for illness, then the system offers no option to override the deadline. |
| FR-13 | A guest shall be able to change a booking to other dates or another room up to 48 hours before the arrival date. | UC-03, D-19 | **AC-13.1** Given a booking with arrival on 20.03 and room 12 free from 22.03 to 24.03, when the guest changes it on 15.03 to 22.03–24.03, then the booking has the new dates. <br>**AC-13.2** Given a booking with arrival on 20.03, when the guest tries to change it on 19.03, then the change is rejected. |
| FR-14 | When a guest changes a booking, the system shall charge the price difference if the new price is higher and refund it if the new price is lower. | UC-03, D-19 | **AC-14.1** Given a booking that cost 200 €, when the guest changes it to a stay that costs 260 €, then the guest is charged 60 €. <br>**AC-14.2** Given a booking that cost 200 €, when the guest changes it to a stay that costs 150 €, then the guest is refunded 50 €. |
| FR-15 | A guest shall be able to extend a booking during the stay. | D-20 | **AC-15.1** Given a guest is staying in room 12 until 12.03 and room 12 is free on 12.03, when the guest extends by 1 night on 11.03, then the stay ends on 13.03 and the guest pays for the extra night. <br>**AC-15.2** Given room 12 is booked by another guest from 12.03, when the guest tries to extend, then the extension is rejected. |
| FR-16 | The system shall not refund a booking when the guest does not arrive (no-show). | D-18 | **AC-16.1** Given a confirmed booking of 300 € for 10.03–12.03, when the guest does not arrive, then no money is refunded. <br>**AC-16.2** Given the same guest asks for a refund on 11.03 because they did not arrive, when the request is processed, then no money is refunded. <br>**AC-16.3** *(to be written by Krish — not the happy path)* |
| FR-17 | An owner shall be able to cancel a booking up to 14 days before the guest's arrival date. | UC-02, D-04 | **AC-17.1** Given a booking with arrival on 30.03, when the owner cancels it on 10.03, then the booking is cancelled. <br>**AC-17.2** Given a booking with arrival on 30.03, when the owner tries to cancel it on 25.03, then the cancellation is rejected and the owner is told to call Kojenwerk support. |
| FR-18 | When an owner cancels a booking, the system shall refund the full amount to the guest, without any upper limit. | UC-02, D-05, D-10 | **AC-18.1** Given a booking that cost 450 €, when the owner cancels it, then the guest is refunded 450 €. <br>**AC-18.2** Given a booking that cost 6,000 €, when the owner cancels it, then the guest is refunded 6,000 € (no maximum). <br>**AC-18.3** *(to be written by Krish — not the happy path)* |
| FR-19 | An owner shall be able to change the price of their rooms at any time. | UC-07, D-09 | **AC-19.1** Given an owner of hotel A, when they change the price of a room in hotel A to 120 €, then new searches show 120 €. <br>**AC-19.2** Given an owner of hotel A, when they try to change a price in hotel B, which they do not own, then the change is rejected. |
| FR-20 | An owner shall be able to manage several hotels with one account. | UC-06, D-22 | **AC-20.1** Given an owner has hotels A and B, when they log in, then they can manage both hotels without logging in again. <br>**AC-20.2** Given an owner has only hotel A, when they log in, then hotel B of another owner is not shown to them. |
| FR-21 | A guest shall be able to write a review of a hotel. | D-11 | **AC-21.1** Given a logged-in guest, when they write a review of hotel A, then the review is shown on hotel A's page. <br>**AC-21.2** Given a visitor who is not logged in, when they try to write a review, then the review is rejected. |
| FR-22 | An owner shall be able to reply to a review of their hotel. | D-11 | **AC-22.1** Given a review of hotel A, when the owner of hotel A replies, then the reply is shown under the review. <br>**AC-22.2** Given the owner does not reply, when someone views hotel A, then the review is still shown. |
| FR-23 | The system shall not allow an owner to delete a review. | D-12 | **AC-23.1** Given a review of hotel A, when the owner of hotel A tries to delete it, then the review is not deleted. <br>**AC-23.2** Given the same review, when the owner looks at their review page, then no delete option is shown. |
| FR-24 | Customer support shall be able to remove a review that contains spam or racist content. | D-12 | **AC-24.1** Given an owner reports a review containing racist insults, when customer support removes it, then it is no longer shown. <br>**AC-24.2** Given an owner reports a review that is critical but contains no spam or racist content, when customer support checks it, then the review stays published. |
| FR-25 | When an owner cancels a booking, the system shall require the owner to enter a reason. | UC-02, D-04 | **AC-25.1** *(to be written by Krish)* <br>**AC-25.2** *(to be written by Krish — not the happy path)* |

## 5. Non-functional requirements

| ID | Category | Requirement | Metric | Target | How it is measured | Source |
|---|---|---|---|---|---|---|
| NFR-01 | Performance | Search results are returned quickly at peak load. | Share of search requests answered within 1 s | ≥ 90 % at 3,000 concurrent users | Load test against the search function with 3,000 simulated concurrent users | D-13, D-14 |
| NFR-02 | Capacity | The system serves the expected number of users at peak time. | Number of concurrent users served without failed requests | 3,000 now; 10,000 later | Load test with simulated concurrent users | D-13 |
| NFR-03 | Availability | The system is available almost all the time. | Share of time per calendar month in which the system is available | ≥ 99.5 % | Automated availability monitoring, monthly report | D-15 |
| NFR-04 | Availability | Planned maintenance happens only in the agreed time window. | Planned maintenance time outside Tuesdays 02:00–04:00 | 0 minutes | Maintenance log compared with availability monitoring, monthly report | D-15 |
| NFR-05 | Responsibility — personal data | Only the guest data needed to book and contact the guest is stored. | Personal data fields stored per guest | First name, last name, email address; phone number only if the guest enters it | Review of all stored data fields; export of a test guest's data | D-08 |
| NFR-06 | Responsibility — personal data | Data of guests without a booking is deleted after the agreed time. | Time from the guest's last activity until deletion | 2 years | Test account whose last activity is 2 years and 1 day ago is no longer found | D-16 |
| NFR-07 | Responsibility — personal data | Data of guests with bookings is deleted after the agreed time (booking and invoice records excluded, see open points). | Time from the guest's last check-out until deletion | 3 years | Test account whose last check-out is 3 years and 1 day ago is no longer found | D-16 |
| NFR-08 | Responsibility — fairness | Cancellation and refund rules treat all guests the same. | Share of test cancellations whose refund matches the rules in D-01, D-02 and D-05, across different hotels, payment methods and guest profiles | 100 % | Test set of cancellations with the same timing for different guests and hotels; compare refunds | D-01, D-02, D-05 |
| NFR-09 | Responsibility — accessibility | Guests who use a screen reader can search, book, pay and cancel. | Number of WCAG 2.1 level AA failures in the guest booking flow | 0 | Accessibility audit of the flow (automated check + manual test with a screen reader such as VoiceOver) | D-24; Barrierefreiheitsstärkungsgesetz (BFSG) / EN 301 549; Selin's email (point 7) |

**Open points for the NFRs** (no source yet, so no target was invented):

- **NFR-02:** by when must the system serve 10,000 users?
- **NFR-03/04:** what should guests see or be able to do while the system is down (Q13)?
- **NFR-07:** how long booking and invoice records are kept was left to Kojenwerk's accountant (D-17); German tax law may require longer than 3 years. Open question Q16, so no number is given here.
- **NFR-08 (fairness risks we found):** paying only online (D-03) can exclude guests without a credit card or online payment account; no exceptions even for illness (D-02) and no refund for no-shows (D-18) can hit guests in emergencies hard. These are open questions for Jan, not decisions we can take.
- **NFR-09:** Kojenwerk has nine employees. Very small companies may be exempt from the BFSG, so whether the law applies must be checked. Selin's email still asks for screen-reader support.
- **Security** (Malte: "it has to be secure") and **mobile use** (Selin: guests book "on their phones") have no measurable target yet.

## 6. Traceability matrix

Rows marked *(diagram only)* are use cases in our use case diagram that are not described in detail. The IDs are the ones in the diagram.

| | FR-01 | FR-02 | FR-03 | FR-04 | FR-05 | FR-06 | FR-07 | FR-08 | FR-09 | FR-10 | FR-11 | FR-12 | FR-13 | FR-14 | FR-15 | FR-16 | FR-17 | FR-18 | FR-19 | FR-20 | FR-21 | FR-22 | FR-23 | FR-24 | FR-25 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| UC-04 Search for a room *(diagram only)* | x | x |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| UC-01 Book a room |  |  | x | x | x | x | x | x | x | x |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| UC-02 Cancel a booking |  |  |  |  |  |  |  |  |  |  | x | x |  |  |  |  | x | x |  |  |  |  |  |  | x |
| UC-03 Change a booking |  |  |  |  |  |  | x |  |  |  |  |  | x | x |  |  |  |  |  |  |  |  |  |  |  |
| UC-07 Set room prices *(diagram only)* |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | x |  |  |  |  |  |  |
| UC-06 Manage hotel and rooms *(diagram only)* |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | x |  |  |  |  |  |

**Gaps found and how we addressed them:**

- **Every described use case has at least one FR:** UC-01 → FR-03 to FR-10, UC-02 → FR-11, FR-12, FR-17, FR-18, FR-25, UC-03 → FR-07, FR-13, FR-14. No gap.
- **UC-03 replaced:** our original UC-03 "Accept or decline a booking request" became obsolete because Jan decided that bookings are confirmed instantly (D-06). We replaced it with "Change a booking" (D-19) and removed "Accept or decline a booking request" from the use case diagram.
- **FRs without a use case:** FR-15 (extend a stay), FR-16 (no-show) and FR-21 to FR-24 (reviews) come only from stakeholder decisions (D-11, D-12, D-18, D-20). They are needed because Jan decided them, but no use case in our diagram covers them yet. They should be added as use cases ("Extend a stay", "Write a review", "Reply to a review", "Remove a review").
- **Use cases without an FR:** UC-05 "View my booking", UC-08 "View bookings", UC-09 "Look up a booking" and UC-10 "Handle booking for guest" have no FR yet. What staff may do for a guest is still open (Q9).

## 7. Decision log

See [decision log](decision-log.md).
