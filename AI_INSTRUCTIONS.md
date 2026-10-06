# Onu App — AI Master Context & Project Blueprint
*Comprehensive Knowledge Base, Clinical Workflows, Architecture, and Autonomous Engineering Instructions for AI Pair Programmers & Human Developers.*

---

## ⚠️ ZERO-TOLERANCE DESIGN & ENGINEERING GUARDRAILS (NEVER VIOLATE)

1. **PRIMARY BUTTON vs. SELECTION STATE COLOR RULE (ABSOLUTE LAW)**:
   - **Solid Forest Green `#052E28` with `#FFFFFF` text is EXCLUSIVELY for Primary Action CTA Buttons** (`Start Shift`, `Save Shift`, `+ Add Shift`, `Confirm Break`, `Join Call`, `Withdraw Funds`, `Save Account`).
   - **ALL Selection States** (Segmented control buttons, Active calendar date pills, Multi-select day pills, Filter chips, Duration selector cards) **MUST ALWAYS** use:
     - `background: var(--color-card-sage)` (`#D6EAE6`)
     - `border: 1px / 1.5px solid var(--color-border-selected)` (`#7EB8AE`)
     - `color: var(--color-primary-btn)` (`#052E28`)
     - `font-weight: 700`
   - **NEVER** give selection states, segmented buttons, or date pills a solid `#052E28` dark green background.

2. **BOTTOM SHEET & POPUP UNIFIED ARCHITECTURE**:
   - **ALL Bottom Sheets** (Edit Shift, Withdraw Funds, Saved Accounts, Add Payout Method, Confirmations) **MUST ALWAYS** follow the standard editorial layout:
     1. Drag handle (`.sheet-drag-handle`)
     2. Top badge icon (`.sheet-badge-icon`, 40x40 rounded container)
     3. Editorial header (`.sheet-hero-header` with `.sheet-editorial-title` in `Urbanist 32px Bold #1E293B` deep slate charcoal and `.sheet-minimal-subtitle` 14px)
     4. Content container / Form fields
     5. Standard action group (`.sheet-actions-group` with `.btn-sheet-cancel` and `.btn-sheet-confirm`) with generous bottom clearance.
   - **NEVER** create custom unstyled inline headers with raw 'x' buttons that deviate from this system.

3. **DESTRUCTIVE ACTIONS CONFIRMATION RULE**:
   - Deleting a shift, deleting a saved payment/bank method, or skipping a patient **MUST ALWAYS** trigger a dedicated editorial confirmation bottom sheet (`#deleteConfirmModalSheet`, `#modalDeleteAccountConfirm`, `#modalSkipPatient`).
   - Never delete or remove items silently on tap.

4. **HERO CARD SPACING & VERTICAL RHYTHM**:
   - Hero balance and patient cards must have generous vertical rhythm (`padding: 20px; gap: 16px;`):
     - Top: `.badge-pill-light` frosted badge pill (`Available Balance`, `Next Patient`)
     - Center: Bold large metric (`৳ 12,400`, `Farzana Khan`)
     - Bottom: Full-width `#052E28` primary action CTA.
   - No redundant multi-line explanatory subtext under amounts.

5. **FORM INPUTS & NO UNNECESSARY CHIP CLUTTER**:
   - Text inputs (e.g. Bank Name, Holder Name, Account Number) must be clean manual inputs. Do not clutter below inputs with preset suggestions unless explicitly requested.

6. **GIT & VERSION CONTROL RULE**:
   - **NEVER run `git commit` or `git push`** under any circumstance unless the user explicitly commands you to do so.

7. **LESS TEXT & COGNITIVE DECLUTTERING**:
   - Keep labels, metrics, and fraction counters ultra-minimal.
   - Zero nested boxes ("No boxes inside boxes inside boxes").

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
  * **Modals / Bottom Sheets**: `#shiftModalSheet`, `#timePickerModalSheet`, `#goingOfflineSheet`, `#cancelShiftModalSheet`, `#endCallModalSheet`, `#addMedicineModalSheet`, `#addLabModalSheet`, `#referDoctorModalSheet`, `#deleteConfirmModalSheet`, `#skipPatientModalSheet`, `#apptFilterModalSheet`.
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

