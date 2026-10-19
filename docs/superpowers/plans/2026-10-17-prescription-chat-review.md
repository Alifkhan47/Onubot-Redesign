# Onu In-Chat Prescription Review Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Let a patient upload a prescription image in an existing Onu thread, review simulated extracted details, save medicines locally as Active medications, or return to that same thread without saving.

**Architecture:** Keep the existing single-page HTML architecture. Add a versioned local review/medication store, an in-thread prescription artifact, a focused review surface, and a minimal Profile/Active medications page. Keep image preview data in memory for the current session; persist review fields and attachment metadata, and explain when a preview needs to be re-uploaded after reload.

**Tech Stack:** Existing HTML, CSS, vanilla JavaScript, browser localStorage, File/URL APIs. No added dependencies or network services.

**Spec:** `docs/superpowers/specs/2026-10-17-prescription-chat-review-design.md`

## Global Constraints

- Extraction, medicine matching, and chat responses are prototype simulations; do not imply actual OCR, internet lookup, diagnosis, or medicine safety verification.
- Keep the upload in the currently open conversation and return to that exact thread from review.
- Saving adds the reviewed medicine rows to local Active medications; returning to chat does not save them.
- Keep the existing app visual system, navigation and primary button style.
- Do not transmit patient data or prescription images to an external service.

## Review Focus

- A non-image upload or unsupported image must never be treated as a prescription photo; show a recoverable message.
- An unreadable image or absent details must not cause invented patient, doctor, or medicine data.
- Editing a medicine name must refresh its simulated status promptly without presenting a miss as clinical invalidity.
- Returning without saving must leave Active medications unchanged and preserve the review in the source thread.
- Missing, malformed, quota-exceeded, or unavailable localStorage must leave chat usable and explain what could not be saved.

---

### Task 1: Add versioned prescription review and Active medication storage

**Files:**
- Modify: `patient-app.html` (Onu storage constants, normalizers, load/save helpers)

**Interfaces:**
- Produces `loadPatientPrescriptionData() -> { reviews: PrescriptionReview[], medications: ActiveMedication[] }`, `savePatientPrescriptionData(data) -> boolean`, and `normalizePatientPrescriptionData(value) -> normalizedData`.
- Use one key, `onuPatientPrescriptionData:v1`, and stable IDs from `patientOnuMakeId()`.
- A review record stores `id`, `threadId`, `attachmentName`, `attachmentType`, `patient`, `prescriber`, `medicines`, `updatedAt`, and `savedAt`.
- A medicine row stores `id`, `name`, `instructions`, `status`, and `statusReason`.
- An active medication stores the source review ID and saved timestamp in addition to the medicine fields.

- [ ] Add schema normalization for empty, malformed, and older stored values. Accept only strings/numbers/arrays with expected shapes; fall back to empty lists without throwing.
- [ ] Add storage read/write helpers that return explicit success/failure and follow the existing Onu storage-warning pattern.
- [ ] Keep photo blobs and object URLs out of localStorage; preserve attachment metadata and mark previews unavailable after reload.
- [ ] Review the resulting state shape against Task 2 and Task 4 before connecting UI.

### Task 2: Route image uploads into the existing thread

**Files:**
- Modify: `patient-app.html` (Onu attachment handling, `appendPatientOnuTurn`, `getPatientOnuReply`, message renderer)

**Interfaces:**
- Produces `createPatientPrescriptionReview(thread, file) -> PrescriptionReview` and `processPatientOnuPrescriptionUpload(thread, file) -> void`.
- Adds an assistant message action `{ type: 'prescription-review', reviewId }` to the current thread.
- Image object URLs are kept in an in-memory map keyed by review ID; they are not serialized into thread storage.

