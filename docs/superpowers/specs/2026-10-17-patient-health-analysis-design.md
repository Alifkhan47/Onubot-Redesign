# Patient Health Analysis Page Design

**Status:** Approved
**Date:** 2026-10-17
**Scope:** Patient app prototype (`patient-app.html`)

## Goal

Give patients one clear place to review saved medicines and record allergies and long-term health conditions. Information saved here should be available to Onu in future conversations on the same device.

## Entry and navigation

- Tapping **Health analysis** on Profile opens a dedicated `Health Analysis` page.
- The page uses the app’s standard white canvas, Urbanist headings, DM Sans controls, Phosphor icons, and spacing/surfaces from `DESIGN_GUIDELINE.md`.
- A back button returns to Profile. The bottom navigation is hidden while this subpage is open and restored when returning.
- Page scroll position resets when opened; returning to Profile restores its normal page state.

## Page structure

### Active medications

- Section is collapsed by default and shows the active medication count.
- Expanding it reveals saved medicines from the existing prescription medication store. A row shows the medicine name and available generic name, dose, frequency, and duration.
- Medicines can be removed with a left swipe and a visible, accessible remove action. Removal deletes the active medication entry but leaves its original prescription review intact.
- With no saved medicines, the expanded section gives a short explanation and a link back to Onu to upload a prescription.

### Allergies

- Shows saved allergies as compact removable tags/list rows and an **Add** action.
- **Add** opens a bottom sheet with search, category filters, multi-select checkboxes, a selected count, and a save action. The sheet includes common medication, food, environmental, insect, and latex allergies, plus a way to add a custom entry when the list has no match.
- Selecting an item does not save it until the patient taps **Save**. Duplicate entries are prevented.
- Empty state says no allergies have been added. The prototype does not assume that no recorded allergies means “no known allergies.”

### Health conditions

- Shows saved conditions as compact removable tags/list rows and an **Add** action.
- **Add** opens a matching searchable multi-select bottom sheet. Categories cover heart and circulation, tumors and cancers, respiratory, endocrine/metabolic, neurological, autoimmune, kidney/liver/digestive, and other conditions. Custom entries are supported.
- Conditions are only added when selected by the patient; the page does not prefill diagnoses or infer them from medication names.
- Empty state says no conditions have been added.

## Chat context and persistence

- Active medications continue to use `onuPatientPrescriptionData:v1`, the existing store for prescription reviews and saved medicines.
- Allergies and conditions use a separate versioned local store, `onuPatientHealthContext:v1`, so existing profile and prescription data remain compatible.
- Onu’s response context is built from saved medications, allergies, and conditions for every conversation. The prototype keeps this on-device and does not claim that it performs clinical checks or provides diagnosis/treatment advice.
- Deleting an allergy or condition removes it from future Onu context. Deleting an active medication removes only the active entry; the original review remains available in chat.
- Storage failures leave current UI state intact where possible and show the app’s existing toast feedback.

## Interaction and visual behavior

- Section headers use clear labels, counts where useful, and caret controls for disclosure.
- Selection sheets reuse the app’s bottom sheet: drag handle, concise title, search field, scrollable categorized options, and paired Cancel/Save actions.
- Keep list rows compact and lightly divided. Avoid nested cards and long instructional copy.
- Provide accessible names and expanded/selected states for disclosure and selection controls. Each swipe removal has an equivalent visible remove action for keyboard and assistive technology users.
- Respect safe areas, preserve at least 44px touch targets, and reduce nonessential motion when reduced motion is enabled.

## Acceptance criteria

1. Health Analysis opens from Profile and returns to Profile with the back control.
2. Active medications are collapsed initially, expand to show saved entries, and can be removed without deleting their prescription review.
3. Allergy and condition sheets support searching, category filtering, multi-selection, custom values, duplicate prevention, and explicit Save/Cancel behavior.
4. Saved selections persist after a page refresh and are included in subsequent Onu conversation context.
5. No sample conditions or allergies appear until added by the patient.
6. The page follows the existing patient app visual system and remains usable on narrow phone screens.

## Design decision

Use one Health Analysis page with separate searchable multi-select bottom sheets for allergies and conditions. This approach and the written spec were approved by the user in chat on 2026-10-17.