### Screen 0: Onu Clinical AI Copilot & Default Home (`#pageOnu`)
* **Purpose**: The primary focal point and default landing screen for the doctor upon opening the app. Serves as an intelligent AI clinical copilot for rapid patient dossiers, lab investigation inquiries, drug safety verification, and shift preparation.
* **Key Components**:
  * **Brand Header**: Editorial title `Onu` with live status pill (`✨ AI Copilot` with pulsing mint dot) and New Chat action (`ph-note-pencil`).
  * **Editorial Hero Greeting**: Confident greeting `Hello, Doctor Sifat` in `Urbanist 28px Bold`.
  * **Live Clinic Context Banner**: Soft sage interactive banner displaying current shift schedule and queue count (`Shift 1 starts at 9:00 AM • 6 patients in queue`). Tapping navigates straight to My Desk.
  * **Smart Clinical Prompts (2x2 Grid)**:
    1. 🩺 **Patient Summary**: *"Summarize Tariqul's visits & current vitals"* -> instant clinical briefing on complaints, history, and medications.
    2. 🧪 **Lab & Reports**: *"Show Farzana's CBC & endoscopy results"* -> breakdown of recent investigations and diagnostic findings.
    3. 💊 **Drug Interaction**: *"Verify Telmisartan + Amlodipine safety"* -> pharmacology check with clinical recommendations.
    4. 📋 **Shift Briefing**: *"Overview of today's Shift 1 patient queue"* -> patient order and chief complaints.
  * **Interactive Conversation Stream**:
    * Clean doctor query speech bubbles (`#052E28`).
    * Structured Onu AI response cards with clinical bullet points, vitals, and actionable quick chips (`[View Profile]`, `[Start Shift Call]`, `[Full Queue List]`).
    * Realistic typing indicator animation (`onu-typing-indicator`).
  * **Floating Glassmorphic Input Dock**:
    * `+` Attachment & Patient Tag button (`openOnuAttachMenu`).
    * Smart text field with Enter key support.
    * Voice Dictation mic button with pulsating listening state (`toggleOnuVoiceListening`).
    * Primary Send / Waveform button (`sendOnuMessage`).
    * Subtle AI disclaimer text at base.
  * **Seamless Full-Screen History Side Panel (`#onuHistoryDrawer`)**: Full-height drawer attached to `.phone-screen` (`z-index: 155`) with full-screen backdrop (`#onuDrawerBackdrop`, `z-index: 150`) and top status bar clearance padding, providing seamless white coverage from the top notch down.