- [ ] Detect image uploads in `handlePatientOnuAttachments` while leaving existing document attachment behavior intact.
- [ ] For an image upload, append the user attachment to the current thread, show a brief processing state, then append a prescription review artifact to that thread. Do not call `beginPatientOnuAssistantFlow` and do not create a new thread.
- [ ] Create deterministic sample review content with clearly marked simulated extraction; ensure missing fields stay blank or “Not provided.”
- [ ] For non-image files, preserve current behavior and make clear they are attached but not interpreted.
- [ ] Add an artifact action that opens the review by stable review ID. Ensure the artifact remains in the thread after returning from review.

### Task 3: Build focused review and original-image viewing surfaces

**Files:**
- Modify: `patient-app.html` (Onu markup, CSS, review/edit functions, message rendering)

**Interfaces:**
- Produces `openPatientPrescriptionReview(reviewId)`, `closePatientPrescriptionReview()`, `updatePatientPrescriptionMedicine(reviewId, medicineId, field, value)`, `addPatientPrescriptionMedicine(reviewId)`, and `openPatientPrescriptionImage(reviewId)`.
- Simulated status helper: `getPatientPrescriptionMatch(name) -> { status, reason }`, with deterministic sample rules and a short debounce when typing.

- [ ] Add a review surface visually consistent with existing patient details pages and the Onu conversation shell. Store the originating thread ID and return to it on close.
- [ ] Render editable patient and prescriber fields plus medicine name/instructions rows, with a clear simulated match label and explanation.
- [ ] Add an Add medicine action; new rows start with blank name/instructions and a “Needs review” prompt instead of fabricated data.
- [ ] Re-run the local simulated name check after name edits. Describe an unmatched entry as “not matched by this demo checker,” never as wrong, unsafe, or invalid.
- [ ] Add an original-image viewer with a visible back/close action. If the browser session no longer has the object URL, explain that the image must be attached again.
- [ ] Keep **Save to Active medications** distinct from **Back to chat**. Disable save when no medicine has a name; do not save on back/close.
- [ ] Add accessible labels, keyboard focus handling, visible focus styles, and text status labels that do not rely on color alone.

### Task 4: Save medications and expose them in Profile

**Files:**
- Modify: `patient-app.html` (patient navigation, Profile page, save/return actions, Onu reply context)

**Interfaces:**
- Produces `savePatientPrescriptionReview(reviewId) -> boolean`, `navigateToPatientProfile() -> void`, and `renderPatientActiveMedications() -> void`.
- Updates `getPatientOnuReply(thread, prompt, attachments)` to use explicitly saved Active medications as prototype context; unsaved review rows are excluded.

- [ ] Enable the existing Profile navigation item and add a minimal Profile page containing an Active medications section, using the existing bottom navigation and page conventions.
- [ ] On save, atomically add the reviewed medicine rows to the active list (without duplicate rows from repeated clicks), set `savedAt`, persist the review and active list, and return to the originating conversation with a saved confirmation.
- [ ] On back to chat, return to the originating conversation without changing Active medications; retain review edits and artifact.
- [ ] Render saved names and instructions in Active medications, with a clear empty state before the first save.
- [ ] Make subsequent prototype chat replies aware of saved names when a patient asks about their medications, while keeping the response clearly simulated and non-diagnostic.
- [ ] If local save fails, leave the patient in review with their edits intact and show a retryable explanation.

### Task 5: Complete upload and storage recovery states

**Files:**
- Modify: `patient-app.html` (upload validation, recovery copy, boundary notice, responsive styles)

**Interfaces:**
- Reuse existing `PATIENT_ONU_MAX_FILE_BYTES`, `getPatientOnuFileCategory(file)`, and `showToast()` where suitable.

- [ ] Ensure invalid/unsupported files and size-limit failures explain how to recover without dropping other valid selected files.
- [ ] Add an unreadable/manual-entry state that does not claim sample values came from the image.
- [ ] Add a concise notice on review explaining that extraction and match statuses are simulated and not medical advice; do not add this disclaimer to the initial Onu home screen.
- [ ] Check layouts at the existing phone viewport widths for scrollable review content, reachable footer actions, and no controls hidden behind system/navigation areas.
- [ ] Review each acceptance criterion in the spec against the implemented flow, including same-thread return and unsaved-versus-saved behavior.
