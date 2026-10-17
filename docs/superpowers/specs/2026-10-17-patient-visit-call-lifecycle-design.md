# Patient Visit Call Lifecycle Design

## Purpose

Redesign the patient Visits cards and connect them to a coherent simulated consultation lifecycle. Preserve the existing doctor, appointment, and pre-visit information before the call, then make the call, rejoin, summary preparation, and prescription-issued states easy to understand.

## Product Direction

- Follow the existing Onu visual system: white canvas, Urbanist headings, DM Sans supporting text, Phosphor icons, forest green actions, sage selection accents, and restrained borders.
- Use the doctor app's call UI as the interaction reference for the active call screen.
- Keep the visit card white, spacious, and minimally layered. Serial and status stay as plain information in the card, never as a nested card.
- Give the pre-visit action its own subtle, full-width, 44px minimum tap target.
- Keep prototype simulation controls outside the phone mockup in a vertically stacked panel to the left of the device, with a clear gap between each control. At narrow viewport widths, stack this panel above the phone so controls remain usable.

## Visit Lifecycle

The appointment shown as `mahim-upcoming` progresses through these patient-facing states:

1. **Scheduled**
   - The date is shown once above the card.
   - The card shows video or in-person mode icon, doctor name and designation, specialty, appointment start time, serial, `Scheduled` status, and the pre-visit action.
2. **Doctor started**
   - The card keeps the serial and appointment time and updates status to `Doctor started`.
3. **Incoming auto-call**
   - When the existing queue simulator reaches the patient's turn, show the incoming-call screen with `Receive & Join` and `Decline` actions.
   - Declining opens the existing options to reschedule with Dr. Mahim, rebook with another doctor, or stay on the incoming-call screen.
4. **Ongoing call**
   - Receiving the call opens the consultation screen with the doctor video, patient preview, elapsed duration, and a single `Back to Visits` action.
   - The call is connected to the doctor; do not show a waiting-for-doctor message. Leaving the call view does not end or reset it.
5. **Ongoing call in Visits**
   - Hide the appointment time, serial, and pre-visit action while the call is active.
   - Show `Ongoing call` at the left and a prominent `Rejoin call` button at the right in one balanced row, with comfortable vertical spacing.
   - Rejoining opens the same waiting/call view and preserves elapsed call time.
6. **Preparing visit summary**
   - The developer simulation panel includes a `Doctor Ends Call` control. Activating it simulates the doctor ending the call, stops the call-duration timer, returns to Visits, and shows a completed-style card with doctor, designation/specialty, visit date/time, a `Completed` label, and `Preparing your visit summary…` with a non-blocking progress indicator.
   - Replace the time in the card's top row with the `Completed` status so the card does not leave an empty time slot. Do not show serial or pre-visit action in this state.
7. **Prescription issued**
   - After a 5 second prototype processing delay, automatically move the appointment from Upcoming to the top of Past Visits and show `Rx Issued`.
   - Use the same spacious white card language for the completed entry: mode icon, doctor and specialty, clear Rx-issued status, and chevron affordance; keep the full visit date as the group heading.
   - Opening the completed appointment continues to use the existing visit details page.

## Completed Visit Details and Notification

- When the prescription is issued, show a tappable, Android-style system notification with the Onu Health identity, `Prescription issued`, and a short message that Dr. Mahim sent the prescription. Tapping it opens the completed visit details.
- Redesign the details header with a clear doctor identity row and a separate date/mode context row.
- Keep the prescription preview and consultation note in the patient details. Do not expose an audio playback control; only the doctor app may access consultation audio.
- Populate the simulated visit with a believable sample consultation note so the notes section has realistic content.

## State and Transition Rules

- Keep one explicit patient visit lifecycle state for the selected upcoming visit: `scheduled`, `doctor_started`, `incoming_call`, `ongoing_call`, `preparing_summary`, or `rx_issued`.
- The queue simulator's `turn` action opens the incoming-call screen and sets `incoming_call`. Receiving it transitions to `ongoing_call` and starts the elapsed call timer.
- `Back to Visits` and `Rejoin call` change only the visible page. They do not change lifecycle state or restart timers.
- Call duration continues until `Doctor Ends Call` is activated in the external simulation panel. Rejoining does not reset it; call completion occurs once and cannot be reversed.
- The summary timer is started once when the call ends. When it completes, update the appointment to completed and activate Past Visits.
- Provide a simulation reset control to restore the visit to the booked state and clear outstanding timers.
- Existing completed visits remain in the list. The transitioned appointment appears as a new completed visit with its own appointment date and Rx status.
- Keep call and prescription transitions scoped to the patient prototype. The current doctor and patient prototypes are standalone HTML documents with no cross-page runtime channel, so the doctor-side end-call and prescription submission are represented by deterministic patient-side simulation timers.

## Interaction and Accessibility

- The visit details region is keyboard operable and exposes an accessible name containing the doctor and appointment mode.
- The pre-visit and rejoin actions are real buttons with visible focus, at least 44px height, and do not trigger the visit-details action.
- The incoming-call screen exposes `Receive & Join` and `Decline`. The decline flow offers rescheduling, rebooking, and staying on the incoming-call screen. The connected call screen has one clearly labeled `Back to Visits` action and no patient end-call action.
- Call status and summary updates are announced through polite live regions without stealing focus.
- Respect reduced-motion preferences for spinner, pulsing, and page transitions.

## Files and Scope

- Modify `patient-app.html`: visit-card presentation, patient call waiting view, lifecycle state and timers, transitions among Upcoming, call, summary, and Past Visits, and the left-side simulation control panel layout.
- Do not change `doctors-app.html`; use its existing call screen as a visual reference. No backend or cross-document synchronization is added.

## Acceptance Criteria

- Selecting the existing patient-turn simulator opens an incoming-call screen with receive and decline actions. Decline presents the reschedule, rebook, and stay options.
- Receiving the call opens the connected consultation screen; it does not show a waiting-for-doctor message.
- A left-side `Doctor Ends Call` simulation button ends the call; the patient sees summary preparation and then automatically sees the Rx-issued visit in Past Visits.
- Back to Visits leaves the call active and the appointment card shows only `Ongoing call` plus `Rejoin call`, without time, serial, or pre-visit action.
- Rejoin returns to the same active call without resetting its timer.
- The simulated call end returns the patient to Visits and displays `Completed` in the time position alongside `Preparing your visit summary`.
- Five seconds later, the same appointment is listed in Past Visits with `Rx Issued` and opens the existing appointment details page.
- Issuing the prescription displays a tappable Android-style Onu Health notification that opens the completed visit details.
- Completed visit details have a clearer doctor/date header, readable sample consultation note, and no patient audio playback control.
- The completed visit uses a spacious white card with a mode icon, doctor/specialty, Rx-issued status, and clear tap-through affordance.
- The scheduled card retains mode, doctor name/designation, specialty, time, serial, status, and a subtle, accessible pre-visit action.
