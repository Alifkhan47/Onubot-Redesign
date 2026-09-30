# Onu App — Doctor's Telemedicine & Desk Prototype
> **Modern Minimalist Healthtech Platform for Doctors**  
> *Inspired by Western / European design standards: Wise, Uber, Hims, Alan Health, and Qonto.*

---

## 🌟 Overview

**Onu App** is an interactive, high-fidelity clinical telemedicine and desk management prototype built for doctors and healthcare specialists. Designed with a pure white canvas, soft neutral surfaces, and zero cognitive clutter, it enables doctors to review queues, conduct video visits, and issue prescriptions with maximum efficiency.

---

## 🚀 Key Features

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

---

## 🎨 Design System

- **Canvas**: Pure White (`#FFFFFF`)
- **Surface Cards**: Soft Neutral (`#F6F8F9` with `1.5px solid #EDF2F1`)
- **Hero / Active Elements**: Soft Sage (`#D6EAE6` with `1.5px solid #7EB8AE`)
- **Primary CTAs**: Deep Forest Green (`#052E28`)
- **Typography**: `Urbanist` (Headings) & `DM Sans` (Body/Meta)
- **Icons**: Phosphor Icons (Regular weight)

For comprehensive design system guidelines, see [`DESIGN_GUIDELINE.md`](./DESIGN_GUIDELINE.md).  
For AI pair programming context and architecture rules, see [`AI_INSTRUCTIONS.md`](./AI_INSTRUCTIONS.md).

---

## 💻 How to Run

1. Clone or download the repository.
2. Open `index.html` directly in any modern web browser (Chrome, Edge, Safari, Firefox).
3. No build step, package manager, or server dependencies required!

---

## 📁 Project Structure

```
.
├── index.html              # Single-page interactive prototype (HTML5 + CSS3 + Vanilla JS)
├── DESIGN_GUIDELINE.md     # Visual design system, tokens, and UI SOPs
├── AI_INSTRUCTIONS.md      # AI context, state machine specifications, and developer guides
└── README.md               # Project overview and documentation
```
