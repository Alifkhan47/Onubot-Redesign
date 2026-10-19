# Onu In-Chat Prescription Review Design

**Status:** Approved for implementation
**Date:** 2026-10-17

## Goal

When a patient uploads a prescription photo from an existing Onu conversation, keep the patient in that conversation and guide them through a clear prescription review. The patient can inspect and correct the extracted information, save medicines to their local Active medications profile, or return to the same chat without saving. Saved medicines remain available as context for later prototype conversations.

This is a standalone UI prototype. It must not imply that it performs real OCR, searches the internet, verifies clinical safety, or persists to a remote patient account.

## Current context

The patient app is a single-page HTML prototype with local chat threads in `localStorage`. Attachments currently retain only file metadata. There is no actual patient profile screen, OCR service, medicine verification service, backend, or account storage. The provided demo is a visual reference: it uses sample records and simulated name checks, not OCR or live internet verification.

## User flow

1. The patient opens or continues an Onu chat and selects a prescription photo using the existing attachment action or camera option.
2. The uploaded image appears in that same conversation. A short processing state follows; the chat is not replaced and no new conversation is created.
3. Onu adds a prescription review artifact to the thread. It summarizes the recognized patient and doctor details and the medicine count, and explains that extraction and checks are simulated in this prototype.
4. Opening the artifact presents a focused review surface. The original uploaded image is available to inspect. Patient and doctor details and each medicine's name and dose can be edited. Each medicine shows a plain-language simulated status such as “Looks matched” or “Needs review,” with the reason available in context. Editing a medicine name re-runs the local simulated check immediately, including while typing. The UI must avoid presenting these statuses as clinical or internet verification.
5. The patient can add a medicine row and edit it using the same review controls.
6. The primary action, **Save to Active medications**, saves the reviewed medicine list and relevant prescription metadata to local prototype storage, then returns to the same chat with a clear saved confirmation. The chat artifact stays available.
7. **Back to chat** returns to the same conversation without saving. It preserves the uploaded image and review edits in the chat artifact so the patient can reopen the review later. This action must be visually distinct from Save and must not silently save medicines as active.
8. Later chat turns may reference medicines explicitly saved to Active medications, using the existing prototype's simulated response behavior. They must not imply that unsaved review edits are active medications.

## UI and interaction design

- Keep the existing chat shell, navigation behavior, typography, palette, and primary button styling.
- Treat prescription review as a focused detail screen or overlay opened from the in-thread artifact, not as a separate conversation.
- Make the distinction between **Save to Active medications** and **Back to chat** explicit using labels and concise supporting copy. Avoid ambiguous labels such as “Save” or “Done.”
- Keep the artifact compact in the conversation, showing processing/review state and a clear action to review details.
- Show original image access from the review surface, with a close/back action that returns to the review.
- Provide understandable empty/error states for unreadable images and incomplete medicine entries. The patient can correct or add entries, or return to the chat; saving an empty list is disabled.
- Preserve attachments and review data across reloads within the local prototype where feasible. Use browser local storage only; do not claim account-level persistence.
- Keep touch targets accessible, labels associated with inputs, focus states visible, and status meaning conveyed with text rather than color alone.

## Prototype processing behavior

- Accept photo uploads from the existing chat attachment flow. Keep supported image types aligned with the input control; unsupported files should receive a clear inline explanation.
- Use a deterministic, clearly labeled sample extraction for the demo flow. Do not upload the image, call external OCR, or transmit patient information.
- Run a deterministic local name check on medicine edits, with a short debounce to avoid flickering while the patient types. “Needs review” must explain that the sample checker could not match the entered text, not that the medicine is invalid.
- If the image type or content cannot be meaningfully processed by the local prototype, show a review state that invites manual entry instead of inventing confidence. Any sample extraction should be visibly marked as demo data.
- This behavior is a UI simulation only. Real OCR, internet medicine lookup, identity extraction, and clinical validation require separate services and are out of scope.

## Local data model

Use a small, versioned local-storage model alongside the existing thread store:

- **Prescription review:** stable ID; owning thread ID; attachment metadata and local preview reference when available; patient name and details; prescriber name and details; medicine rows; per-row simulated status/reason; last edited time; saved state.
- **Medicine row:** stable ID; name; dose/instructions; optional strength; simulated match status and explanation.
- **Active medications:** medicines saved by the patient, linked back to the prescription review and carrying a saved timestamp.

Use `FileReader`/data URLs or an equivalent local mechanism only if the prototype needs the photo to survive reloads. Avoid writing oversized image data into localStorage without a reasonable size limit and a graceful fallback. If preview persistence is unavailable, preserve the file metadata and tell the patient they may need to re-upload to view the image after reload.

Storage reads should tolerate missing, malformed, or older values and fall back without breaking chat. The existing thread identifier is the source of truth for returning to the same conversation. Do not duplicate or fork chat threads when opening and closing review.

## Failure and safety states

- **Unreadable or unavailable image:** explain that the prototype could not extract it; offer manual medicine entry and return to chat.
- **Uncertain medicine match:** label “Needs review,” say the demo checker did not find a confident sample match, and let the patient edit or keep the name. Do not assert the medication is wrong or unsafe.
- **Missing details:** leave fields blank or mark them “Not provided”; do not invent patient, prescriber, or dosing data.
- **Storage failure or quota:** explain that the list could not be saved locally and leave the review intact so the patient can retry or return to chat.
- **Clinical boundary:** include a concise notice on the review surface that the prototype extraction and match status are simulated and are not medical advice. Do not repeat a long warning in the initial chat home screen.

## Out of scope

- Real OCR or document understanding.
- Live web search, external medicine databases, or medication safety checks.
- Cloud/account synchronization or a production medical record.
- Editing the existing visual design outside the chat upload-to-review path and the minimum Profile surface needed to display locally saved Active medications.
- A new chat type or standalone prescription conversation.

## Acceptance criteria

1. Uploading an image while inside an existing chat keeps the same thread open and adds the image and prescription artifact there.
2. The artifact opens an editable review with patient/prescriber details, medicine name and dose rows, simulated match explanations, add-medicine action, and original-image viewing.
3. Medicine-name edits refresh the simulated status while typing without claiming internet verification.
4. Saving clearly adds the reviewed medicine rows to the local Active medications profile and returns to the originating chat with confirmation.
5. Returning to chat without saving preserves the review artifact and does not add medicines to Active medications.
6. A later prototype chat can reference saved Active medications; unsaved medicines are not treated as active.
7. Unreadable input, missing fields, unsupported upload, and local-storage failure have recoverable states.
8. The design retains the app's existing visual system and clearly labels all simulated extraction and checking.
