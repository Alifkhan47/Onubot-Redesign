# Patient Visit Call Lifecycle Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Implement the patient visit lifecycle from scheduled appointment through auto-call, rejoin, summary preparation, and prescription-issued history.

**Architecture:** Keep the prototype self-contained in `patient-app.html`. Add one explicit lifecycle state and timer set for the active appointment, render the appointment card from that state, and reuse the existing incoming-call and consultation layers. The external simulation panel lets the presenter open the incoming call and simulate the doctor ending it; a short processing timer then moves the visit to Rx Issued.

**Tech Stack:** HTML5, CSS3, vanilla JavaScript, Phosphor icons.

**Spec:** `docs/superpowers/specs/2026-10-17-patient-visit-call-lifecycle-design.md`

## Global Constraints

- Keep the patient prototype self-contained; do not add a backend or cross-document messaging.
- The patient must receive or decline the incoming call. The active call lasts until the presenter activates `Doctor Ends Call`; summary preparation lasts 5 seconds.
- The patient can leave the call view without ending the call and can rejoin while the call remains active.
- The incoming call has Receive & Join and Decline actions, and the decline flow retains its reschedule, rebook, and stay options. The connected call has no patient end-call action.
- Simulation controls remain outside the phone mockup, stacked vertically to its left on wide screens and above the phone on narrow screens.
- Do not commit or push changes.

## Review Focus

- Call duration continues while the patient is on Visits; verify only the presenter control ends it, once.
- The pre-visit button does not navigate into appointment details; verify event propagation and keyboard operation.
- Appointment moves to Past Visits once; verify existing historical cards remain and details open in completed mode.
- Narrow viewports keep the simulation controls and phone usable without horizontal overflow.
- Reduced-motion preference suppresses nonessential spinner, pulse, and transition animation.

---

### Task 1: Add the patient visit lifecycle state and card rendering

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Produces: `patientVisitLifecycle`, with values `scheduled`, `doctor_started`, `ongoing_call`, `preparing_summary`, and `rx_issued`.
- Produces: `renderPatientVisitCardState()` to update the existing upcoming card without rebuilding its appointment data.
- Consumes: existing `visitsDb['mahim-upcoming']`, the date-grouped Upcoming/Past sections, and the active mode icon.

- [x] Add lifecycle state and timer handles beside the existing Visits controller state. Define the summary delay as a named constant: `5000` ms. Keep call duration as an elapsed-time counter only.
- [x] Implement `renderPatientVisitCardState()` so scheduled and doctor-started states show date, mode, doctor, specialty, time, serial, status, and pre-visit; ongoing call shows only status and a 44px `Rejoin call` button; preparing state shows visit date/time, `Completed`, and a polite live `Preparing your visit summary…` message.
- [x] Keep the appointment detail area keyboard-operable and make the entire non-action card area open details. Keep the pre-visit and rejoin controls as separate buttons that do not bubble into visit navigation; expose changing call/summary labels through polite live regions.
- [x] Connect the existing `setDemoSimulationState('pending'|'active')` branches to the lifecycle renderer and retain the current status labels `Scheduled` and `Doctor started`.
- [x] Add a reduced-motion rule for call spinner, pulse, and page transitions.
- [ ] Manually inspect Scheduled and Doctor started states at the phone mockup size and a narrow browser width.

### Task 2: Add incoming-call choices, connected call, Back to Visits, and Rejoin

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Consumes: `patientVisitLifecycle` and `renderPatientVisitCardState()` from Task 1.
- Produces: `startPatientAutoCall()`, `showPatientCallView()`, `backToVisitsFromCall()`, and `rejoinPatientCall()`.
- Reuses: existing `videoRoomView`, doctor visual assets, timer display, and Visits navigation.

- [x] Restyle the call view to show the doctor video area, centered waiting-for-doctor indicator and copy, elapsed call time, and a single `Back to Visits` action. Remove patient accept/decline and end-call actions from this auto-call path.
- [x] Make the existing queue simulator `turn` branch set state to `ongoing_call`, open the call view automatically, and start an elapsed-time interval without a call-end timeout.
- [x] Implement Back to Visits and Rejoin so they toggle the call view without resetting its elapsed timer. Hide time, serial, and pre-visit while the ongoing call card is shown.
- [ ] Manually verify that the `turn` simulation auto-opens the call, Back to Visits preserves the call, and Rejoin returns to it.

### Task 3: Simulate call completion, summary processing, and Rx Issued history

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Consumes: call state and timers from Task 2; existing `visitsDb` and `renderVisitDetailsContent()`.
- Produces: `finishPatientCall()` and `finishPatientSummaryPreparation()`.

- [x] Add a `Doctor Ends Call` control to the left-side simulation panel. It calls `finishPatientCall()` to clear the active call view, transition once to `preparing_summary`, navigate to Visits, and start the 5-second summary timer.
- [x] Implement `finishPatientSummaryPreparation()` to mark `mahim-upcoming` completed, insert it at the top of Past Visits with `Rx Issued`, hide it from Upcoming, and activate Past Visits. Use a spacious white card with mode icon, doctor/specialty, Rx status, and an accessible details affordance.
- [x] Ensure the completed entry opens the existing appointment details page as a completed visit and that existing past-visit entries remain intact.
- [ ] Manually verify the complete sequence from simulator `turn` through Rejoin, explicit `Doctor Ends Call`, summary preparation, automatic Past Visits selection, and Rx Issued detail navigation.

### Task 4: Place simulation controls left of the phone

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Consumes: existing `.external-sim-dock`, `.ext-sim-buttons`, and `.mockup-container`.
- Produces: a responsive prototype workspace containing the simulation control list and phone mockup.

- [x] Wrap the simulation dock and phone mockup in a workspace row. Stack the controls vertically with consistent button gaps and align them to the left of the phone on wide viewports.
- [x] At narrow widths, stack the simulation panel above the phone while preserving readable labels and touch targets.
- [x] Add a `Reset Visit Simulation` control that clears call/summary timers and restores Scheduled state, Upcoming selection, and default card content.
- [ ] Manually verify simulation states, call-end and reset controls, and inspect wide and narrow layouts for overlap, clipping, and horizontal scrolling.

### Task 5: Polish active-call card and completed visit details

**Files:**
- Modify: `patient-app.html`
- Update: `docs/superpowers/specs/2026-10-17-patient-visit-call-lifecycle-design.md`

- [x] Place `Ongoing call` and a prominent `Rejoin call` button in one horizontally balanced row with comfortable vertical spacing.
- [x] Replace patient audio playback with a doctor-only audio policy; remove the audio control from patient completed visit details.
- [x] Redesign the details header with a doctor identity row and a separate appointment context row.
- [x] Add believable sample consultation notes to the simulated completed visit.
- [x] Show a tappable Android-style prescription notification when Rx is issued; tapping it opens the completed visit details.
- [ ] Manually inspect the details screen, notification, and active-call card in a browser.

## Completion Check

- Run `git diff --check`.
- Open `patient-app.html` and manually walk through the full lifecycle and simulation layout.
- Confirm only `patient-app.html` and the approved spec/plan documents changed for this feature; do not commit or push.
