# Onu Telemedicine Ecosystem — Doctor & Patient Web Prototypes
> **Modern Minimalist Healthtech Platform for Doctors and Patients**  
> *Inspired by Western / European design standards: Wise, Uber, Hims, Alan Health, and Qonto.*

---

## 🌟 Overview & Dual-App Architecture

The repository contains the complete interactive, high-fidelity prototypes for both sides of the Onu Telemedicine ecosystem:

1. **🩺 Doctor App ([`doctors-app.html`](./doctors-app.html))**:
   - Clinical desk management, patient queue conveyor belt, ambient AI notes, shift scheduling, live video consultations, and digital prescription issuance.
2. **👤 Patient App ([`patient-app.html`](./patient-app.html))**:
   - Care discovery, instant universal search, boxless specialist directory, interactive appointment booking (Video Call vs Chamber Visit), live visits tracker, alerts, and Onu AI triage assistant.

Both apps feature a top ecosystem switcher bar enabling seamless switching between doctor and patient views.

---

## 🚀 Patient App Highlights ([`patient-app.html`](./patient-app.html))

- **🧭 Redesigned Discover Page**:
  - Crisp header with location chip (`Dhaka, BD`).
  - Instant universal search bar with quick focus.
  - Hero Care Category: **Specialist Doctors** (2,300+ verified doctors with instant video and chamber visits).
  - Specialty fast-browse horizontal strip (Cardiology, Medicine, Pediatrics, Neurology, Dermatology, Gynecology, Orthopedics).
  - Live "Available Today" spotlight doctor card with quick booking.
  - Future Care preview (Hospitals & Diagnostics) with subtle "Coming Soon" badges.
- **🔍 Redesigned "Find a Doctor" Directory (Zero Card Fatigue)**:
  - Box-less list rows with subtle hairline dividers (Uber/Wise standard).
  - Doctor avatar with online/offline live status dot.
  - BMDC verified seal, qualifications, chamber hospital, and rating score.
  - Bold consultation fee (`৳ 1,200`) and next available slot pill.
  - Live search filtering by doctor name, specialty, hospital, or symptoms.
  - Horizontal filter chips with strict selection tokens (`#D6EAE6` + `#7EB8AE` border).
- **📅 Interactive Doctor Booking Sheet**:
  - Mode selection: `Video Call (Online)` vs `Chamber Visit (In-Person)`.
  - Date pills and available slot grid (`03:30 PM`, `04:00 PM`, etc.).
  - One-tap booking confirmation with animated toast and instant slotting into the Visits tab.
- **✨ Onu AI Health Triage**:
  - Center bottom nav sparkle action opening an interactive AI symptom matcher that matches patients with the right specialist in one tap.
- **📱 Master 5-Tab Navigation**:
  - `Discover`, `Visits`, center `Onu AI`, `Alerts`, and `Profile`.

---

## 🩺 Doctor App Highlights ([`doctors-app.html`](./doctors-app.html))

- **🏠 My Desk (Operational Dashboard)**:
  - Real-time shift status with locked state protection (`Shift Locked Until 8:58 AM`) and 2-minute auto-unlock protocol before shift start.
  - Interactive demo time simulation (tap status bar clock to toggle between Locked `8:22 AM` and Ready `8:58 AM`).
  - Online/Offline availability toggle with subtle red alert feedback and auto-cancellation handling.
  - Financial overview showing total income and available balance.
- **📹 Live Video Consultation & Ambient AI**:
  - Fullscreen video consultation interface with Picture-in-Picture (PiP) doctor tile.
  - In-call patient pre-visit intake drawer.
  - One-tap patient skipping (with automated return re-queuing 3 turns ahead).
  - Ambient AI audio transcription transition into structured clinical notes.
- **📝 Consultation Review & Rx Finalization**:
  - Editable AI-generated Chief Complaint summary.
  - Medication stack builder with dosage, frequency, and duration.
  - Diagnostic lab tests with priority tagging (`Routine` / `Urgent`).
  - Specialist referral selector and follow-up chips.
  - Official PDF-like digital prescription preview with doctor credentials.
- **📅 Calendar Strip & Shift Management**:
  - 7-day horizontal calendar strip.
  - Shift editor modal with patient capacity controls and repeat settings.
  - Destructive action protection with confirmation bottom sheet modals.
- **📋 All Appointments & Shift History**:
  - **Upcoming Tab**: Live shift queues from Today through future dates with active turn highlights.
  - **History Tab**: Completed consultations and past records chronologically sorted.
  - Multi-parameter filter sheet (Status, Consultation Type, Shift).
  - Appointment Clinical Details with dynamic relevance sorting and empty intake states.
- **💰 My Wallet & Payout System**:
  - Elevated Available Balance card with live "Ready to withdraw" chip and primary Withdraw CTA.
  - Symmetrically aligned two-column collapsible breakdown for Today and Total earnings.
- **👤 Doctor Profile & Practice Details**:
  - Spacious boxless layout with prominent credentials, chamber address, phone, bio, and settings.

---

## 🎨 Unified Design System

- **Canvas**: Pure White (`#FFFFFF`)
- **Surface Cards**: Soft Neutral (`#F6F8F9` with `1.5px solid #EDF2F1`)
- **Hero / Active Elements**: Soft Sage (`#D6EAE6` with `1.5px solid #7EB8AE`)
- **Primary CTAs**: Deep Forest Green (`#052E28`)
- **Typography**: `Urbanist` (Headings & Metrics) & `DM Sans` (Body/Meta)
- **Icons**: Phosphor Icons (Regular weight)

For comprehensive design system guidelines, see [`DESIGN_GUIDELINE.md`](./DESIGN_GUIDELINE.md).  
For AI pair programming context and architecture rules, see [`AI_INSTRUCTIONS.md`](./AI_INSTRUCTIONS.md).

---

## 💻 How to Run

1. Clone or download the repository.
2. Open [`doctors-app.html`](./doctors-app.html) or [`patient-app.html`](./patient-app.html) directly in any modern web browser.
3. Use the top switcher button on either app to toggle between Doctor and Patient experiences.
4. No build step, package manager, or server dependencies required!

---

## 📁 Project Structure

```
.
├── doctors-app.html        # Doctor Desk & Shift Management SPA Prototype
├── patient-app.html        # Patient Care Discovery & Booking SPA Prototype
├── phosphor-embedded.css   # Embedded Phosphor icons stylesheet
├── DESIGN_GUIDELINE.md     # Visual design system, tokens, and UI SOPs
├── AI_INSTRUCTIONS.md      # AI context, state machine specifications, and developer guides
└── README.md               # Project overview and documentation
```
