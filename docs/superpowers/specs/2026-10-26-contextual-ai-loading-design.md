# Contextual AI Loading and Plain Text Replies

## Intent
Make the patient and doctor chat demos feel active during a several-second simulated AI wait. Use progress copy that changes with the request, and show prescription upload progress through recognizable review steps. Render doctor AI replies as plain text so formatting stays consistent.

## Goals and limits
- For patient and doctor chat replies, show a small animated status whose wording moves through context-specific stages before the demo response appears.
- For patient prescription uploads, animate staged statuses such as scanning the prescription, detecting medicines, and preparing the review before showing the existing review.
- Keep progress clearly presentational; do not imply that real OCR or generative AI is running.
- Preserve existing replies, chat history, prescription review behavior, and controls.
- Render doctor response content as plain text with intentional line breaks, without Markdown/HTML styling.

## Approaches considered
- **Inline rotating status:** change a compact animated status in place. This keeps the chat lightweight and supports contextual copy.
- **Expanded progress card:** show a larger animated card for every response. This is more prominent but adds visual weight to ordinary turns.
- **Inline for replies, staged card for prescription review (chosen):** ordinary replies stay compact, while the longer upload gets a distinct sequence of steps that suits the wait.

## Implementation calls
- Add a few seconds of staged demo delay, with status text selected from the user's message context.
- Give prescription uploads their own timed steps and retain the existing review card as the completion state.
- Use an accessible live status and honor reduced-motion preferences for decorative animation.
- Convert doctor AI reply markup to a safe text-only container with preserved newlines; retain existing action controls.

## Builder choices
The builder may choose exact timings, animation details, and context keyword groups to fit the existing prototype styles, while keeping status changes readable and the total demo wait to a few seconds.
