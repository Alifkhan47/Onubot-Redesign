# Patient Cancellation Alerts Design

## Intent

Improve the patient Alerts list readability and let a patient open a doctor-cancelled appointment notification into appointment details that clearly explain the cancellation and booking credit, then offer concise paths to book again.

## Goals

- Reduce alert body text size slightly while preserving legibility and complete message text; improve separation between groups and rows.
- Show the two older read alerts with muted text and icon styling rather than an unread green dot; keep recent alerts visually active.
- Remove notification dots. Distinguish cancellation alerts with red icon/title styling while keeping their row background transparent.
- Shorten notification body copy across all alert types instead of reducing the text size further.
- Reuse the existing Appointment Details page for cancelled appointments, regardless of pre-visit submission state.
- Show a subtle red cancellation notice, a compact background-free booking credit line above the actions, and actions to find another doctor or reschedule with the same doctor.
- Make clear that the credit remains available if the patient leaves without booking.

## Non-goals and constraints

- No backend, payment, or credit-balance implementation; this is a static prototype interaction.
- No change to the doctor app schedule-clearing behavior, which already shows affected patients were notified.
- Keep the existing single-file HTML/CSS/JavaScript structure and existing appointment details navigation.

## Approaches

1. **Extend the shared Appointment Details screen (recommended; assumed).** Mark the cancelled visit in the prototype data and conditionally render the cancellation notice, credit message, and rebooking actions in the existing screen. This preserves the current layout and pre-visit behavior.
2. **Create a dedicated cancellation details screen.** This separates the content but duplicates the doctor, date, and appointment context already displayed by the shared details screen.

The shared details screen is selected as the working assumption because the current alert routing already opens it and it can represent both filled and unfilled pre-visit states.

## Copy and behavior

- Alert title: “Appointment cancelled”; alert body identifies the doctor and appointment and notes that the booking amount is available as credit.
- Cancellation notice: “Appointment cancelled”.
- Credit line: “৳{amount} credit added” with “Available for a future booking.” Amount matches the cancelled booking price.
- Actions: **Find a doctor** is a framed low-emphasis action that opens Discover; **Reschedule** is the primary action and opens the same doctor’s booking page.
- Submitted pre-visit details may remain visible as read-only context; when none were submitted, omit that section. Cancellation status is always shown, and no pre-visit actions are offered for a cancelled appointment.
- When a cancellation alert opens Appointment Details, its back button returns to Alerts.

## Visual direction

Use a low-emphasis red text treatment on a subtle red background without a border, or with a visually unstroked surface. Tighten alert row spacing while keeping alert text concise and readable. Read alerts use softer neutral foregrounds without dots; cancellation rows keep a transparent background and use red icon/title styling.

## Open implementation choices

Exact demo booking amount and rebooking navigation target should follow the existing patient booking flows. If an exact amount is not already stored, use an explicit prototype field on the cancelled visit rather than inferring from unrelated visit data.
