# Patient Cancellation Alerts Implementation Plan

> **For agentic workers:** Implement this plan task-by-task in the current workspace.

**Goal:** Improve patient alert readability and add a cancellation notification that opens appointment details with credit and rebooking actions.

**Architecture:** Extend the existing patient alert data and shared appointment details renderer in `patient-app.html`. Keep this as a static front-end prototype using current navigation methods.

**Tech Stack:** Single-file HTML, CSS, and JavaScript.

**Spec:** `docs/superpowers/specs/2026-10-25-patient-cancellation-alerts-design.md`

## Global Constraints

- Preserve full notification messages while reducing their visual size.
- Reuse Appointment Details for the cancelled state and support either pre-visit state.
- Treat the cancelled booking amount as an equal amount of reusable BDT credit.
- Keep doctor-side schedule clearing and backend/payment behavior out of scope.

## Review Focus

- A read cancellation alert remains readable and has no unread dot.
- Cancellation notice and credit information appear whether or not pre-visit details are submitted.
- “Find a doctor” and “Other dates” land on their intended existing booking flows.

---

### Task 1: Alerts and cancellation appointment flow

**Files:**
- Modify: `patient-app.html`

**Implementation:**
- Shorten every alert body and refine row/group spacing; show only the two older read rows as muted, remove dots, and distinguish cancellations with red text/icon styling on a transparent row.
- Add a cancelled-booking alert and prototype visit with an explicit BDT price.
- Extend shared appointment details to show a pale-red cancellation notice; put a compact background-free equal-value credit line above its actions.
- Add a framed low-emphasis **Find a doctor** action and primary **Reschedule** action using existing Discover and same-doctor booking paths; return to Alerts from cancellation details.

**Verification:**
- Inspect the changed HTML and exercise the cancellation alert, read state, and both navigation actions in the patient prototype if the browser preview is available.
- Do not add or run automated tests unless the user requests testing.
