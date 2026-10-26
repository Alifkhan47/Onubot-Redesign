# Contextual AI Loading and Plain Text Replies Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make demo AI replies and prescription uploads feel active with contextual staged loading, and make doctor replies display as plain text.

**Architecture:** Keep the two standalone HTML prototypes self-contained. Add reusable in-page status markup and timers to existing reply flows, and have the doctor response engine return plain text plus its existing action toolbar instead of formatting response prose as HTML.

**Tech Stack:** HTML, CSS, vanilla JavaScript.

**Spec:** `docs/superpowers/specs/2026-10-26-contextual-ai-loading-design.md`

## Global Constraints

- Loading is presentational; no real OCR or generative AI is claimed.
- Ordinary replies use compact contextual stages; prescription upload uses a more distinct sequence.
- Preserve existing chat history, review, and action behavior.
- Doctor reply content is plain text with preserved line breaks.
- Respect reduced-motion preferences for decorative effects.

## Review Focus

- Empty, short, or unmatched patient prompts should still receive a valid contextual loading sequence.
- Repeated sends should not let an old timer replace a newer turn's status or content.
- Multiple uploaded prescription photos should each reach the correct review artifact.
- Doctor responses containing punctuation, quotes, ampersands, or line breaks must remain safe and readable as text.
- Regeneration must retain status behavior and still append the correct plain-text response.

---

### Task 1: Patient Chat and Prescription Progress

**Files:**
- Modify: `patient-app.html`

**Interfaces:**
- Use `getPatientOnuReply(thread, prompt, attachments)` to obtain the existing response before starting the staged delay.
- Keep `processPatientOnuPrescriptionUpload(file, autoOpen)` as the upload entry point and preserve its review action.

- [x] Add compact animated status markup and reduced-motion styling for ordinary replies and staged prescription progress.
- [x] Update `appendPatientOnuTurn` to show several timed, context-sensitive status labels before rendering the already-computed reply, and announce completion through the existing live region.
- [x] Update `processPatientOnuPrescriptionUpload` to progress through scanning, medicine detection, and review preparation before switching to the existing review state.
- [x] Confirm by code inspection that status timers are scoped to their turn, status updates are accessible, and current history/review flow remains intact.

### Task 2: Doctor Chat Progress and Plain-Text Responses

**Files:**
- Modify: `doctors-app.html`

**Interfaces:**
- `generateOnuClinicalResponse(query)` remains the response entry point used by send and regenerate.
- `copyAiResponse`, `speakAiResponse`, and response action buttons continue to target `.onu-msg-ai-text`.

- [x] Add contextual staged status markup and CSS using the existing chat visual language; honor reduced-motion preferences.
- [x] Update send and regenerate flows to use a multi-second sequence whose labels reflect query themes such as patient lookup, schedule, earnings, or general drafting.
- [x] Render response prose and structured artifact details as escaped plain text with preserved line breaks; keep response action buttons.
- [x] Confirm by code inspection that all response branches use a text container safely and that copy, read-aloud, and regenerate controls still locate the response text.

## Verification

- Do not add or run automated tests unless requested.
- Inspect the final diff and relevant HTML/CSS/JavaScript call paths for both apps.
