# Patient Health Analysis Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a patient Health Analysis page for saved medicines, allergies, and long-term conditions, and make those saved health details available to Onu in future chats on this device.

**Architecture:** Extend the existing single-file patient app with a dedicated page and a shared searchable multi-select bottom sheet for allergies and conditions. Reuse the current active medication store and add a separate versioned local store for allergy and condition selections; build Onu context from these saved records at reply time.

**Tech Stack:** HTML, CSS, and vanilla JavaScript in `patient-app.html`; browser `localStorage`; existing Phosphor icons and app bottom sheet styles.

**Spec:** `docs/superpowers/specs/2026-10-17-patient-health-analysis-design.md`

## File Map

- `patient-app.html`: Page markup, bottom sheet styles, navigation, local storage, active medication rendering/removal, searchable catalogs, and Onu context integration. The prototype keeps patient UI and logic in this existing file.
- `docs/superpowers/specs/2026-10-17-patient-health-analysis-design.md`: Approved behavior and visual requirements.

## Global Constraints

- Use the app’s existing white canvas, Urbanist headings, DM Sans controls, Phosphor icons, and spacing/surfaces from `DESIGN_GUIDELINE.md`.
- Active medications continue to use `onuPatientPrescriptionData:v1`.
- Allergies and conditions use `onuPatientHealthContext:v1`.
- Do not prefill allergies or diagnoses, infer conditions from medicines, or claim clinical checks or diagnosis/treatment advice.
- Keep the bottom navigation hidden on Health Analysis and restore it when returning to Profile.
- Preserve at least 44px touch targets and provide a visible alternative to every swipe action.

## Review Focus

- Existing prescription review integrity when an active medicine is deleted: verify removal affects only the saved medication list.
- Empty and unavailable local storage: verify empty sections render safely and storage errors preserve current app behavior.
- Search and custom entries with different casing or surrounding spaces: verify duplicate prevention is case-insensitive and normalized.
- Long catalog labels and custom values on narrow phones: verify rows wrap or truncate without horizontal overflow.
- Health context changes between messages: verify edits and removals are reflected in the next Onu reply, including in an existing thread.

---

### Task 1: Add Health Analysis navigation and page structure

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Produces: `openPatientHealthAnalysis()` and `returnFromPatientHealthAnalysis()` navigation functions; page element `#pagePatientHealthAnalysis`.

- [ ] Add a `Health Analysis` app-page with a back/title header and three sections: Active medications (disclosure, initially collapsed), Allergies, and Health conditions.
- [ ] Change the Profile Health Analysis row to call `openPatientHealthAnalysis()` instead of showing the placeholder toast; shorten the subtitle to `Your health overview` if it has not already been updated.
- [ ] Implement `openPatientHealthAnalysis()` to hide the bottom navigation, activate the Health Analysis page, reset its scroll position, and render current health data.
- [ ] Implement `returnFromPatientHealthAnalysis()` to restore Profile and bottom navigation; capture and restore Profile’s `scrollTop` when opening and returning.
- [ ] Add `pagePatientHealthAnalysis` to the page-reset lists used by `navigateToDiscover()`, `navigateToVisits()`, `navigateToOnu()`, and `navigateToPatientProfile()` so stale active pages cannot remain underneath other views.
- [ ] Manually check Profile → Health Analysis → back and confirm the Profile scroll position is restored.
- [ ] Manually navigate from Health Analysis to Discover, Visits, Onu, and Profile. Confirm the Health Analysis page is reset and the bottom navigation is visible on the destination pages.

### Task 2: Render and delete Active medications

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Consumes: `loadPatientPrescriptionData()` and `savePatientPrescriptionData()`.
- Produces: `renderPatientHealthMedications()`, `togglePatientHealthMedications()`, and `removePatientHealthMedication(medicineId)`.