### Screen 1: My Desk (`#pageDesk`)
* **Purpose**: The primary operational dashboard for the doctor during their shift.
* **Key Components**:
  * Top navigation bar with Doctor Avatar, Online/Offline Toggle, and Notification Bell.
  * Today's Date & Shift Meta (`Sept 29 • 9:00 AM – 11:00 AM`).
  * **Hero Queue Card (`#heroCard`) Three-Stage State Machine**:
    1. **Stage 1 (Locked - e.g. 8:22 AM)**: Neutral card background (`#F6F8F9`) with quiet white badges. Displays `Shift Starts at 9:00 AM`, subtext `"Calling room unlocks at 8:58 AM (2 mins before shift)"`, and locked action button `🔒 Shift Locked Until 8:58 AM`. Tapping the locked button simulates fast-forwarding to 8:58 AM.
    2. **Stage 2 (Ready to Start - 8:58 AM)**: Transforms into vibrant active Sage (`#D6EAE6`). Calling room unlocks 2 minutes before shift start. Displays `Video Consultation` badge on the left, `Shift 1` badge on the top right corner, title `Ready To Begin`, subtext `Video Consultation • 6 in Queue`, and dark green primary CTA `▶ Start Shift` (`#052E28`).
    3. **Stage 3 (Active / In Call - 9:00 AM)**: Vibrant Sage card (`#D6EAE6`) displaying active live patient (`Serial #1 Tariqul Islam`, `34 Yrs • Male`) with CTA `Join Video Call • #1`.
  * **Doctor Offline State (Subtle Alert Standard)**:
    * When the doctor toggles offline, the Hero card transforms into a soft blush card (`#FEFAF9` with `1.5px solid #FECDCA`), soft rose icon pill (`#FEF3F2`, `#D92D20` moon icon), rose status pill with a subtle pulsing red dot, `"Doctor Offline"` toggle indicator, and `"Shift Paused"` meta header.
  * **Go Offline Availability Sheet (`#goingOfflineSheet`)**:
    * **Header**: Amber `ph-power` badge icon with short-month toggle (e.g. `Sept 2026`).
    * **Week View (7-Day Rolling Strip)**: Shows 7 consecutive days starting today in a single row without column header text (day name + date inside card).
    * **Month View**: Standard Sunday-to-Saturday grid with weekday headers and **numbers only** inside cards (zero redundant day names).
    * **Unified Single-Dot Indicator**: At most 1 dot per date (No dot = empty; Soft Light Eucalyptus `#48BB95` = empty shift; Soft Light Apricot `#F6A84B` = booked shift).
    * **Confirmation Flows**:
      * Selecting 1–6 days opens `#offlineConfirmedModalSheet` with clean summary tile (`Sept 15 – 16 • Offline` + auto-reschedule confirmation).
      * Selecting an entire week (>= 7 days) with no remaining open shifts opens `#createShiftToOfflineModalSheet` with an amber calendar badge guiding the doctor to open a new shift.
  * **Interactive Demo Mechanism**: Tapping the clock time in the status bar (`#statusClockTime`) toggles between Locked (`8:22 AM`) and Ready (`8:58 AM`) anytime for effortless presentations.
  * **Action Cards**: Quick access to `View All Appointments` and `Edit Schedule`.

### Screen 2: Edit Shift / Schedule (`#pageSchedule`)
* **Purpose**: View and manage consultation shift hours across a 7-day calendar strip.
* **Key Components**:
  * 7-day horizontal scrollable date strip with single-dot status indicators beneath each date pill.
  * Prominent `+ Add Shift` action button triggering in-page shift creation.
  * List of configured shifts displaying all-caps shift chip container (`.shift-name-chip` e.g. `SHIFT 1`, `SHIFT 2`), consultation type pill (`[📹 Video Consultation]`), time window, and minimal capacity metric (e.g. `04/15 Patients` or `0/15 Patients` for new/empty shifts).
  * Edit button (`editExistingShift`) and Delete trash button (`requestDeleteShift`).
  * **Booked Shift Editing & Start Time Lock**: Shifts with active booked patients can be edited freely (start time is locked to preserve booked appointments; end time and max patient capacity can be adjusted).
  * **Android Compose Floating Snackbar (`#androidSnackbar`)**: Tapping the locked start time tile (or other locked properties) displays an Android Compose-styled floating snackbar (`#2A2F2D` dark surface, mint accent icon, clear natural message e.g. *"4 patients already booked, can't change start time"*, `OK` action, auto-dismiss in 3s) without intrusive persistent banner clutter.
  * **Shift Deletion & Auto-Rescheduling Protocol**: Always prompts `#cancelShiftModalSheet` before removing the shift. If patients are already booked, warns with `⚠️ X Patients Already Booked` and informs the doctor that deleting will automatically reschedule them to the next available shift, matching the offline auto-rescheduling protocol.

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

