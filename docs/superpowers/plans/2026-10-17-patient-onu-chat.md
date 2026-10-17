# Patient Onu Chat Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a patient-facing Onu chat with a fresh-chat home, message and attachment flow, and locally saved conversation history.

**Architecture:** Add a dedicated patient Onu page inside the existing single-file prototype, reusing current app page transitions, design tokens, bottom navigation, and Phosphor icons. Keep chat data and thread-history UI in patient-only JavaScript; simulate replies locally and persist message and attachment metadata in `localStorage`.

**Tech Stack:** Standalone HTML, CSS, vanilla JavaScript, browser `localStorage`, existing patient app CSS variables and Phosphor icons.

**Spec:** `docs/superpowers/specs/2026-10-17-patient-onu-chat-design.md`

## Global Constraints

- Use the patient app's existing forest green primary (`--color-primary-btn`), sage accents, white canvas, Urbanist headings, DM Sans supporting text, and Phosphor icons.
- Do not change `doctors-app.html`, visit lifecycle logic, payment flow, or pre-visit intake.
- Do not add a backend, network model call, remote storage, or real medical analysis.
- Do not persist patient file contents; persist filenames, MIME types, sizes, and timestamps only.
- Keep header and composer controls at least 44px high and honor the home-indicator safe area.
- Do not add or run tests; verify with the manual flows and `git diff --check` only.

## Review Focus

- Missing or invalid local storage: chat remains usable in memory and does not fail during load or save.
- Malformed stored thread data: ignore invalid records and render a safe empty history state.
- Empty text submit or unsupported file type: do not create an empty chat; show concise inline or toast feedback.
- Long prompt and filename: wrapping/truncation must not cause horizontal overflow or cover the composer.
- Changing tabs or opening/closing history: preserve the intended thread, draft, and underlying screen state.

---

### Task 1: Patient Onu Navigation and Screen Layout

**Files:**
- Modify: `patient-app.html` bottom navigation markup, app-page markup, and Onu CSS.

**Interfaces:**
- Produces: `navigateToOnu()` to activate the Onu page and set `home_empty` when entering from another app tab.
- Produces: `setPatientOnuView(view)` where `view` is `'home_empty' | 'conversation_new' | 'conversation_saved'`; this controls the home/chat header, welcome shortcuts, composer, and bottom-nav visibility.

- [x] Enable the center nav item, rename it `Onu`, and route its click to `navigateToOnu()`.
- [x] Add the patient Onu page using the app's existing `.app-page` transitions and current typography, colors, and icon family.
- [x] Add the redesigned fresh-chat header, welcome area, `Upload prescription` and `Book appointment` actions, disclaimer, and composer dock.
- [x] Add the conversation header with Back left, centered `Onu`, and icon-only New chat plus History controls on the right; keep the bottom nav visible only on the home state.
- [x] Add pressed/focus states and ensure the composer sits above the home indicator and nav bar.
- [ ] Manually check entry from Discover and Visits, Onu active-tab styling, and return from Onu to both tabs.

### Task 2: Conversation Messages and Attachments

**Files:**
- Modify: `patient-app.html` Onu markup and patient Onu controller script.

**Interfaces:**
- Consumes: `setPatientOnuView(view)` from Task 1.
- Produces: `submitPatientOnuMessage()` to add a non-empty user message and a deterministic prototype reply.
- Produces: `handlePatientOnuAttachments(files)` to add supported image/PDF metadata and switch from home to chat.
- Produces: `renderPatientOnuMessages()` to render user messages, assistant responses, and attachment tiles in message order.

- [x] Add a labeled textarea composer with plus/file, microphone, and send controls; Enter sends and Shift+Enter inserts a newline.
- [x] Add a hidden multiple-file input accepting images and PDFs; use it from both the home upload card and composer attachment control.
- [x] Render selected file names and types in the user message stream and provide explicitly simulated assistant responses.
- [x] Keep actual file contents out of local storage and do not claim the prototype performed a real analysis.
- [x] Add concise feedback for empty submissions and unsupported attachments; announce appended messages through a polite live region.
- [ ] Manually check text submit, multiline input, one and multiple files, image/PDF display, and the home-to-conversation transition.

### Task 3: Thread Persistence and Left History Drawer

**Files:**
- Modify: `patient-app.html` drawer markup, controller script, and related styles.

**Interfaces:**
- Consumes: `renderPatientOnuMessages()` and `setPatientOnuView(view)` from earlier tasks.
- Produces: `loadPatientOnuThreads()`, `savePatientOnuThreads()`, `startNewPatientOnuChat()`, `openPatientOnuHistory()`, `closePatientOnuHistory()`, and `openPatientOnuThread(threadId)`.
- Data shape: `{ id, title, updatedAt, flow?, messages: [{ id, role, text, createdAt, attachments: [{ name, type, size }], action? }] }`.
- Storage key: `onuPatientThreads:v1`.

- [x] Save the first submitted turn as a thread and derive its title from the initial text or first attachment name.
- [x] Persist thread metadata and messages to `localStorage`; catch storage errors and retain the active session in memory.
- [x] Add a left sliding drawer with overlay, close action, New chat action, and saved threads grouped by recency.
- [x] Restore a selected thread and its messages; keep the conversation header and hidden bottom navigation active.
- [x] Make Back and New chat return to the fresh-chat home without deleting saved threads; preserve the current view when history is dismissed.
- [x] Add Escape dismissal, focusable accessible controls, and `aria-expanded`/selected state where relevant.
- [ ] Manually check save/reload/restore, switching threads, New chat, Back, backdrop close, Escape, and malformed storage fallback.

### Task 4: Appointment Route and Final UI Review

**Files:**
- Modify: `patient-app.html` Onu action-card handlers and responsive/accessibility styles.

**Interfaces:**
- Consumes: existing `openDoctorsList()` flow and all patient Onu view/controller functions.
- Produces: `openPatientOnuAppointmentBooking()` to start the guided doctor-finding chat and `openPatientOnuRecommendedDoctors(specialty)` to open matching results.

- [x] Route `Book appointment` into a guided chat that asks the main concern, duration, and other symptoms; show a prototype specialty suggestion and a button to browse matching doctors.
- [x] Return from matching doctor results to the recommendation chat.
- [ ] Verify the home retains bottom navigation and conversation mode hides it; ensure the composer and drawer do not overlap safe areas.
- [x] Review keyboard order, labels, visible focus, 44px touch targets, long text/filenames, small phone width, and reduced-motion behavior in source.
- [ ] Review the rendered patient app manually and run `git diff --check`; do not add or run automated tests.

## Implementation Handoff

Implement sequentially in `patient-app.html`; the markup/state APIs in Task 1 are used by later tasks, so this plan does not benefit from parallel work.

## Execution Note

Implemented in `patient-app.html`, including the updated guided doctor-finding flow and Onu header styling requested after plan approval. `git diff --check` is clean and the inline JavaScript passes `node --check`. A screenshot review was unavailable because this session has no enabled browser surface; browser interactions remain visually unconfirmed here.
