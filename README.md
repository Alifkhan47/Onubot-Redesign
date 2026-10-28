# Onu App Prototypes

A set of three interactive, mobile-first HTML demos for exploring the Onu experience—from sign-in and onboarding to patient care and the doctor workspace.

## Start here

**To review login and onboarding, open [`onubot-app.html`](./onubot-app.html) first.** It begins with the sign-in experience and includes the doctor network onboarding flow.

You can open any demo directly in a modern browser, or serve the project folder locally:

```sh
python -m http.server 8000
```

Then visit [localhost:8000](http://localhost:8000) and open the HTML file you want to explore. No package installation or build step is required. Some fonts, icons, and sample imagery load from external services and may need an internet connection.

## The three demos

| File | What it contains | Open it when… |
| --- | --- | --- |
| [`onubot-app.html`](./onubot-app.html) | Login, sign-in choices, and doctor network onboarding/profile setup. | You want to start with login or onboarding. |
| [`patient-app.html`](./patient-app.html) | Patient discovery, doctor search, booking, visits, Onu chat, prescription review, health information, and profile. | You want to explore the patient journey. |
| [`doctors-app.html`](./doctors-app.html) | Doctor Onu assistant, desk and queue, schedule, consultation, notes and prescription, appointments, patient records, wallet, and profile. | You want to explore the doctor workflow. |

## Feature guide

### Login and onboarding — `onubot-app.html`

- Patient sign-in entry and doctor network entry.
- First-time patient basic information page before opening the patient app.
- Doctor onboarding and profile setup.
- Onboarding preview and progress flow.

### Patient app — `patient-app.html`

- Discover and search for doctors by name or specialty.
- View doctor profiles and choose a consultation type, date, and time.
- Review booking details and explore the Visits and appointment detail flows.
- Use Onu chat for a demo specialty suggestion or prescription review.
- Explore alerts, health information, documents, and profile settings.

### Doctor app — `doctors-app.html`

- Use the Onu clinical assistant and doctor desk.
- Review the patient queue and schedule shifts.
- Explore the consultation, pre-visit information, AI notes, and prescription workflow.
- Browse appointments, patient records, wallet, and profile screens.

## Using and editing the project

- The HTML files are standalone prototypes. Their page markup, CSS, and JavaScript are currently kept in each file.
- There is no backend. Sign-in, booking, payments, video calls, AI responses, and clinical workflows are demonstrations, not real services.
- Most interaction state is temporary. The patient app saves selected information in browser storage; the onboarding demo keeps some preview state for the current browser session.
- Edit the HTML file for the app or flow you are changing. Check related element IDs and inline event handlers when changing navigation or interactions.
- Preview changes at a mobile viewport and follow the affected flow from beginning to end.
- The prototypes use the fixed demo date **Tuesday, September 29, 2026**.

## Project reference

- [`DESIGN_GUIDELINE.md`](./DESIGN_GUIDELINE.md) — visual styles and interface conventions.
- [`AI_INSTRUCTIONS.md`](./AI_INSTRUCTIONS.md) — project behavior and implementation guidance.
- `assets/` — local images and illustrations.
- `phosphor-embedded.css` — local Phosphor icon styles.
