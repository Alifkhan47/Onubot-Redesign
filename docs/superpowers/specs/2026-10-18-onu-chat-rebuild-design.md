# Onu Chat Rebuild Design

## Goal

Rebuild the patient app’s Onu chat area as an isolated mobile interface that preserves its current appearance and capabilities while making chat history and prescription review open reliably in the phone viewport.

## User intent

- Keep the existing Onu visual language and familiar chat layout.
- Make the hamburger open chat history from the right edge on both home and conversation views.
- Keep prescription upload and review usable without the screen clipping or sliding off the left edge.
- Preserve all existing chat options, data, and integrations with the patient app.

## Existing capabilities to preserve

- Onu home greeting, upload prescription and book appointment suggestions, message composer, and attachment menu for photos, camera, and documents.
- New chat, saved chat history grouped by Today, Previous 7 Days, and Older, and reopening a saved conversation.
- Text messages, simulated assistant replies, the health information disclaimer, and browser speech recognition when available.
- Booking intake for reason, duration, and optional symptoms; specialty recommendation; and handoff to the doctor list with a return path to the same chat.
- Prescription upload feedback, review of patient and prescriber details, editable medication fields, medicine verification states, add/delete medicine, original-image viewing, save to Active Medications, and use as context in the current chat.
- Current local storage keys and data shape for saved Onu conversations and prescription data.

## Visual direction

Retain the current Onu styling: white screen, existing navy text and teal accents, mint user bubbles, simple Phosphor icons, current typography tokens, and a bottom composer dock. Keep the design tap-first with accessible touch targets. The history panel remains a white right-side drawer with a dimmed backdrop. Prescription review keeps its current form hierarchy and fixed bottom actions.

## Architecture

Create one isolated Onu feature root directly under `.phone-screen`, separate from the horizontally sliding `.app-page` elements. The Onu root owns its header, home, conversation, history drawer, attachment menu, booking intake, and prescription review views. A small controller owns the current view, open drawer/menu, active thread, active review, and return destination. It renders or switches only Onu-owned content; it does not manipulate unrelated app pages except through the existing navigation handoffs.

Use one active Onu screen at a time: `home`, `conversation`, or `prescription-review`. Keep history and attachment choices as lightweight panels owned by the Onu root. The history drawer has its own explicit open/close state. Prescription review is a screen within the same fixed root, with a back action to the originating conversation. Do not stack a second app-page transition on top of an Onu transition. The drawer can slide horizontally from the right; prescription review uses a short opacity transition or an immediate state switch, not a horizontal page transform.

Preserve the existing public entry points used elsewhere in `patient-app.html`—including `navigateToOnu`, `startPatientOnuPrescriptionChat`, `openPatientOnuRecommendedDoctors`, and the return-from-doctor-list path—as thin adapters to the new controller. Keep the chat and prescription storage contracts unchanged.

## View and interaction behavior

1. Opening Onu from the bottom navigation shows the home view and preserves the existing tab behavior.
2. The hamburger is present on home and conversation views. Tapping it always opens history from the right; tapping the close button, backdrop, or Escape closes it and restores focus to the opener. Selecting a thread closes history and opens that conversation.
3. Starting a new chat resets the active conversation and returns to the current home/chat behavior without deleting saved chats.
4. Submitting a message appends the user message and existing simulated assistant response, scrolls the conversation to the latest turn, and persists the thread.
5. Uploading supported files keeps the current size/type checks and visible feedback. Prescription processing updates the originating thread, then opens that review in the same Onu root only if that thread is still the active view. Opening history or leaving Onu cancels the automatic review handoff.
6. Closing or completing prescription review returns to its originating chat. Saving still writes to Active Medications; “Use in chat” still adds medication context to the originating thread.
7. Booking intake keeps its current prompts and doctor-list handoff. Returning from doctor results restores the same Onu conversation.
8. If voice recognition is unavailable or an upload/storage operation fails, keep the current message and show the existing inline or toast feedback without changing screens.
9. Every transition has a visible destination or recovery state. In particular, tapping the hamburger must never open prescription review, and completing a prescription upload must never leave a blank phone screen. While processing, show progress in the conversation; after success, show the complete review; on failure, return to the conversation with an actionable message.

## Accessibility and motion

- Use semantic buttons, dialogs, and headings; label all icon-only controls.
- Keep primary tap targets at least 44 by 44 CSS pixels and preserve visible keyboard focus.
- Keep focus inside the history panel while open, restore focus on close, and support Escape.
- Give prescription review a clear back control and maintain a visible keyboard focus path through form fields and bottom actions.
- Respect `prefers-reduced-motion`; the UI must remain fully usable with transitions disabled.
- Avoid horizontal overflow at the narrowest supported phone width.

## Error handling and data

Continue to handle unavailable or malformed local storage with in-memory chat state and user feedback. Preserve the existing file type and 15 MB size checks. Keep prescription processing visibly in progress, recover to the conversation if processing cannot complete, and do not open a review belonging to another or inactive thread.

## Out of scope

- Changing the chat response content, medical behavior, booking logic, doctor matching, prescription data model, or patient app’s other pages.
- Adding a server, package, or third-party chat service.
- Reworking the wider patient app navigation or its non-Onu page transitions.

## Acceptance criteria

- The home and conversation hamburger buttons both open the history drawer from the right edge of the phone screen.
- Opening or closing history never navigates to prescription review or changes the active patient app page.
- Prescription upload opens a correctly aligned review view; its full header, content, and fixed actions remain within the phone screen, including after returning to the same chat. At no point does upload produce a blank screen.
- Tapping either hamburger from home or conversation displays the Chats drawer, not any other view.
- The listed chat, booking intake, voice, attachment, history, prescription review, and medication-context features remain functional.
- Onu internal transitions do not inherit transforms or clipping from the patient app’s `.app-page` transitions.
- The rebuilt interface matches the existing Onu visual style and supports reduced motion, keyboard focus, and touch interaction.

## Verification expectations

Exercise the flows on the actual patient app preview at narrow phone dimensions: home to history and close by each supported method; conversation to history and back; new chat; text send; each attachment option; prescription processing, review, back, save, and use in chat; booking intake through doctor results and return; and voice input both available and unavailable. Confirm no horizontal clipping and inspect the browser console for errors during each flow.