### Screen 6: Official Prescription (`#pagePrescriptionPreview`)
* **Purpose**: Digital representation of the generated prescription rendered on a pure white canvas (`#FFFFFF`) with a subtle 1px border (`#E2E8F0`) and mild elevation shadow. Includes official doctor header, patient demographics strip, Rx symbol, medications, investigations, advice, digital certification stamp, and doctor signature.
* **Top Bar Controls**: Back button, `Prescription` title, and Download button (`ph-download-simple`).

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
### Screen 11: Onu Clinical AI Copilot (`#pageOnu`)
* **Purpose**: Primary conversational intelligence assistant and default home landing page of the application.
* **Key Components**:
  * **Unified App Header**: Screen title `Onu` (`Urbanist 25px Bold`), subtitle `Your Clinical AI Assistant` (`DM Sans 13.5px #717171`), and right-handed chat thread history toggle (`ph-clock-counter-clockwise`).
  * **Right-Hand Slide-in Drawer (`#onuHistoryDrawer`)**: Displays recent chat threads, search history CTA, and quick `+ New chat` trigger.
  * **Gemini-Style Minimal Empty State (`#onuWelcomeView`)**:
    * Clean 4-point gradient sparkle icon (`#0D7A5F` → `#2DD4BF` → `#38BDF8`).
    * Centered greeting: `Ask away, Dr. Sifat !` (`Urbanist 26px Bold`) + `Your clinical AI copilot is ready.` (`DM Sans 14px Medium #64748B`).
    * Pure negative space without cluttering cards or boxes.
  * **Google Gemini Unified Floating Input Pill (`.onu-input-pill-box`)**:
    * Single floating pill container above bottom navigation (`height: 52px`, `border-radius: 28px`, `border: 1.5px solid #E2ECEA`).
    * Contains `+` Attach/Tag button, spacious input field, and Dictation Mic (`ph-microphone`).
    * **Morphing Voice Bot / Send Action Button (`.btn-onu-action-morph`)**:
      * In empty state: Soft sage waveform button (`.voice-mode` with `ph-waveform`) opening the full-screen **Live AI Voice Bot Modal (`#modalLiveVoiceBot`)**.
      * While typing: Morphs immediately into deep forest green Send button (`.send-mode` with `ph-bold ph-arrow-up`) sending the clinical prompt.

### Screen 12: My Wallet & Payout System (`#pageWallet`)
* **Purpose**: Doctor earnings tracking, transaction history, withdrawal requests, and payment method management.
* **Key Components**:
  * **Header**: `My Wallet` with Settings gear button opening Saved Accounts & Payout Settings.
  * **Hero Balance Card**: Sage glassmorphic card with available balance (`৳ 12,400`) and full-width `Withdraw Funds` CTA.
  * **Financial Overview**: Split metrics for `Today's Earnings` and `Total Earnings`.
  * **Recent Transactions List**: Grouped transactions with income/payout icons, amounts, and dates.
  * **Transaction Filter Bottom Sheet (`#transactionFilterSheet`)**: Dual-filter modal supporting **Transaction Type** (`All`, `Payouts`, `Withdrawals`) and **Date Period** (`All Time`, `Today`, `Yesterday`, `This Week`, `This Month`) with paired Reset and Apply Filter actions. Trigger button features an active filter dot indicator.

### Screen 13: Doctor Profile & Practice Details (`#pageDoctorProfile`)
* **Purpose**: Manage physician clinical identity, contact details, chamber address, bio, and settings.
* **Key Components**:
  * **Hero Card**: Avatar with camera photo picker, BMDC Verified seal, specialty subtitle, and embedded stats row (`Total Patients: 1,420+`, `Experience: 5+ Years`).
  * **Contact & Practice Section (Editable)**:
    * **Contact Phone Tile**: Dynamic phone display with bottom sheet editor (`#editPhoneModalSheet`).
    * **Chamber Address Tile**: Dynamic chamber location (e.g. `BSMMU (PG Hospital), Shahbag, Dhaka`) with bottom sheet editor (`#editChamberModalSheet`).
    * **About You Bio Card**: Formatted bio preview with bottom sheet popup editor (`#editBioModalSheet`), supporting real-time character count and instant saving.
  * **Professional Identity (Verified)**: BMDC Registration (`437193172`) and verified Consultation Fee (`৳ 1,200 BDT`).
  * **More Navigation**: Settings, Help & Support, and Log Out modal triggers.

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