- [ ] Render the medication count in the initially collapsed section header and render current `patientActiveMedications` when expanded.
- [ ] Show each saved medicine’s name and available generic name, dose, frequency, and duration using compact rows and existing divider styles.
- [ ] Add left-swipe deletion and a visible remove control that calls `removePatientHealthMedication(medicineId)`.
- [ ] In `removePatientHealthMedication(medicineId)`, filter only `patientActiveMedications`, then persist with `savePatientPrescriptionData({ version: 1, reviews: patientPrescriptionReviews, medications: patientActiveMedications })` and re-render. Do not modify `patientPrescriptionReviews` or the originating review’s medicines.
- [ ] Render an empty state only when the section is expanded and no active medicines exist; include a short action returning to Onu to upload a prescription.
- [ ] Manually save a medicine through the existing prescription flow, confirm it appears here, delete it, confirm it disappears from Active medications, and confirm its original prescription review remains in chat.

### Task 3: Add allergy and condition multi-select sheets

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Produces: `PATIENT_HEALTH_CONTEXT_STORAGE_KEY`, `PATIENT_ALLERGY_CATALOG`, `PATIENT_CONDITION_CATALOG`, `normalizePatientHealthContext(raw)`, `loadPatientHealthContext()`, `savePatientHealthContext(data)`, `openPatientHealthPicker(type)`, `renderPatientHealthPicker()`, `savePatientHealthSelections()`, and `closePatientHealthPicker()`.
- Data shape: `{ version: 1, allergies: [{ id, name, category }], conditions: [{ id, name, category }] }`.

- [ ] Define the versioned local storage key and normalize stored records to the data shape above. Use case-insensitive trimmed names to prevent duplicates, including custom entries.
- [ ] Add curated, searchable allergy options grouped into medication, food, environmental, insect, and latex categories. Include a custom entry field for items not found.
- [ ] Add curated, searchable condition options grouped into heart/circulation, tumors/cancers, respiratory, endocrine/metabolic, neurological, autoimmune, kidney/liver/digestive, and other categories. Include a custom entry field.
- [ ] Build one reusable bottom sheet for both kinds of records. `openPatientHealthPicker(type)` sets the mode and temporary selected values; `renderPatientHealthPicker()` applies search/category filters; Save persists the selection set; Cancel/backdrop/Escape closes without persisting temporary changes.
- [ ] Render saved items as compact removable tags or rows with an Add action. Do not render default/sample selections. Removing an allergy or condition must update local storage and the page immediately.
- [ ] Manually check search, category changes, multi-selection, custom values, duplicate casing/spacing, Cancel, and Save.
- [ ] Refresh the page to confirm saved selections persist; remove entries and confirm they remain removed after refresh.
- [ ] Check empty results, empty saved sections, unavailable/corrupt storage behavior, and a narrow phone viewport.

### Task 4: Supply saved health context to Onu

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Produces: `getPatientOnuHealthContext()` returning a compact object with active medicine names/details, saved allergies, and saved conditions.
- Integrates with: `getPatientOnuReply(thread, prompt, attachments)`.

- [ ] Implement `getPatientOnuHealthContext()` to load the latest active medication and health context stores at reply time; omit empty sections and never infer missing health facts.
- [ ] Make `getPatientOnuReply()` use the current context for relevant medication/allergy/condition questions, while preserving the prototype’s explicit limit that it does not provide medical advice or clinical validation.
- [ ] Ensure each new reply reads current saved state so edits or removals affect existing and new threads without requiring a new chat.
- [ ] Manually add one allergy and one condition, ask a relevant question in an existing Onu thread and a new thread, remove each record, then confirm subsequent replies no longer include the removed information.

### Task 5: Final interface and interaction review

**Files:**
- Modify: `patient-app.html`

- [ ] Review section hierarchy, concise labels, safe-area spacing, touch targets, bottom sheet behavior, empty states, keyboard dismissal, and accessible expanded/selected labels against the spec and `DESIGN_GUIDELINE.md`.
- [ ] Parse all inline JavaScript with Node; confirm all inline scripts parse successfully.
- [ ] Run `git diff --check`; confirm there are no whitespace errors.
- [ ] Manually walk the acceptance criteria in `docs/superpowers/specs/2026-10-17-patient-health-analysis-design.md`; record any unavailable visual/browser checks rather than assuming they passed.
