# Patient Onu Chat Design

## Purpose

Replace the disabled Onu AI tab in the patient prototype with a patient-facing health assistant experience. The design uses familiar ChatGPT and Claude conversation patterns while following the patient app's existing Onu visual system and navigation.

## Product Direction

- Use the patient app's current white canvas, Urbanist headings, DM Sans supporting text, Phosphor icons, forest green primary action (`--color-primary-btn`), sage accents, and restrained borders.
- Keep the conversation readable and calm. User messages use a pale sage surface; assistant responses remain plain text on white with clear paragraph spacing.
- Keep doctor-facing clinical copilot tools and data separate. The patient assistant uses a simple patient-facing prototype response flow.
- Keep patient navigation predictable: bottom navigation is present on the fresh-chat home and hidden during a conversation, matching the supplied references.

## Entry and Fresh Conversation

- Rename the center bottom navigation label from `Onu AI` to `Onu`, enable it, and make it open the Onu page.
- The fresh-chat home header has a left history button styled like the app's existing circular page buttons and a centered `Onu` title.
- Show a distinct welcome layout and two clear actions: `Upload prescription` and `Book appointment`.
- `Upload prescription` opens a new conversation, gives a prototype-only prompt, and opens the multiple-file picker for images and PDFs. Selected file names appear as user attachments followed by a clearly simulated response.
- `Book appointment` opens a guided conversation. Onu asks the patient's main concern, duration, and other symptoms before suggesting a doctor specialty and offering a button to browse that specialty.
- Both action cards enter the conversation interface; neither sends the patient directly to doctor discovery.
- Keep the composer fixed above the patient bottom navigation. It supports text, attachment, and microphone controls, plus an accessible send action. Keep the medical-information disclaimer visible above the composer.
- The bottom navigation remains visible while this empty state is active.

## Active Conversation

- Sending the first text or adding a file starts a conversation. Hide the patient bottom navigation for this state; keep it visible on the empty-chat home.
- The header becomes: Back on the left; centered `Onu`; icon-only New chat and History buttons on the right, in that order. Use the same circular button style as other patient app pages.
- Back returns to the fresh-chat home. New chat clears the visible conversation and opens a new fresh-chat session without deleting saved threads.
- Keep the composer anchored above the home-indicator safe area. It supports multi-line text, attachments, microphone input, and send.
- Render uploaded files as compact attachment tiles that show filename and file type. Render simulated assistant replies as calm, readable response blocks. Never imply a real AI analysis or file upload occurred beyond the local prototype.
- After the first user turn, save the thread locally. Use the initial prompt or first file name as its title. Reopening a saved thread restores its messages and attachments.

## Thread History Drawer

- The hamburger button opens a side panel from the left with an overlay, a `New chat` action, and recent threads grouped by recency.
- Selecting a thread closes the drawer, restores that conversation, and keeps the conversation header and hidden bottom navigation.
- Selecting `New chat` returns to the fresh-chat home, clears only the current draft/conversation, and preserves saved threads.
- Close the drawer from its close control, tapping the backdrop, or pressing Escape. Keep touch targets at least 44px and expose expanded/selected states accessibly.

## State Model

The patient Onu experience has these visible states:

1. `home_empty`: greeting, action cards, composer, bottom navigation visible.
2. `conversation_new`: first prompt/file has been submitted; conversation header, stream and composer visible; bottom navigation hidden.
3. `conversation_saved`: a locally stored thread is open; same conversation layout with restored content.
4. `history_open`: left drawer overlays the current home or conversation without losing draft or scroll position.

State transitions:

- Onu tab -> `home_empty`.
- Submit text or select Upload prescription or Book appointment from home -> `conversation_new`.
- History -> `history_open`; select saved thread -> `conversation_saved`.
- Back or New chat -> `home_empty`.
- Close history -> restore the state beneath the drawer.
- Guided doctor flow -> specialty suggestion -> matching doctor-discovery page.

## Persistence and Prototype Boundaries

- Store thread records in browser `localStorage` so the prototype preserves conversations after navigation or reload.
- Store message text, generated titles, timestamps, and attachment metadata only. Do not store the contents of patient files in local storage.
- Simulate assistant responses and specialty suggestions locally. Clearly label prototype behavior; do not claim to analyze documents or diagnose patients.
- Reuse the app's existing page and bottom-nav transitions. Do not change `doctors-app.html`, visit lifecycle logic, payment flow, or pre-visit intake.

## Accessibility and Responsive Behavior

- Use semantic buttons for navigation and actions, visible keyboard focus, and descriptive labels on icon-only controls.
- Announce newly added user and assistant messages through a polite live region without moving focus.
- Keep all composer and header actions at least 44px high and respect the phone's top and bottom safe areas.
- Support narrow phone widths without horizontal scrolling; long filenames wrap or truncate with an accessible full name.
- Respect reduced-motion preferences for the drawer and page transitions.

## Scope

- Modify `patient-app.html` to add the patient Onu page, composer, upload interaction, local conversation model, thread-history drawer, and navigation state handling.
- Keep the existing doctor Onu copilot in `doctors-app.html` unchanged.
- No backend, network model call, remote storage, or real medical analysis is introduced.

## Acceptance Criteria

- The center navigation item is enabled and labeled `Onu`.
- Opening Onu shows the redesigned fresh-chat home with the left history menu, welcome mark, upload and doctor-finding actions, composer, disclaimer, and visible bottom navigation.
- Sending text, selecting Upload prescription, or selecting Find a doctor changes to conversation mode and hides bottom navigation. The conversation header uses the app's standard circular icon buttons for Back, New chat, and History.
- Back returns to the fresh-chat home; New chat does not remove stored threads.
- History opens from the left, preserves the underlying state, lists saved threads, and restores the chosen thread.
- Conversations persist locally across page navigation and reload; uploaded file contents are not persisted.
- Book appointment starts a guided concern-and-duration chat, then suggests a specialty and opens matching doctor results when selected.
- The patient Onu UI uses current patient app colors and typography rather than copying reference colors.
- Keyboard focus, accessible labels, live message announcements, minimum tap sizes, safe areas, and reduced motion are handled.
