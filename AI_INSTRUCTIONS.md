# Onu App — AI Master Context & Project Blueprint
*Comprehensive Knowledge Base, Clinical Workflows, Architecture, and Autonomous Engineering Instructions for AI Pair Programmers & Human Developers.*

---

## 1. Executive Project Overview

**Onu App** is a next-generation clinical telemedicine and desk management platform built specifically for doctors and healthcare specialists.

### 1.1 Core Mission & Product Identity
* **Target User**: Busy doctors, middle-aged and senior healthcare professionals who require clean, friction-free scannability without cognitive overload or clutter.
* **Design Aesthetic**: Modern Western / European minimal healthtech standard inspired by **Wise, Uber, Hims, Alan Health, and Qonto**. Pure white canvas (`#FFFFFF`), gentle neutral surface cards (`#F6F8F9`), high-contrast typography, and single-purpose primary action buttons.
* **Tech Stack**: High-fidelity, self-contained single-page interactive web prototype in [`index.html`](file:///c:/Alif/Onu%20App%20Prototype/index.html) powered by vanilla HTML5, CSS3, and JavaScript, with Phosphor Icons and Google Fonts (`Urbanist` + `DM Sans`).

---

## 2. Core Clinical Mental Model & Strict Rules

When modifying or expanding any part of the app, any AI assistant or developer **MUST STRICTLY** adhere to these foundational principles:

### 2.1 Sequential Queue Flow (The "Doctor's Conveyor Belt")
1. **Consecutive Flow Only**: Doctors consult patients sequentially one by one (`Serial #1` -> `Serial #2` -> `Serial #3`...).
2. **No Random "Start Call" Buttons**: Doctors cannot randomly jump ahead or trigger calls for patients out of turn.
3. **Doctor Cannot "Recall" Skipped Patients**:
   - When a patient is absent or unresponsive during a video call, the doctor taps **Skip Patient**.
   - The doctor moves immediately to the next patient in queue.
   - The skipped patient is notified on their patient-side app. When the patient confirms they are back, the system **auto-slots them 3 turns ahead**. The doctor does not manually manage re-queuing.
4. **Queue & Video Call State Synchronization**: The patient shown on the Desk Hero Card, the Video Call Screen, and the All Appointments list must stay 100% synchronized in state and patient data.

### 2.2 Cognitive Decluttering & Minimal Demographic Standard
1. **Subtext Rule**: Subtext directly below patient names must strictly contain only:
   ```
   [Age] Yrs • [Gender]
   ```
   *Example*: `34 Yrs • Male` or `29 Yrs • Female`.
2. **No Redundant Repetition**: Never repeat type (`Initial`, `Follow Up`) or status (`Skipped`, `Prescribed`) in the subtext line if it is already indicated by a pill badge or dedicated status tag.
3. **No Nested Boxes ("No Boxes Inside Boxes Inside Boxes")**: Lists (prescriptions, investigations, appointments, documents) must use clean single-layer flat cards on the white page background.

### 2.3 Strict Destructive Action Confirmation
* **Never Delete Instantly**: Deleting a shift in the Schedule (`#pageSchedule`) or removing medications/investigations in Consultation Review (`#pageConsultationReview`) **must always** open the editorial confirmation bottom sheet (`#deleteConfirmModalSheet`).
* The sheet must display the exact item/shift name (e.g. `Delete Shift 1?`), provide context, and require explicit confirmation.

### 2.4 Fixed Sticky Action Docks
* Floating/sticky primary action bars (e.g. `Review & Finalize Rx`, `View Issued Prescription`, `Save Shift`) must be docked with a subtle blur background (`backdrop-filter: blur(12px)`) so they stay anchored at the viewport bottom and do not scroll away.

### 2.5 Dynamic Clinical Relevance Ordering (Appointment Details)
When rendering a patient's historical details in `#pageAppointmentDetails`:
* **If Prescribed (`prescribed`)**: The top priority is what was done in this visit!
  1. `Issued Prescription` (Top)
  2. `Consultation Notes` (Live AI transcription notes)
  3. `Pre-visit Details` (Patient intake summary)
  4. `Patient Documents` (Uploaded reports/images)
* **If In Queue / Upcoming**:
  1. `Pre-visit Details` (Top)
  2. `Patient Documents`
* **Pre-Visit Empty State Handling**:
  - If pre-visit intake was submitted: Show `Pre-visit Details` with `✨ AI Summary` badge + symptom/quote card.
  - If pre-visit intake was NOT submitted (`preVisit: null`): Replace `✨ AI Summary` with `Not Submitted` tag and show a clean neutral empty card: `"No pre-visit intake submitted by patient"`.

---

## 3. Architecture & File Structure

The prototype lives in the root directory:

```
c:\Alif\Onu App Prototype\
├── index.html              # Main interactive SPA prototype (HTML + CSS + JS)
├── DESIGN_GUIDELINE.md     # Visual design system, color tokens, and UI SOPs
└── AI_INSTRUCTIONS.md      # This file: Project context, clinical logic & AI instructions
```

### 3.1 Structure of `index.html`
* **Lines 1–150**: HTML `<head>` with CDN stylesheets (Phosphor Icons, Google Fonts `Urbanist` & `DM Sans`).
* **Lines 150–4200**: Comprehensive CSS Design System:
  * CSS Variables (`:root`) defining colors, typography, spacing, shadows, and transitions.
  * Mobile phone frame container (`.phone-mockup`, `.phone-screen`).
  * Page views and smooth slide transitions (`.page-left`, `.page-right`, `.active-page`).
  * Surface components, bottom sheet modal system (`.bottom-sheet`, `.modal-backdrop`), sticky docks, and status chips.
* **Lines 4200–5600**: HTML Page Views and Modal Sheets:
  1. `#pageDesk`: Doctor's Home Desk & Patient Queue Hero.
  2. `#pageSchedule`: Calendar strip & shift slot editor.
  3. `#pageVideoCall`: Fullscreen video consultation with PiP camera, call controls, and patient notes.
  4. `#pageAiWrapUp`: Post-call AI transcription transition screen.
  5. `#pageConsultationReview`: Prescription composer, chief complaint editor, medicine stack, lab tests, and referrals.
  6. `#pagePrescriptionPreview`: Official PDF-like digital prescription preview.
  7. `#pageAppointments`: All Appointments & Shift History with tab switching (`Upcoming` vs `History`) and Date/Shift filtering.
  8. `#pageAppointmentDetails`: Clinical record inspection with dynamic relevance sorting.
  * **Modals / Bottom Sheets**: `#shiftModalSheet`, `#goingOfflineModalSheet`, `#endCallModalSheet`, `#addMedicineModalSheet`, `#addLabModalSheet`, `#referDoctorModalSheet`, `#deleteConfirmModalSheet`, `#skipPatientModalSheet`, `#apptFilterModalSheet`.
* **Lines 5600–7850**: Core JavaScript Application State & Controllers.

---

## 4. Key JavaScript State Variables & Data Models

### 4.1 Master State Variables
| Variable | Type | Purpose |
| :--- | :--- | :--- |
| `isShiftActive` | `Boolean` | `false` before starting Shift 1; `true` once Shift 1 starts. |
| `isDoctorOffline` | `Boolean` | Toggled when doctor goes offline / pauses shifts. |
| `currentPatientIndex` | `Number` | Pointer to the active patient in `queuePatients[]`. |
| `currentApptTab` | `String` | `'upcoming'` or `'history'` on `#pageAppointments`. |
| `currentApptDateKey` | `String` | Selected date filter (`'all'`, `'today'`, `'yesterday'`, `'sept30'`, etc.). |
| `activeFilterSettings` | `Object` | Applied filters `{ status: 'all', type: 'all', shift: 'all' }`. |
| `callTimerSeconds` | `Number` | Consultation video call elapsed seconds timer. |
| `pendingDeleteCallback` | `Function` | Holds closure for item or shift deletion after modal confirmation. |

### 4.2 Data Collections
* **`queuePatients`**: Array of active patients in the current live shift (`serial`, `name`, `age`, `gender`, `avatar`, `subtitle`, `time`, `phone`).
* **`appointmentsData`**: Master collection of all appointment records spanning Today, Yesterday, Saturday Sep 27, Tomorrow Sep 30, and Thu Oct 1.

```javascript
// Example Appointment Record Schema
{
  id: 'apt1',
  dateKey: 'today',             // 'today' | 'yesterday' | 'sept27' | 'sept30' | 'oct01'
  dateLabel: 'Today, Sept 29',
  shiftId: 1,                   // 1 | 2
  shiftName: 'Shift 1 • 9:00–11:00 AM',
  shiftType: 'Video Consultation',
  serial: '#1',
  name: 'Tariqul Islam',
  age: 34,
  gender: 'Male',
  phone: '+880 1712-345678',
  status: 'queued',             // 'queued' | 'in_call' | 'draft_rx' | 'prescribed' | 'skipped'
  time: '9:00 AM',
  type: 'Follow Up',            // 'Initial Consultation' | 'Follow Up'
  preVisit: {                   // Or null if patient skipped pre-visit intake
    symptoms: 'Tension Headache & Neck Stiffness',
    duration: '7 Days',
    severity: 'Mild (3/10)',
    severityLevel: 'mild',
    complaintQuote: 'Tight pressure when working on computer.',
    uploadedDocs: [
      { name: 'Previous_Rx_Aug2026.pdf', size: '1.2 MB', type: 'Prescription', icon: 'ph-file-pdf' }
    ]
  },
  consultationNotes: 'Patient reports 80% improvement...',
  prescriptionPdf: 'RX_Tariqul_Islam_Sep29.pdf'
}
```

---

## 5. Screen-by-Screen User Journeys

### Screen 1: My Desk (`#pageDesk`)
* **Purpose**: The primary operational dashboard for the doctor during their shift.
* **Key Components**:
  * Top navigation bar with Doctor Avatar, Online/Offline Toggle, and Notification Bell.
  * Today's Date & Shift Meta (`Sept 29 • 9:00 AM – 11:00 AM`).
  * **Hero Queue Card (`#heroCard`) Three-Stage State Machine**:
    1. **Stage 1 (Locked - e.g. 8:22 AM)**: Neutral card background (`#F6F8F9`) with quiet white badges. Displays `Shift Starts at 9:00 AM`, subtext `"Calling room unlocks at 8:58 AM (2 mins before shift)"`, and locked action button `🔒 Shift Locked Until 8:58 AM`. Tapping the locked button simulates fast-forwarding to 8:58 AM.
    2. **Stage 2 (Ready to Start - 8:58 AM)**: Transforms into vibrant active Sage (`#D6EAE6`). Calling room unlocks 2 minutes before shift start. Displays `Start Shift 1`, `Serial #1 Tariqul Islam • 34 Yrs • Male`, and dark green primary CTA `▶ Start Shift • Call Serial #1` (`#052E28`).
    3. **Stage 3 (Active / In Call - 9:00 AM)**: Vibrant Sage card (`#D6EAE6`) displaying active live patient (`Serial #1 Tariqul Islam`, `34 Yrs • Male`) with CTA `Join Video Call • #1`.
  * **Doctor Offline State (Subtle Alert Standard)**:
    * When the doctor toggles offline, the Hero card transforms into a soft blush card (`#FEFAF9` with `1.5px solid #FECDCA`), soft rose icon pill (`#FEF3F2`, `#D92D20` moon icon), rose status pill with a subtle pulsing red dot, `"Doctor Offline"` toggle indicator, and `"Shift Paused"` meta header.
  * **Interactive Demo Mechanism**: Tapping the clock time in the status bar (`#statusClockTime`) toggles between Locked (`8:22 AM`) and Ready (`8:58 AM`) anytime for effortless presentations.
  * **Action Cards**: Quick access to `View All Appointments` and `Edit Schedule`.

### Screen 2: Edit Shift / Schedule (`#pageSchedule`)
* **Purpose**: View and manage consultation shift hours across a 7-day calendar strip.
* **Key Components**:
  * 7-day horizontal scrollable date strip (starting from Today).
  * Prominent `+ Add Shift` action button triggering `#shiftModalSheet`.
  * List of configured shifts (Shift 1: 10 AM–12 PM, Shift 2: 6 PM–11 PM).
  * Edit button (`editExistingShift`) and Delete trash button (`requestDeleteShift`).
  * **Shift Deletion**: Always prompts `#deleteConfirmModalSheet` before removing the shift.

### Screen 3: Video Consultation Call (`#pageVideoCall`)
* **Purpose**: Telemedicine video interface between doctor and patient.
* **Key Components**:
  * Fullscreen patient camera feed with name, serial badge, and live elapsed timer (`00:00`).
  * Doctor PiP (Picture-in-Picture) tile with camera flip animation.
  * Call Controls: Mute Mic, Toggle Camera, Flip Camera, and End Call (`openEndCallModal`).
  * Floating Skip Patient button triggering `#skipPatientModalSheet`.
  * Collapsible bottom sheet for patient Pre-visit intake summary during the call.

### Screen 4: Live AI Wrap-Up (`#pageAiWrapUp`)
* **Purpose**: Interstitial screen showing ambient AI transcribing conversation into structured clinical notes.
* **Behavior**: Displays animated audio waves, transcribing message, and automatically navigates to `#pageConsultationReview` after 2.6 seconds (or allows returning to Desk).

### Screen 5: Consultation Wrap-Up Review & Rx Finalization (`#pageConsultationReview`)
* **Purpose**: Finalizing clinical notes, prescriptions, investigations, and referrals before issuing.
* **Key Components**:
  * **Chief Complaint**: AI-generated summary, editable by doctor.
  * **Draft Prescription**: List of medications with dosages, frequencies, and durations. Doctor can edit or delete items (with confirmation) or add new medicines via `#addMedicineModalSheet`.
  * **Lab Tests / Investigations**: Diagnostic tests with priority tags (`Routine` / `Urgent`). Addable via `#addLabModalSheet`.
  * **Specialist Referral**: Optional referral doctor search and selector via `#referDoctorModalSheet`.
  * **Follow-up Chips**: `None`, `3 Days`, `7 Days`, `14 Days`, `1 Month`.
  * **Sticky Bottom Action Dock**: Full-width primary CTA `Preview & Issue Prescription`.

### Screen 6: Official Prescription Preview (`#pagePrescriptionPreview`)
* **Purpose**: Digital representation of the generated prescription with official doctor header, patient info, Rx symbol, medications, investigations, advice, and digital signature.
* **Primary CTA**: `Issue & Send to Patient` (marks visit as prescribed and returns to Desk).

### Screen 7: All Appointments & Shift History (`#pageAppointments`)
* **Purpose**: Comprehensive list of all past, present, and future patient bookings.
* **Tabs**:
  * **Upcoming Tab**: Starts from Today (queued, in-call, draft Rx visits) through future dates (`Tomorrow`, `1 Oct`).
  * **History Tab**: Starts from Today (strictly `prescribed` or `skipped` visits) backwards through past dates (`Yesterday`, `27 Sep`). Never shows future dates.
* **Date Filters**: Concise pills (`All`, `Today`, `Tomorrow`, `1 Oct` for Upcoming; `All`, `Today`, `Yesterday`, `27 Sep` for History).
* **Modal Filter**: Tap top filter icon to open `#apptFilterModalSheet` for Status, Type, and Shift filtering.
* **Turn Now Highlight**: If a patient is currently active on Desk, their card in the list highlights with `.status-in-call` and `Turn Now` pulse badge.
* **Offline Auto-Cancellation**: When the doctor goes offline, booked visits within the offline duration (e.g. `Today`) are automatically cancelled and hidden from the Upcoming queue. Viewing a cancelled date displays an informative offline empty state (`Doctor is Offline • Appointments cancelled & patients notified`). Returning online restores active queues.

### Screen 8: Appointment & Visit Clinical Details (`#pageAppointmentDetails`)
* **Purpose**: Detailed inspection of any individual appointment or historical visit record.
* **Top Meta Strip Transformation**:
  * **For Completed / Prescribed Appointments & Patient Visit Log Details**: Title displays `Visit Details`. The 3-box strip is replaced by `.visit-details-meta-card` containing:
    * Top row: `● COMPLETED` green badge + consultation mode & duration pill (e.g. `Video Call • 25 Mins`).
    * Bottom row: Consultation date (`Aug 20, 2026`) + call time (`08:00 PM`).
  * **For Upcoming / Queued / Draft Rx / Skipped Appointments**: Title displays `Appointment Details`. Displays the 3-column info strip (`Status`, `Serial`, `Type`).
* **Card Color & Visual Hierarchy**:
  * **Consultation Notes (`.details-notes-card`)**: High-importance clinical outcome card styled in crisp mint/sage tint (`#F4F8F7`, `border: 1.5px solid #D1E5E1`) with deep forest text (`#0F2F29`).
  * **Pre-visit Details (`.details-previsit-card`)**: Patient intake history styled in soft, warm neutral tone (`#FAF8F5`, `border: 1.5px solid #EFE5D6`) with warm amber quote bar (`#D97706`) and `.info-chip-warm` tag. Displays the patient's specific chief complaint from AI triage (e.g. `Sore Throat & Mild Fever`, `Seasonal Allergies & Runny Nose`), duration, severity, and conversational complaint quote given to the AI intake bot.
* **Dynamic Section Ordering**:
  * **For Completed (`prescribed`)**: Issued Prescription -> Consultation Notes -> Pre-visit Details -> Patient Documents.
  * **For Draft Rx (`draft_rx`)**: Consultation Notes -> Pre-visit Details -> Patient Documents (with sticky bottom dock `Review & Finalize Rx`).
  * **For Queued / Upcoming**: Pre-visit Details -> Patient Documents.
* **No Redundant Bottom Dock on Completed Visits**:
  * The bottom dock button is removed for completed visits because the **Issued Prescription** card on top already contains the primary `View Rx` action. Bottom dock is active only for pending tasks (`Review & Finalize Rx`, `Re-join Active Call`).
* **Empty State Handling**: If pre-visit intake is missing, displays `Not Submitted` tag and neutral empty card. If documents are missing, displays `0 Files` and `"No patient files uploaded for this visit"`.
* **Contextual Back Navigation**: Back arrow returns to `#pagePatientProfile` if opened from a patient visit log, or to `#pageAppointments` if opened from the appointments list.

### Screen 9: My Patients Directory (`#pagePatientsList`)
* **Purpose**: Complete patient directory containing every patient ever consulted by the doctor once or multiple times.
* **Key Components**:
  * Top header: `.app-header` with Title `My Patients` (`Urbanist 25px Bold`), Subtitle `Your patient directory & history` (`DM Sans 13.5px #717171`), with *no notification bell* for a clean secondary tab layout.
  * Real-time search bar (`#inputPatientsSearch`) matching patient name and phone number (`DM Sans 13.5px Medium`) + filter button (`ph-sliders-horizontal`).
  * **Modern Clinical Metrics Box (`.patient-metrics-card`)**: 3-column split card in soft sage tint (`#EFF7F5`, border `1.5px solid #D4EAE4`) with vertical dividers displaying `Total Patients` (`8`), `Consultations` (`24`), and `Repeat Rate` (`62%`) in clean typography (`Urbanist 22px Bold #052E28` + `DM Sans 11.5px #4A6E67`) without clunky icon circles, matching the 8 directory records below.
  * Section header (`.section-text-group`): Title `All Patients` (`Urbanist 20px Bold #000000`) + Subtitle `8 Patients` (`DM Sans 13px #717171`), consistent with the top header typography system.
  * Patient Cards with circular pastel initials avatar (`#E8F4F1`), patient name, minimalist subtext (`[X] Visits`), and caret chevron. No patient ID or dates displayed on the tile.
  * Clean empty state when search returns zero matching records.
  * Tapping any patient card smoothly opens that patient's **Patient Profile (`#pagePatientProfile`)**.

### Screen 10: Patient Profile & Medical History (`#pagePatientProfile`)
* **Purpose**: Full clinical dossier for a single patient with comprehensive medical vitals and past visit history.
* **Key Components**:
  * Sticky top bar with return back arrow (`returnFromPatientProfile()`) and direct phone call trigger.
  * **Patient Hero Card**: Circular initials badge (`52px × 52px`), patient name, demographics (`[Age] Yrs • [Gender]`), and tap-to-call phone pill (no patient ID).
  * **Patient Info & Vitals Grid**: Dedicated `Patient Info` card with circular white icon bubbles for `Age`, `Gender`, `Visits`, `Blood`, `Weight`, and `Height`.
  * **Visits Log (Max 3 Default + Inline "See All" Expansion)**:
    * Chronological list of consultations showing up to 3 visits by default.
    * Each visit tile displays consultation type, date, time, and doctor notes.
    * **Interactive Tap Flow**: Tapping any visit tile opens the **Visit Details** view for that visit with completed call mode, duration, date, time, consultation notes, and issued prescription.
    * If a patient has >3 visits, a `.btn-see-all-visits` button (`See all [N] visits` with `ph-caret-down`) appears below the 3rd visit. Clicking it seamlessly expands the remaining visits inline without navigating away.
  * **Files Section**: Completely removed per design direction; files and prescriptions are accessed directly via individual appointment details.

### Bottom Navigation Bar Master Standard
* **Active Tab**: Displays inside a soft rounded pastel pill (`.active-nav-pill` on `#EFF7F5`), with the **filled icon** (`ph-fill`) in `#052E28`, a subtle horizontal accent indicator bar, and **NO title text**.
* **Inactive Tabs**: Displays the **outline icon** (`ph`) in `#717171` + title text in `DM Sans 11px Medium #717171`.
* **Synchronization**: Automatically managed via `setActiveNavTab(tabName)`.

---

## 6. Design Tokens & Visual Hierarchy Quick-Reference

| Element | Specification | Hex / Value |
| :--- | :--- | :--- |
| **App Canvas** | Pure White Background | `#FFFFFF` |
| **Hero & Metric Cards** | Sage Glassmorphism | `linear-gradient(135deg, rgba(239, 247, 245, 0.95), rgba(214, 234, 230, 0.8))` + `backdrop-filter: blur(16px)` + `border: 1.5px solid rgba(126, 184, 174, 0.4)` |
| **Surface & Neutral Cards** | Frosted Glass Neutral | `linear-gradient(135deg, rgba(246, 248, 249, 0.95), rgba(238, 244, 243, 0.8))` + `backdrop-filter: blur(16px)` + `border: 1.5px solid rgba(226, 236, 234, 0.85)` |
| **Primary Action CTA** | Deep Forest Green Fill | `#052E28` (Text: `#FFFFFF`, Weight: `700`) |
| **Primary Text** | Urbanist Bold | `#000000` |
| **Secondary / Meta Text** | DM Sans Regular / Medium | `#717171` |
| **Section Spacing** | Strict Section Wrapper Gap | `24px` between `<section>` blocks, `10px` between title and cards inside sections |
| **Bottom Sheet Radii** | Fluid iOS Curve | `32px 32px 0 0` with drag grabber (`#CBD5E1`) |

---

## 7. Instructions for Future AI Assistants & Developers

When you are prompted by the user to add a feature, fix a bug, or redesign a screen:

### Step 1: Read and Align
1. Read both [`DESIGN_GUIDELINE.md`](file:///c:/Alif/Onu%20App%20Prototype/DESIGN_GUIDELINE.md) and this file ([`AI_INSTRUCTIONS.md`](file:///c:/Alif/Onu%20App%20Prototype/AI_INSTRUCTIONS.md)).
2. Confirm you understand the user's intent within the Wise/Uber minimalist healthtech framework.

### Step 2: Enforce Inviolable Rules
- **DO NOT** show clinical patient ID numbers or redundant dates in patient directory tiles. Keep subtext minimal: `[X] Visits` or `[Age] Yrs • [Gender]`.
- **DO NOT** create nested card boxes inside other card boxes.
- **DO NOT** bypass delete confirmation modals.
- **DO NOT** add start call or recall controls for skipped patients.
- **DO NOT** revert the pure white canvas (`#FFFFFF`) to dark or gray backgrounds.

### Step 3: Implement & Keep Context Synchronized
- Modify `index.html` cleanly using single contiguous replacements.
- Test and verify state changes, DOM IDs, and transition classes.
- Always update [`DESIGN_GUIDELINE.md`](file:///c:/Alif/Onu%20App%20Prototype/DESIGN_GUIDELINE.md) and [`AI_INSTRUCTIONS.md`](file:///c:/Alif/Onu%20App%20Prototype/AI_INSTRUCTIONS.md) after modifying or expanding screens.
- **MANDATORY**: After making any significant structural, behavioral, or feature changes, update both `DESIGN_GUIDELINE.md` and `AI_INSTRUCTIONS.md` to reflect the latest modifications.
