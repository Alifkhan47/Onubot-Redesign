# Onu App — UI/UX Design System & Autonomous Redesign SOP
*European / Western Minimal Healthtech Standard (Inspired by Hims, Uber, Wise, Alan Health, Qonto)*

---

## 1. Core Visual Foundations & Color Tokens

Every screen in the Onu App prototype **MUST strictly** use these exact color codes and typography rules.

### 1.1 Strict Color Tokens & Action vs. Selection Hierarchy

| Token | Exact Hex | Role & Application |
| :--- | :--- | :--- |
| `--color-primary-btn` | **`#052E28`** | **Primary Action Buttons ONLY**: High-focus CTAs (`Save Shift`, `Start Shift`, `Join Video Call`, `+ Add Shift`, `Go Offline`). **DO NOT** use as a solid fill for multi-selection chips, segment controls, or active calendar date pills. |
| `--color-card-sage` | **`#D6EAE6`** | **Active Selection States & Hero Cards**: Active calendar date pills, selected segmented buttons, selected day chips, modal duration pills, hero cards (`#052E28` text on `#D6EAE6` fill). |
| `--color-border-selected`| **`#7EB8AE`** | **Soft Selection Border**: Calming, noticeable soft-sage outline for selected/active chips, date pills, segmented buttons, and duration items. Replaces hard `#052E28` borders for gentle visual ergonomics. |
| `--color-text-primary` | **`#000000`** | **Primary Text**: Screen titles, section headers, entity names, large numeric values (`৳`). |
| `--color-text-secondary`| **`#717171`** | **Secondary Text**: Subtitles, metadata, timestamps, queue counts, metric labels. |
| `--color-card-neutral` | **`#F6F8F9`** | **Secondary Cards & Inactive Selectors**: Neutral surfaces (Toggle cards, Financial overview, unselected date/day pills, List tiles). |
| `--color-app-bg` | **`#FFFFFF`** | **App Screen Canvas**: Clean, crisp white background. |
| `--color-badge-bg` | **`#FFFFFF`** | **Pill Badges**: White tags placed inside sage/colored cards. |
| `--color-bell-bg` | **`#F0F6F5`** | **Circular Button BG**: Notification bell and top icon containers. |
| `--color-dashed-border` | **`#CAD8D5`** | **Auxiliary Actions**: Dashed outline pill buttons (`View All...`). |
| `--color-divider` | **`#E2ECEA`** | **Subtle Dividers**: Vertical & horizontal 1px split lines. |
| `--color-nav-inactive` | **`#8E9F9D`** | **Inactive Navigation**: Bottom nav icons and inactive labels. |

---

## 2. Typography System

Fonts are loaded from Google Fonts:
- **Heading & Hero Font**: `Urbanist` (Weights: 600 SemiBold, 700 Bold, 800 ExtraBold)
- **Body, UI & Meta Font**: `DM Sans` (Weights: 400 Regular, 500 Medium, 600 SemiBold)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&family=Urbanist:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
```

### Typographic Application Rules

| UI Role | Font Family | Size | Weight | Color | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Screen Title** | Urbanist | `25px` | 700 (Bold) | `#000000` | Letter-spacing `-0.02em`, line-height `1.15` |
| **Subtitle / Slogan** | DM Sans | `13.5px` | 400 (Regular)| `#717171` | Directly below screen title |
| **Section Header** | Urbanist | `21px` | 700 (Bold) | `#000000` | Left-aligned section start |
| **Section Right Meta** | DM Sans | `13.5px` | 500 (Medium) | `#717171` | E.g. `"12 Patient In Queue"` |
| **Entity / Card Title** | Urbanist | `20px` | 700 (Bold) | `#000000` | Patient name, Doctor name, service title |
| **Entity Subtitle / Meta**| DM Sans | `13px` | 400 (Regular)| `#717171` | Separated by subtle `•` dot |
| **Pill Badge Text** | Urbanist / DM | `12.5px` | 600/700 | `#052E28` | Text inside white badge |
| **Primary Button** | Urbanist / DM | `15px` | 600 (SemiBold)| `#FFFFFF` | Centered with Phosphor icon |
| **Dashed Button** | DM Sans | `14.5px` | 600 (SemiBold)| `#052E28` | Dashed border container |
| **Metric Value (৳ / $)** | Urbanist | `24px` | 700 (Bold) | `#052E28` | Rich deep forest brand accent numbers |
| **Metric Label** | DM Sans | `13px` | 400 (Regular)| `#717171` | Above/below numeric value |
| **Bottom Nav Label** | DM Sans | `11.5px` | 500 (Medium) | Active: `#052E28`, Inactive: `#8E9F9D` |

---

## 3. Iconography Standard: Phosphor Icons (Regular)

All icons across the application use **Phosphor Icons** in the **`Regular`** weight (with `Fill` only for specific active/selected indicators like the docked Home tab).

```html
<link rel="stylesheet" type="text/css" href="https://unpkg.com/@phosphor-icons/web@2.1.1/src/regular/style.css"/>
<link rel="stylesheet" type="text/css" href="https://unpkg.com/@phosphor-icons/web@2.1.1/src/fill/style.css"/>
```

* Top Actions: `<i class="ph ph-bell"></i>`, `<i class="ph ph-gear"></i>`, `<i class="ph ph-sliders-horizontal"></i>`
* Status / Calendar: `<i class="ph ph-calendar-blank"></i>`, `<i class="ph ph-clock"></i>`
* Primary CTAs: `<i class="ph ph-video-camera"></i>`, `<i class="ph ph-phone-call"></i>`, `<i class="ph ph-chat-teardrop"></i>`
* Navigation Arrows: `<i class="ph ph-arrow-right"></i>`, `<i class="ph ph-caret-right"></i>`
* Bottom Navigation: `<i class="ph-fill ph-house"></i>`, `<i class="ph ph-users"></i>`, `<i class="ph ph-chat-centered-text"></i>`, `<i class="ph ph-wallet"></i>`, `<i class="ph ph-user-circle"></i>`

---

## 4. Autonomous Redesign SOP for Future Screens

When the user uploads a legacy screen from the existing app, follow this **5-Step Autonomous Redesign Protocol**:

```
[ Step 1: Feature & Data Audit ]
       ↓
[ Step 2: Visual Weight & Hierarchy Calibration (Hims / Uber Model) ]
       ↓
[ Step 3: Spatial Staging & Cognitive De-Cluttering ]
       ↓
[ Step 4: Eye-Tracking & Visual Flow Architecture ]
       ↓
[ Step 5: Pixel-Perfect HTML/CSS Execution in Mockup ]
```

### Step 1: 100% Feature & Data Audit (Zero Functional Loss)
* **Scan and list every interactive element**: Toggles, buttons, dropdowns, filter tabs, counters, search bars, badges, status indicators, and links.
* **Identify all data points**: Timestamps, prices, patient information, IDs, tags, financial breakdowns.
* **Rule**: *Never drop a functional capability.* Instead, re-architect how it is presented.

### Step 2: Visual Weight & Hierarchy Calibration (Inspired by Hims / Uber / Wise)
* **Section Header**: Left Title (`"Sept 29"` in `Urbanist 21px Bold`) + Right Meta (`"9:00 AM – 11:00 AM"` shift time window in `DM Sans 13.5px #717171`).
* **Primary Anchor (Tier 1 - Immediate Attention)**:
  * The single most important task on the screen.
  * **State 1: Pre-Shift Card (`#D6EAE6`)**:
    * Badges: `Video Session` (with `ph ph-video-camera` icon) + `12 in Queue` in white pill badges (`#FFFFFF`).
    * Title: `"Start Shift 1"` (`Urbanist 20px Bold #000000`) — mentions Shift 1 once in big text. No repeated subtitle.
    * CTA: `<i class="ph-fill ph-play"></i>` + `"Start Shift • Call Serial #1"` (`#052E28` button).
  * **State 2: Active Shift / Next in Queue Card (`#D6EAE6`)**:
    * Badges: `Serial #2` (with `ph ph-user` icon) + `Next in Queue` / `Patient In Call` in white pill badges (`#FFFFFF`). No "Shift 1" label once the shift is running.
    * Title: `"${nextPat.name}"` (`Urbanist 20px Bold #000000`).
    * Subtitle: `"${nextPat.subtitle}"` (e.g. `"31 Years • Female"` in `DM Sans 13px #717171`) — no duplicate shift time window.
    * CTA: `<i class="ph ph-video-camera"></i>` + `"Join Video Call"` (`#052E28` button).
  * **State 3: Doctor Offline Empty-State Card (`#F6F8F9`)**:
    * Clean neutral card with `1.5px solid #EDF2F1` border and `18px` radius.
    * Header Row: Circular/pill icon badge (`ph ph-moon` in `#717171`) + `"Offline (Duration)"` status pill.
    * Title: `"You’re offline"` (`Urbanist 21px Bold #000000`).
    * Description: *"Booked patients have been automatically notified with 1-tap rebooking options."* (`DM Sans 13.5px #717171`).
    * Interaction: No resume button inside the card (since canceled queues don't auto-restore); going back online is handled directly via the top **Accepting Patients** toggle.
* **Secondary Focus (Tier 2 - Operational Context)**:
  * State switches, schedule summaries, filters, and metric summaries.
  * Styled with **Neutral Surfaces (`#F6F8F9`)** with clean `16px` border radii.
* **Tertiary / Navigation (Tier 3 - Exploratory & Auxiliary)**:
  * "View All...", "History", "Download Report".
  * Styled with **Dashed Outlines (`#CAD8D5`)** or subtle **Arrow Rows (`ph ph-arrow-right`)**.

### Step 3: Spatial Staging & Cognitive De-Cluttering
* **Eliminate Visual Noise**:
  * ❌ NO heavy colored gradients, harsh 1px black borders, drop shadows on every tile, or rainbow badge colors.
  * ✅ USE flat pastel fills (`#D6EAE6`), soft neutral surfaces (`#F6F8F9`), and crisp white badges (`#FFFFFF`).
* **Chunking Information**:
  * Group related fields into unified single-level cards rather than deeply nested boxes.
  * For split stats (e.g. Total Income vs. Available Balance), use **2-column or 3-column split cards with a subtle 1px divider (`#E2ECEA` / `#D0E5E0`)** instead of multiple separate clunky cards.
* **Modern Healthtech Glassmorphism Standard**:
  * **Hero & Primary Metric Cards** (`.patient-hero-card`, `.patient-metrics-card`, `.calendar-action-btn`):
    * `background: linear-gradient(135deg, rgba(239, 247, 245, 0.95) 0%, rgba(214, 234, 230, 0.8) 100%);`
    * `backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);`
    * `border: 1.5px solid rgba(126, 184, 174, 0.4);`
    * `box-shadow: 0 4px 20px -2px rgba(5, 46, 40, 0.06), inset 0 1px 1px rgba(255, 255, 255, 0.95);`
  * **Neutral Frosted Cards** (`.financial-card`, `.accepting-patients-card`, `.profile-hero-card`, `.profile-vitals-card`, `.patient-hero-card.locked-card`):
    * `background: linear-gradient(135deg, rgba(246, 248, 249, 0.95) 0%, rgba(238, 244, 243, 0.8) 100%);`
    * `backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);`
    * `border: 1.5px solid rgba(226, 236, 234, 0.85);`
    * `box-shadow: 0 4px 18px -2px rgba(0, 0, 0, 0.03), inset 0 1px 1px rgba(255, 255, 255, 0.9);`
* **Master Spacing System (Strict Semantic Wrapper Rule Everywhere)**:
  * **Section-to-Section Distance**: Exactly **`24px`** (`--spacing-section: 24px`) between distinct `<section>` blocks (e.g. Quick Status to Queue Section, Queue Section to Financial Overview, Metrics Card to All Patients Section, Patient Info Section to Visits Log Section).
  * **Inside-a-Section Distance (Title to Content)**: Exactly **`10px`** (`--spacing-element: 10px`) inside any `<section>` block (`.desk-section`, `.patients-section`, `.profile-section`, `.schedule-section`).
  * **Inner Card Padding**: `14px` to `20px`
  * **Micro Gap (Icon to Text)**: `6px` to `8px`
  * **Element Shrinkage Prevention**: All primary action buttons, hero cards, shift cards, and metric tiles MUST specify `flex-shrink: 0; min-height: 48px;` to guarantee zero height distortion or shrinking when content overflows.
  * **Tap Target Minimum**: `44px` height (Buttons `48px` to `52px`)

### Step 4: Eye-Tracking & Visual Flow Architecture
1. **Top Anchor**: Immediate orientation with `Screen Title` (`Urbanist 25px Bold`) + `Subtitle` (`DM Sans 13.5px #717171`) + top right utility icon.
2. **Immediate Action Row**: High-priority status switch or primary quick-tiles (e.g., Accepting Patients + Calendar tile).
3. **Hero Content Block**: The active queue item or primary entity in `#D6EAE6` pastel sage.
4. **Secondary Information**: 2-column metric cards or clean table-less list rows.
5. **Docked Navigation**: Fixed bottom 5-tab bar with clean active indicators.

### Step 5: Pixel-Perfect HTML/CSS Delivery
* Encapsulate inside the standard **Phone Mockup Frame** (`phone-screen` 844px height, status bar, home indicator).
* Use semantic HTML5, embedded Phosphor Icons (Regular), Google Fonts, and lightweight vanilla JS for realistic tap and toggle states.

---

## 5. Hims-Inspired Editorial Minimalism Standard (Bottom Sheets & Modals)

Rather than rendering standard administrative dialogs with dense text, modals and bottom drawers adopt **Hims/Western editorial minimalism**:

### 5.1 Editorial Typography & Copy Reduction
* **Giant Editorial Headline**: `Urbanist 32px Bold / ExtraBold` (`#000000`), letter-spacing `-0.03em`. Use punchy, human phrasing (e.g., *"Take a break"* instead of verbose clinical titles).
* **Radical Text Reduction**: Maximum **1 concise sentence** of supporting copy (`DM Sans 14px #717171`). Eliminate redundant explanations.
* **Top Accent Badge**: Clean `38px × 38px` rounded square pastel badge (`#D6EAE6`) with a Phosphor icon (e.g. `ph ph-moon`) + minimal top-right circular dismiss button (`ph ph-x`).

### 5.2 Clutter-Free Pill Selectors
* Replace bulky nested cards with **Sleek Duration Pill Chips** (`border-radius: 18px`):
  * **Option Label**: Kept concise and on a **single line** (e.g. `1 Week` instead of `1 Week (Full Leave)`).
  * **Unselected**: Flat neutral surface (`#F6F8F9`), `Urbanist 17px Bold` title + subtle capsule count badge (`#717171` over `rgba(255,255,255,0.75)`).
  * **Selected**: Pastel Sage fill (`#D6EAE6`) with `#052E28` border and `#052E28` bold count badge.

### 5.3 Standardized Modal Action Buttons (Cancel + Action CTA)
* All modal and bottom sheet popups maintain a consistent **Dual Pill Action Row**:
  * **Cancel Button**: Background `#F6F8F9`, text `#052E28`, `Urbanist 15.5px Bold`, height `52px`, `border-radius: 100px`.
  * **Primary Action CTA**: Background `#052E28`, text `#FFFFFF`, `Urbanist 15.5px Bold`, height `52px`, `border-radius: 100px`, subtle elevation `box-shadow: 0 8px 24px rgba(5,46,40,0.25)`.
* **Dismiss Pattern**: No redundant top `X` close icon; dismissal is handled cleanly via the **Cancel** button or tapping the blurred backdrop.

---

## 6. Shift & Schedule Management System (Edit Shift Flow)

The schedule configuration screens transform clinical timetable settings into a **sleek, European calendar and shift management workflow**:

### 6.1 Universal Sticky Top Navigation & 1-Week Date Strip
* **Universal Sticky Navigation**: All top navigation panels (back button, screen title, actions) MUST remain **permanently pinned/sticky at the top** (`position: sticky; top: -12px; z-index: 20; background: var(--color-app-bg);`) so the user can always navigate back instantly regardless of scroll position.
* **Back Button**: Circular icon container (`44px × 44px`, background `#F0F6F5`, icon `ph ph-arrow-left` in `#052E28`).
* **Screen Title**: `Urbanist 24px Bold` (`#000000`).
* **Horizontal 1-Week Date Strip (Starting Today)**:
  * Inactive Day: `#F6F8F9` background, `border: 1.5px solid #EDF2F1`, sleek `10px` radius (not overly circular/bubbly), `DM Sans 11px` day name (`#717171`), `Urbanist 17px Bold` date number (`#000000`).
  * Active/Selected Day: Pastel Sage `#D6EAE6` fill with `border: 1.5px solid #052E28`, `DM Sans 11px Bold #052E28` day name, `Urbanist 17px Bold #052E28` date number. (Keeps calendar cards airy and distinct from dark CTA buttons).

### 6.2 Top-Anchored Prominent Action CTA (`+ Add Shift`)
* **Placement**: The `+ Add Shift` CTA button MUST be positioned **on top** directly between the selected date header and the shifts list, eliminating any need for the user to scroll through existing shift cards to create a new shift.
* **Styling**: High-visibility primary button (`background: #052E28; color: #FFFFFF; height: 48px; border-radius: 12px; font-weight: 700; box-shadow: 0 4px 14px rgba(5, 46, 40, 0.18)`).
* **Modal Trigger**: Tapping `+ Add Shift` or `Edit Shift` smoothly launches the **Shift Hours Editor Bottom Sheet Modal (`#shiftModalSheet`)** over the blurred backdrop, keeping the main page 100% clean and free of inline form clutter.

### 6.3 Configured Shift Cards (Saved State)
* **Container**: Clean neutral surface `#F6F8F9` with `1.5px solid #EDF2F1`, `18px` border radius, padding `16px`.
* **Top Badges**:
  * Left Pill: White badge with video/user icon: `Video Consultation` (`ph ph-video-camera`).
  * Right Pill: Pastel Sage pill `Shift 1` (`#D6EAE6` background with `#052E28` bold text).
* **Time & Capacity**: `Urbanist 21px Bold` (`#000000`) for `10:00 AM – 12:00 PM` + `DM Sans 13px` for `Capacity: Max 15 Patients`.
* **Card Actions Row**:
  * `Edit Shift`: Pill button (`#FFFFFF` background, border `1px solid #DCE5E3`, text `#052E28`, `Urbanist 14px Bold`).
  * `Delete`: Minimal square button (`#FFFFFF`, border `1px solid #FEE4E2`, icon `ph ph-trash` in `#D92D20`).

### 6.4 Shift Hours Editor Bottom Sheet Modal (`#shiftModalSheet`)
* **Editorial Modal Structure (Universal Big Text Standard)**:
  * Top Badge: Clean rounded square pastel badge (`#D6EAE6`) with `<i class="ph ph-clock"></i>` in `#052E28`.
  * Headline: `Urbanist 30px Bold #000000` (`Add Shift Hours` / `Edit Shift 1`).
  * Subtitle: `DM Sans 13.5px #717171` (`Configure consultation hours and maximum patient limit.`).
  * Consultation Segment: Dual segmented pills (`Video` vs `In Person`), active button in `#D6EAE6` (Card Sage) with soft `#7EB8AE` border and `#052E28` bold text.
  * Start & End Time Tiles: Side-by-side `#FFFFFF` tiles (`14px` radius) with `11.5px` label and `Urbanist 17px Bold` time text.
  * Repeat Day Selector: 7 modern rounded square day chips (`8px` radius, `S`, `M`, `T`, `W`, `T`, `F`, `S`). Selected days in `#D6EAE6` (Card Sage) with soft `#7EB8AE` border and `#052E28` bold text.
  * Patient Limit Stepper: Integrated `[-] 15 [+]` counter in `#FFFFFF` container.
  * Repeat Weekly Switch: Row with `Urbanist 15px Bold` title + toggle switch.
  * Dual Action Row: `Cancel` (`#F6F8F9` background, `#052E28` text, height `52px`, `border-radius: 100px`) + `Save Shift` (`#052E28`, `#FFFFFF` text, height `52px`, `border-radius: 100px`, `box-shadow: 0 6px 20px rgba(5,46,40,0.22)`).

---

## 7. Telehealth Video Consultation System (In-Call Experience)

When the doctor initiates or joins a video consultation session (`Join Video Call`), the interface transitions into a **focused, distraction-free clinical telehealth workspace**:

### 7.1 Immersive In-Call Canvas & Top Patient Header
* **Immersive Theme**: Dark slate / deep forest backdrop (`#04120F` to `#091A16`) with white status bar elements and docked bottom nav auto-hidden.
* **Patient Identity Cluster**:
  * **Serial Number Badge**: `#D6EAE6` (Card Sage) rounded square with `#052E28` bold text (e.g. `#2`).
  * **Patient Info**: Name (`Urbanist 17px Bold #FFFFFF`) + animated pulsing status indicator (`#10B981` dot + `Connected` in `#7CE7BD`).
* **End Call CTA**: Soft crimson pill button (`#EA3B50`, `height: 38px`, `border-radius: 100px`, icon `ph ph-phone-x`, `Urbanist 13.5px Bold #FFFFFF`).

### 7.2 Central Video Feed Viewport & Doctor PiP Window
* **Patient Main Stream**:
  * Large rounded viewport (`border-radius: 24px`, border `1.5px solid rgba(214,234,230,0.12)`).
  * High-res patient portrait with pulsing audio waves (`patient-avatar-ring`), `Urbanist 19px Bold` patient name, and `DM Sans 12.5px` feed status.
* **Doctor Picture-in-Picture (PiP) Window**:
  * Floating top-right tile (`100px × 136px`, `border-radius: 16px`, background `#112823`, border `1.5px solid rgba(214,234,230,0.25)`).
  * Contains doctor avatar / camera preview, `Doctor Feed` label, and 1-tap flip camera button (`ph ph-camera-rotate`).
* **Floating Live Call Duration Pill**:
  * Glassmorphism centered pill (`background: rgba(5,46,40,0.75); backdrop-filter: blur(12px); border-radius: 100px; padding: 6px 16px;`).
  * Displays active blinking red indicator dot + live ticking timer (`12:32 Min`).

### 7.3 Standard In-Call Action Toolbar (Strict 10px Spacing)
* **Mic & Camera Toggles**: Circular buttons (`48px × 48px`, background `rgba(255,255,255,0.1)`, icons `ph ph-microphone` / `ph ph-video-camera`). Toggle state turns crimson red with slash icon when muted/disabled.
* **Skip Patient Button**: Pill button (`height: 48px`, `flex: 0.95`, background `rgba(234, 179, 8, 0.12)`, border `1px solid rgba(234, 179, 8, 0.35)`, text `#FACC15`, icon `ph ph-fast-forward`, `padding: 0 10px`).
* **Back to Desk Button**: Pill button (`height: 48px`, `flex: 1.45`, background `rgba(255, 255, 255, 0.1)`, border `1px solid rgba(255, 255, 255, 0.18)`, text `#FFFFFF`, icon `ph ph-house`, `padding: 0 14px`). Allows doctor to background the call and step out to the lobby while waiting for the patient.
  * **Desk Hero Card State upon Return**: Updates to `In Call (Lobby)` badge and dynamically changes the CTA button to `Re-join Call`. Clicking `Re-join Call` seamlessly returns the doctor to the ongoing video call screen without resetting the timer.

### 7.4 End Call Confirmation Bottom Sheet Modal (`#endCallModalSheet`)
* **Editorial Structure (Hims Style)**:
  * Top Badge: Soft danger badge (`#FEE4E2` rounded square with `#D92D20` `ph ph-phone-disconnect` icon).
  * Headline: `End Consultation?` (`Urbanist 28px Bold #000000`).
  * Subtitle: `This will end your call with Farzana Khan and start AI Consultation wrap-up.` (`DM Sans 13.5px #717171`).
  * Call Summary Tile: Neutral card (`#F6F8F9`, `16px` radius) with `Current Call Duration` label + bold duration value (`12:32 Min`).
  * Dual Action Row:
    * `Stay In Call`: Neutral pill button (`#F6F8F9` background, `#052E28` text, height `52px`, `border-radius: 100px`).
    * `End Call`: Crimson CTA (`#EA3B50`, `#FFFFFF` text, height `52px`, `border-radius: 100px`, `box-shadow: 0 6px 20px rgba(234,59,80,0.3)`).

### 7.5 Skip Patient Confirmation Bottom Sheet Modal (`#skipPatientModalSheet`)
* **Editorial Structure (Big Text Standard with Contextual Clarity)**:
  * Top Badge: Warning badge (`#FFF5EB` rounded square with `#D97706` `<i class="ph ph-fast-forward"></i>` icon).
  * Headline: Dynamic patient title (`Skip Farzana Khan?` in `Urbanist 28px–32px Bold #000000`).
  * Context Subtitle: Clear trigger condition (`Skip patient if they are absent from or not joining the call.` in `DM Sans 14px #717171`).
  * Auto-Slot Informational Callout Box: `#FFFBEB` background with `#FDE68A` border, `12px` radius, `<i class="ph-fill ph-clock-counter-clockwise"></i>`, and text: `When they are back, they will be auto-slotted 3 turns ahead upon return` (`DM Sans 12.5px #92400E`).
  * Dual Action Row:
    * `Cancel`: Neutral pill button (`#F6F8F9` background, `#052E28` text, height `52px`, `border-radius: 100px`).
    * `Skip Patient`: Warning CTA (`#D97706`, `#FFFFFF` text, height `52px`, `border-radius: 100px`, `box-shadow: 0 6px 20px rgba(217, 119, 6, 0.28)`).
  * Behavior on Confirm: Closes modal, stops call timer, advances queue to the next patient, updates the Desk Hero Card with clean patient context, and smoothly returns doctor to My Desk.

---

## 8. AI Consultation Wrap-Up & Live Processing System

Following call completion, the doctor is transitioned to the **AI Real-Time Processing Screen (`#pageAiWrapUp`)**:

### 8.1 Top Navigation & Live Status Tag
* **Live AI Tag**: Pastel Sage pill badge (`#D6EAE6` with green pulsing dot and `AI Real Time Processing` in `#052E28`).
* **Dismiss / Minimize**: Top-right circular close button (`44px × 44px`, `#F0F6F5` background with `ph ph-x`) that allows returning to desk at any time.

### 8.2 Generative AI Breathing Loader & Typography
* **Generative Spinner**: Sleek rotating circular SVG ring in Sage (`#D6EAE6`) and Dark Forest (`#052E28`) with smooth infinite rotation.
* **Editorial Title**: `Generating Consultation Wrap Up` (`Urbanist 24px Bold #000000`, center-aligned).
* **Subtitle**: `Compiling clinical notes for Serial #2 (Farzana Khan)` (`DM Sans 13.5px #717171`).

### 8.3 Real-Time Step Progress Card
* **Card Container**: `#F6F8F9` neutral surface with `18px` border radius, `1.5px solid #EDF2F1`, and `14px` internal row spacing.
* **Step Row States**:
  * **Completed**: `<i class="ph-fill ph-check-circle"></i>` in emerald `#10B981` + `#052E28` bold text (e.g. *Audio & transcript analyzed*, *Chief complaints & symptoms extracted*).
  * **In Progress**: `<i class="ph ph-spinner ph-spin"></i>` animated spinner in `#0D9488` + `#052E28` bold text (e.g. *Drafting prescription medicines*), dynamically auto-completing to checkmark ✅.

### 8.4 Return to Desk CTA
* **Action Button**: Full-width primary capsule button (`height: 52px; background: #052E28; color: #FFFFFF; border-radius: 100px; font-family: Urbanist; font-weight: 700; font-size: 15.5px; icon ph ph-house; box-shadow: 0 6px 20px rgba(5,46,40,0.2);`).
* **Result**: Returns doctor to My Desk, advancing queue to ready next patient (`#3 Tanvir Ahmed`).

---

## 9. Consultation Wrap-Up Review & Rx Finalization System

Following AI processing, the screen automatically transitions into the **Consultation Wrap-Up Review Screen (`#pageConsultationReview`)**:

### 9.1 Calming, Soft Clinical Hierarchy (Zero Harsh Colors)
* **Soft Surfaces**: Avoid loud, saturated green or neon fills. Use **Card Neutral (`#F6F8F9`)** surfaces with `1.5px solid #EDF2F1` borders and crisp white icon bubble containers (`#FFFFFF` with `#E2ECEA` border).
* **AI Generated Badge**: Pastel Sage pill tag (`#D6EAE6` with `#052E28` text and `<i class="ph ph-sparkle"></i>`).
* **Section-to-Section Spacing**: Strict `24px` gap between distinct review blocks.
* **Element-to-Element Spacing**: Strict `10px` gap inside lists and action containers.

### 9.2 Clinical Information Architecture
1. **Chief Complaint (AI Summarized)**:
   * Clean `#F6F8F9` editable card with `DM Sans 13.5px` body (`#334155`) summarizing symptoms from patient audio.
   * **Selection & Focus State**: When tapped/focused, displays our brand `#052E28` border with subtle `0 0 0 3px rgba(5, 46, 40, 0.08)` focus ring (`outline: none;` prevents browser default magenta/blue borders).
2. **Draft Prescription (Auto-filled from voice recommendations)**:
   * Individual medicine tiles (`Napa Extra 500mg`, `Vergon 5`) displaying `Urbanist 15px Bold` title, dosage (`1-0-1 • After Meal • 5 Days`), and Edit/Delete icon controls.
   * `+ Add Medicine`: Dashed border button (`border: 1.5px dashed var(--color-dashed-border); background: #FFFFFF;`).
3. **Lab Tests / Investigations**:
   * Auto-extracted tests (`CBC (Complete Blood Count)`) with flask icon (`ph ph-flask`) + `+ Add Tests` dashed button.
4. **Refer a Doctor (Clean Empty State)**:
   * Neutral container displaying `"No Referral Added"` (`DM Sans 13.5px #717171`) + `+ Add Referral` dashed button.
5. **Schedule Follow-Up (Standard Selection System)**:
   * 4 horizontal duration chips (`None`, `7 Days`, `15 Days`, `1 Month`) + custom calendar date picker.
   * Selected state strictly uses **Card Sage (`#D6EAE6`)** fill with **`#052E28`** border and bold text.

### 9.3 Floating Actions Dock (Preview RX + Mark As Done)
* **Sticky Dock System**: Sticky at bottom of the scroll container (`position: sticky; bottom: -30px; margin: 16px -20px -30px -20px; background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(12px); border-top: 1.5px solid #EDF4F2; z-index: 25;`).
  * **Preview RX**: Neutral capsule button (`#F6F8F9` background, `#052E28` text, `Urbanist 14.5px Bold`, height `48px`, `border-radius: 100px`).
  * **Mark As Done**: Primary Dark CTA (`#052E28`, `#FFFFFF` text, `Urbanist 15px Bold`, height `48px`, `border-radius: 100px`, icon `ph-fill ph-check-circle`).
* **Finalization Flow**: Tapping `Mark As Done` safely finalizes the consultation, returns the doctor to **My Desk**, and advances the active queue to **`Serial #3 • Tanvir Ahmed`**.

### 9.4 Medicine & Lab Test Bottom Sheet Editor Standard (`#addMedicineModalSheet`, `#addLabModalSheet`)
* **Universal Big Text Editorial Architecture (Zero Subtext Clutter)**:
  * **Top Badge**: Clean `40px × 40px` rounded square pastel badge (`#D6EAE6`) with Phosphor icon (`<i class="ph ph-pill"></i>` or `<i class="ph ph-flask"></i>` in `#052E28`).
  * **Giant Editorial Headline**: `Urbanist 30px Bold #000000` (`Add Medicine`, `Edit Medicine`, `Add Investigation`). No redundant subtext.
  * **Clutter-Free Form Inputs**:
    1. **Medicine / Test Name**: Clean input card in neutral surface `#F6F8F9` with `1.5px solid #EDF2F1`, `14px` border radius, and natural title case label (`Medicine Name`).
    2. **Frequency Toggle Chips**: `Daily Frequency` label with 3 horizontal chips (`Morning`, `Noon`, `Night` with icons). Selected chips in **Card Sage (`#D6EAE6`)** with **`#052E28`** border/text.
    3. **Meal Timing Segment**: `Meal Timing` label with `After Meal` vs `Before Meal` toggle chips.
    4. **Dose & Duration**: 2-column side-by-side inputs (`Dose` e.g. `1 Tablet` + `Duration` e.g. `5 Days`).
    5. **Instructions / Notes**: Optional minimal notes input (`Instructions (Optional)`).
  * **Standard Dual Action Buttons**:
    * `Cancel`: Background `#F6F8F9`, text `#052E28`, `Urbanist 15.5px Bold`, height `52px`, `border-radius: 100px`.
    * `Confirm / Add`: Background `#052E28`, text `#FFFFFF`, `Urbanist 15.5px Bold`, height `52px`, `border-radius: 100px`, `box-shadow: 0 6px 20px rgba(5,46,40,0.22)`.
* **Color Rule Adherence**:
  * Action Buttons = Primary Dark `#052E28`.
  * Selection Chips / Toggles = Card Sage `#D6EAE6` with `#052E28` border/text.
  * Neutral Surfaces = `#F6F8F9` with `#EDF2F1` borders.

---

## 10. Page 6: Real-Time Generated Digital Prescription Standard (`#pagePrescriptionPreview`)

The Prescription Preview screen provides an ultra-clean, legible, digital clinical letterhead that is formatted in real time from the consultation wrap-up review screen.

```
[ Top Bar: Back Button + "Prescription Preview" Title + Share Action ]
                               ↓
[ Digital Paper Canvas (.rx-paper-container) ]
  ├── 1. Doctor Profile & Onubot Telehealth Branding Header
  ├── 2. Patient Demographics Strip (Name, Age/Sex, Date, Consult ID)
  ├── 3. Two-Column Clinical Body
  │      ├── Left Column (36%): C/C (Chief Complaints), O/E (Vitals), Tests, Referral
  │      ├── 1px Vertical Divider (#E8EEED)
  │      └── Right Column (64%): ℞ Glyph, Numbered Medications Stack, General Advice, Follow-Up
  └── 4. Electronic Signature & Verification Stamp Footer
```

### 10.1 Doctor Profile & Onubot Telehealth Branding Header
* **Doctor Profile Block**:
  * **Doctor Name**: `Dr. Tanvir Ahmed` in `Urbanist 16.5px ExtraBold #052E28`.
  * **Degrees**: `MBBS (DMC), FCPS (Medicine), MD` in `DM Sans 11px SemiBold #2D3748`.
  * **Institution**: `Senior Consultant • Dhaka Medical College Hospital` in `DM Sans 10.5px Regular #717171`.
  * **BMDC Registration**: `BMDC Reg. No: A-74829` in `DM Sans 10px SemiBold #052E28`.
* **Onubot Telehealth Branding**:
  * **Verification Badge**: Capsule in Card Sage (`#D6EAE6`) with `#052E28` text and `<i class="ph-fill ph-seal-check"></i>`.
  * **Sub-label**: `Digital Rx System` (`DM Sans 9.5px #717171`).

### 10.2 Patient Demographics Strip
* **Neutral Surface**: `#F7FAF9` background with `1px solid #EBF1F0` and `10px` border radius.
* **3-Column Compact Grid**:
  * `Patient Name`: Dynamically extracted from active queue patient (e.g. `Alif Khan`).
  * `Age / Sex`: `28 Yrs / Male`.
  * `Date`: Current formatted date (`29 Sep 2026`).

### 10.3 Two-Column Clinical Body Layout
* **Left Column (Clinical Findings)**:
  * **C/C (Chief Complaints)**: Clean bulleted list parsed in real time from the editable Chief Complaint area.
  * **O/E (Vitals)**: Structured vitals grid (`BP: 120/80 mmHg`, `Pulse: 76 bpm`, `Temp: 98.6°F`, `Weight: 68 kg`).
  * **Tests / Investigations**: Dynamically synced from the lab investigations list.
  * **Referral**: Dynamically displays referred specialist name and department if selected in the wrap-up screen; automatically hidden if no referral was added.
* **Right Column (℞ Medications & Advice)**:
  * **℞ Glyph**: Classic serif medical glyph in `#052E28` (`Georgia`, `24px Bold Italic`).
  * **Numbered Medications**: Real-time stack of all prescribed medicines with timing badge (`1-0-1 • After Meal • 5 Days`) and specific instructions.
  * **General Advice**: Bullet points for lifestyle/hydration guidance.
  * **Follow-Up Box**: Dynamically displays selected follow-up duration (`Within 7 Days`, `15 Days`, `1 Month`, or `None`).

### 10.4 Digital Signature & Verification Footer
* **QR Verification Seal**: Digital square stamp (`24px × 24px`) with `<i class="ph ph-qr-code"></i>`, `Digitally Certified`, and real-time generation timestamp.
* **Doctor Sign-Off**: Calligraphy cursive signature (`Tanvir Ahmed`), clean 1px baseline rule, doctor name in `Urbanist 8.5px Bold`, and `Signed via Onubot Telehealth`.

### 10.5 Single-Page Bangladesh A4 Dimension Ratio (1 : 1.414)
* **Single-Page Requirement**: All prescription elements fit strictly on a single A4 page.
* **Space Optimization**: Reduced wordiness and tight typography ensure up to 6–8 medications fit with comfortable breathing room.

---

## 11. Universal Delete Confirmation Modal Standard (`#deleteConfirmModalSheet`)

* **Trigger**: Tapping the trash/delete icon on any medicine, lab test, or referral doctor on the Consultation Wrap Up screen.
* **Architecture**:
  * **Top Badge**: `40px × 40px` rounded square in light red `#FEECEC` with `#D32F2F` icon (`<i class="ph ph-trash"></i>`).
  * **Editorial Big Title**: `Urbanist 30px Bold #000000` (e.g. `Delete Medicine?`, `Delete Lab Test?`, `Remove Referral?`). Zero subtext paragraphs.
  * **Dual Action Row**:
    * `Cancel`: Neutral button (`#F6F8F9` background, `#052E28` text, height `52px`, `border-radius: 100px`).
    * `Delete`: Destructive button (`#EA3B50` background, `#FFFFFF` text, height `52px`, `border-radius: 100px`, `box-shadow: 0 6px 20px rgba(234, 59, 80, 0.22)`).
* **Execution**: Executing confirmation removes the target item with smooth scale/fade animation and auto-updates the real-time Prescription Preview.

---

## 12. Skip Patient Confirmation Modal Standard (`#skipPatientModalSheet`)

* **Trigger**: Tapping the **Skip** action button inside the active Video Consultation Call screen.
* **Minimalist Architecture (Zero Subtext Clutter)**:
  * **Top Badge**: `40px × 40px` rounded square in warm amber/orange tint (`#FFF5EB`) with `#D97706` icon (`<i class="ph ph-fast-forward"></i>`).
  * **Editorial Big Title**: `Urbanist 30px Bold #000000` (`Skip [Patient Name]?`). Zero redundant subtitle paragraphs.
  * **Single Compact Auto-Slot Note Pill**:
    * Sleek pill (`#FFFBEB` background, `1px solid #FDE68A`, `12px` border-radius, `padding: 10px 14px`).
    * Icon & Copy: `<i class="ph-fill ph-clock-counter-clockwise"></i> Auto-slotted 3 turns ahead upon return` (`DM Sans 12.5px Medium #92400E`).
  * **Dual Action Row**:
    * `Cancel`: Neutral button (`#F6F8F9` background, `#052E28` text, height `52px`, `border-radius: 100px`, `onclick="closeSkipPatientModal()"`).
    * `Skip Patient`: Accent Amber CTA (`#D97706` background, `#FFFFFF` text, `Urbanist 15.5px Bold`, height `52px`, `border-radius: 100px`, icon `ph ph-fast-forward`, `box-shadow: 0 6px 20px rgba(217, 119, 6, 0.28)`, `onclick="confirmSkipPatientAction()"`).
* **Execution & Redirection Flow**:
  1. Stops the live call timer.
  2. Advances the queue index to the next patient.
  3. Updates the **My Desk** Hero Card with the new patient's name, serial, and `"Join Video Call • Serial #[N]"` CTA.
  4. Smoothly navigates the doctor directly back to the **My Desk** screen.

---

## 13. All Appointments & Non-Disruptive Background AI Pipeline (`#pageAppointments`)

### 13.1 Background AI Wrap-Up Generation & Flow Control
* **Zero Disruption Policy**: When a consultation call ends and enters the AI processing screen (`#pageAiWrapUp`), the doctor can tap **Return to Desk** (or the top-right `X` button) at any time.
* **Non-Blocking Execution**:
  * The AI processing continues silently in the background.
  * The automatic page popover timer is safely canceled so the doctor's flow on **My Desk** is never interrupted.
  * The appointment status in the background transitions to **`Draft Rx`** with `<i class="ph ph-pencil-simple"></i> Draft Rx` tag.
  * The Desk Hero Card immediately advances to the next patient in the queue so the doctor can proceed without delay.

### 13.2 All Appointments Screen Architecture
* **Access Point**: Direct 1-tap navigation via **`View All Appointments`** button on My Desk.
* **Segmented Mode Tabs**: `Upcoming` vs `History` pills with smooth toggle transitions.
* **Horizontal Date Filter Bar**: Scrollable pills (`All`, `Today (12)`, `Sept 28`, `Sept 29`, `Sept 30`, `Oct 01`) styled with soft selection token `--color-border-selected: #7EB8AE`.
* **Appointment Status Badge Hierarchy**:
  * **`Prescribed`**: `#E8F7F0` background, `#0D7A48` bold text, `#B8EBD1` border + checkmark icon. Tapping opens the single-page A4 Prescription Preview.
  * **`Draft Rx`**: `#FFFBEB` background, `#92400E` bold text, `#FDE68A` border + pencil icon. Tapping opens the Consultation Wrap-Up Review screen where the doctor can edit medicines, tests, and click **Mark As Done**.
  * **`Skipped`**: `#FEF2F2` background, `#991B1B` bold text, `#FECACA` border. Represents absent/unreachable patients.
  * **`In Call Now`**: `#D6EAE6` pastel sage with animated pulsing live indicator dot. Tapping returns directly to the active video call.
  * **`Re-queued`**: `#FAF5FF` background, `#6B21A8` bold text, `#E9D5FF` border. Identifies returning skipped patients auto-slotted 3 turns ahead.
  * **`In Queue`**: Neutral surface `#F6F8F9` with `#717171` text for upcoming scheduled patients.

---

## 14. Multi-Shift Schedule & Appointment Details Architecture (`#pageAppointmentDetails`)

### 14.1 Multi-Shift Section Grouping & Strict Spacing System
* **Multiple Shifts per Day**: One calendar day supports multiple distinct shifts (e.g. `Shift 1 • 9:00 AM – 11:00 AM`, `Shift 2 • 6:00 PM – 11:00 PM`).
* **Strict Spacing Architecture**:
  * **Shift-to-Shift Distance**: Exactly **`24px`** (`--spacing-section: 24px`) between Shift 1 container and Shift 2 container (`.appointments-list { gap: 24px; }`).
  * **Card-to-Card Distance (Inside a Shift)**: Exactly **`10px`** (`--spacing-element: 10px`) between individual appointment cards (`.appts-shift-cards-group { gap: 10px; }`).
* **Shift State Transitions**:
  * **Before Shift Started (`!isShiftActive`)**: All patient cards in Shift 1 display as `In Queue` / `Upcoming` with sequential booking serials (`#1`, `#2`, etc.).
  * **Active Ongoing Shift (`isShiftActive`)**: Reflects live real-time status across patient cards (`Prescribed`, `Draft Rx`, `Skipped`, `In Call`, `In Queue`).
  * **Upcoming Shifts (e.g. Shift 2)**: All bookings remain cleanly indexed in queue order.

### 14.2 Wise / Uber Minimalist Appointment Details Dossier (`#pageAppointmentDetails`)
Adopting **Wise / Uber** clean minimalist UI standards to avoid nested "box-inside-a-box" card syndrome:
* **Clean Flat Cards**: Single-level `#F6F8F9` background cards with soft `1.5px solid #EDF2F1` borders and `16px` border-radius.
* **Single-Line Section Headers**: Left title (e.g. `Pre-visit Details`) + right single-line capsule tag (e.g. `<span class="ai-sparkle-tag">✨ AI Summary</span>`). No multi-line redundant headers.
* **Direct Speech Quote**: Clean white surface with a refined `3px solid #0D9488` teal vertical accent bar.
* **Soft Selection States**: Uses `--color-border-selected: #7EB8AE` for gentle visual ergonomics.

### 14.3 Dynamic Relevance Content Ordering
Sections are dynamically rendered based on the patient's lifecycle state:

1. **For `Prescribed` (Done & Finalized Patients)**:
   * **1. Issued Prescription (`#D6EAE6` Sage Banner Tile)**: Direct 1-tap `View Rx` action opening the A4 Digital Prescription.
   * **2. Live Consultation Notes (`✨ Live Call AI`)**: Extracted clinical findings, medicines prescribed, and lifestyle advice.
   * **3. Pre-visit Details (`✨ AI Summary`)**: Reported symptoms, duration, severity tags, and patient quote.
   * **4. Patient Documents**: Past medical records and previous prescriptions uploaded during intake.

2. **For `Draft Rx` (Call Ended, Awaiting Review)**:
   * **1. Live Consultation Notes (`✨ Live Call AI`)**
   * **2. Pre-visit Details (`✨ AI Summary`)**
   * **3. Patient Documents**

3. **For `In Queue` / `Upcoming` / `Skipped` / `In Call`**:
   * **1. Pre-visit Details (`✨ AI Summary`)**
   * **2. Patient Documents**

### 14.4 Contextual Action Dock
* **Prescribed**: `View Issued Prescription` (preview signed prescription)
* **Draft Rx**: `Review & Finalize Rx` (opens consultation review wrap-up)
* **In Call**: `Re-join Active Call` (re-enters video consultation)
* **In Queue / Skipped**: **No CTA button rendered** (`display: none;`). Doctors follow sequential queue execution from the main Desk; skipped patients are requeued automatically when they mark presence in their patient app.

---

## 15. Sticky Frosted Bottom Action Dock & Real-Time Queue Synchronization Standard

### 15.1 Sticky Frosted Bottom Action Dock (`.details-bottom-dock`)
* **No Floating Overlap**: Primary bottom action buttons (e.g. `Review & Finalize Rx`, `View Issued Prescription`) must **never float transparently** over list content or document files.
* **Sticky Positioning & Frosted Backdrop**:
  * Fixed to the bottom edge: `position: sticky; bottom: -30px; margin: 16px -20px -30px -20px;`
  * Solid frosted background: `background: rgba(255, 255, 255, 0.96); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);`
  * Top divider border: `border-top: 1.5px solid #edf4f2;`
  * Subtle elevation: `box-shadow: 0 -4px 20px rgba(0, 0, 0, 0.05); z-index: 25;`
* **Primary Button Geometry (`.btn-dock-primary`)**:
  * Height: `48px` full-width pill button (`border-radius: 100px; width: 100%;`).
  * Typography: `Urbanist 15px Bold #FFFFFF`.
  * Background: `#052E28` with subtle drop shadow `box-shadow: 0 4px 16px rgba(5, 46, 40, 0.22);`.

### 15.2 Real-Time 1-to-1 Patient Queue Synchronization
* **Sequential Indexing**: Starting Shift 1 begins strictly with **Serial #1 (`Tariqul Islam`)**.
* **Zero Discrepancy Flow**:
  1. Starting shift transitions Desk Hero Card to Serial #1 (`Tariqul Islam`).
  2. Joining video call syncs feeds, name tags, skip modals, and end-call subtitles to Serial #1.
  3. Ending call / skipping Serial #1 updates `appointmentsData` status (`prescribed`, `draft_rx`, or `skipped`) and automatically advances the queue to Serial #2 (`Farzana Khan`), then Serial #3 (`Nusrat Jahan`), etc.
  4. The **All Appointments** screen reflects exact real-time patient statuses without mock mismatches.
* **Focused Shift 1 View**: Displays Shift 1 (6 bookings) without overcrowding secondary shifts.

---

## 16. Minimal Patient Subtext & Strict "Type" vs "Status" Separation

### 16.1 Minimal Patient Subtext Standard (Age & Gender Only)
* **Principle**: Never overwhelm or dump redundant data on the doctor. Keep demographic metadata as concise as possible.
* **Strict Rule**: Subtext directly under patient names in all cards, queues, and detail screens must **strictly contain ONLY age and gender**:
  * Format: `[Age] Yrs • [Gender]` (e.g., `31 Yrs • Female`, `34 Yrs • Male`).
  * **DO NOT** append phone numbers, consultation types (`Initial`/`Follow Up`), or timestamps to the name subtext.

### 16.2 Strict Separation of "Type" vs "Status"
* **"STATUS" Field**: Shows the lifecycle state of the appointment (`In Queue`, `In Call`, `Draft Rx`, `Prescribed`, `Skipped`).
* **"TYPE" Field**: Shows the clinical consultation type (`Initial` or `Follow Up`).
* **Rule**: Updating the appointment lifecycle state (`status`) must **never overwrite or alter** the clinical consultation `type`. The "Type" column in the 3-column info grid must always cleanly display `Initial` or `Follow Up`.

---

## 17. Sequential Queue Flow & Current Turn Highlighting Standard

### 17.1 No Arbitrary Calls or Manual Recalls
* **No "Start Call" from Details**: Doctors cannot arbitrarily start calls with any upcoming queued patient out of order. Calls proceed sequentially through the active shift queue.
* **No Manual Patient Recall**: Doctors do not manually recall skipped patients. When a skipped patient returns, they mark themselves present in their patient app, and the system automatically requeues them.

### 17.2 "Turn Now" & "In Call" Highlighting on All Appointments Screen
* **Active Turn Recognition**: When a shift is ongoing (`isShiftActive`), the patient currently at the front of the queue (`queuePatients[currentPatientIndex]`) is clearly highlighted on the All Appointments list:
  * **Card Styling**: Adds `.is-current-turn` with soft sage highlight (`background: #f4f9f8; border-color: var(--color-border-selected); box-shadow: 0 3px 12px rgba(126, 184, 174, 0.16);`).
  * **Serial Box**: Styled with `.status-in-call` sage pill.
  * **Badge Indicator**:
    * If waiting on Desk to join: `<span class="appt-status-badge in-call"><span class="status-dot-pulse"></span> Turn Now</span>`
    * If video call is active: `<span class="appt-status-badge in-call"><span class="status-dot-pulse"></span> In Call</span>`

---

## 18. All Appointments Screen Architecture & Filter Standard

### 18.1 History vs Upcoming Semantic Separation & Punchy Date Pills
* **Upcoming Tab**:
  * Displays upcoming / in-progress shifts starting from **Today** (all queued, in-call, and draft Rx visits) through future dates (`Tomorrow`, `1 Oct`).
  * Concise Date Pills: `All`, `Today`, `Tomorrow`, `1 Oct`.
* **History Tab**:
  * Displays finished consultations starting from **Today** (strictly visits with status `prescribed` or `skipped`) followed chronologically backwards through past dates (`Yesterday`, `27 Sep`).
  * Never contains future dates.
  * Concise Date Pills: `All`, `Today`, `Yesterday`, `27 Sep`.

### 18.2 Clean Hierarchical Grouping (Date -> Shift -> Patient Cards)
* **No Cluttered Long String Headers**: Headers never concatenate date + shift + full time range into a multi-line wrapping string (e.g. avoid `🕒 Yesterday, Sept 28 · Shift 1 · 9:00 AM – 11:00 AM`).
* **Visual Hierarchy**:
  * **Primary Date Header**: `Yesterday, Sept 28` with total patient count `5 Patients` (shown when viewing "All").
  * **Shift Sub-Header**: `Shift 1 • 9:00–11:00 AM` with capacity badge `4 Patients`.
  * **Patient Cards**: `flex: 1` text container allowing full patient names to render cleanly without premature ellipsis.

### 18.3 Interactive Filter Bottom Sheet Modal (`#apptFilterModalSheet`)
* **Contextual Options**:
  * **Upcoming**: Status (`All`, `In Queue`, `In Call / Next`, `Draft Rx`), Consultation Type (`All`, `Initial`, `Follow Up`), Shift (`All`, `Shift 1`, `Shift 2`).
  * **History**: Status (`All`, `Prescribed`, `Skipped`), Consultation Type (`All`, `Initial`, `Follow Up`), Shift (`All`, `Shift 1`, `Shift 2`).
* **Active Indicator Dot**: Displays a subtle teal active dot (`.filter-active-dot`) on the top filter icon button whenever any non-default filter is applied.

### 18.4 Sub-View Elevation (Clean Screen Bottom)
* **Bottom Nav Isolation**: Sub-views with top back navigation (e.g. `All Appointments`, `Appointment Details`) elevate with `z-index: 21` and `padding-bottom: 36px`, giving the appointment list complete visual breathing room without being crowded by the 5-tab bottom navigation bar.

---

## 19. App-Wide Wise & Uber iOS Minimalism Standard

### 19.1 Canvas & Surface Tokens
* **App Canvas**: Pure crisp white `#FFFFFF` across all root pages.
* **Surface Cards**: Soft neutral surface `#F6F8F9` with `1.5px solid #EDF2F1` borders, subtle `border-radius: 16px` to `18px`.
* **Hover / Tap States**: Elevates to `background: var(--color-card-neutral-hover) (#EEF2F4)` for micro-responsive tactile feedback.

### 19.2 Zero Nested Boxes ("No Boxes Inside Boxes")
* **Principle**: All screens avoid wrapping cards within cards. Lists (prescriptions, investigations, appointments, documents, saved shifts) use flat, distinct single-layer rows on the white canvas.
* **Section Separation**: Strict uniform `24px` (`--spacing-section`) between major logical sections, with `10px` (`--spacing-element`) between child items.

### 19.3 Modal Bottom Sheet Standard
* **Fluid Drag Grabber**: Every modal bottom sheet features a standard iOS drag pill (`width: 38px; height: 4.5px; border-radius: 100px; background: #CBD5E1;`).
* **Radius & Shadow**: `border-radius: 32px 32px 0 0` with high-blur backdrop (`backdrop-filter: blur(8px)`).
* **High-Contrast Editorial Typography**: Confident titles (`Urbanist 24px–32px Bold`) with quiet subtitles (`DM Sans 13.5px–14px #64748B`).

### 19.4 Scannability for Doctors
* **Minimalist Subtext**: Strictly limited to key demographics (`[Age] Yrs • [Gender]`).
* **Fast Decision Making**: High-impact primary action buttons (full width or docked) so busy practitioners can complete consultations and review clinical notes with minimal cognitive load.

### 19.5 Destructive Action Confirmation Standard (Shift Deletion & Item Removal)
* **Never Delete Instantly**: All destructive actions (e.g. deleting a shift slot in Schedule or removing medications/investigations) must prompt the doctor with a confirmation bottom sheet modal (`#deleteConfirmModalSheet`).
* **Editorial Modal Structure**:
  * Danger badge icon (`<i class="ph ph-trash"></i>`).
  * Explicit confirmation title (e.g. `Delete Shift 1?`, `Delete Medicine?`).
  * Contextual subtitle explaining the consequence (e.g. `This shift will be removed from your scheduled hours.`).
  * Paired actions: Neutral `Cancel` and bold red `Delete` CTA (`.btn-sheet-danger-confirm`).
* **Feedback**: Smooth micro-exit animation (`opacity: 0, scale: 0.95`) followed by a concise toast confirmation (e.g. `Shift 1 deleted`).

### 19.6 Consultation Notes vs. Pre-Visit Intake Card Hierarchy & Universal Information Chips
* **Clinical Principle**: Once a consultation is concluded, the doctor's **Consultation Notes** represent the primary clinical outcome and must have highest visual priority, while the patient's **Pre-visit Intake** represents background history and should use a soft, warm neutral tone to avoid cognitive confusion.
* **Universal Information Chip System (`.info-chip`)**:
  - **Shared Geometry Rule**: Every information chip across all section headers shares the exact same height (`24px`), identical padding (`0 9px`), identical corner radius (`8px`), and typography (`Urbanist 11px Bold`, uppercase `letter-spacing: 0.02em`).
  - **Variants**:
    * `.info-chip-sage`: `background: #E8F6F3; color: #0D7A5F; border: 1px solid #C2E7DF;` (e.g. `✨ Live AI Notes`).
    * `.info-chip-warm`: `background: #FEF3C7; color: #92400E; border: 1px solid #FDE68A;` (e.g. `Patient Intake`).
    * `.info-chip-neutral`: `background: #F1F5F9; color: #475569; border: 1px solid #E2E8F0;` (e.g. `[N] Files`, `Not Submitted`).
* **Consultation Notes Card (`.details-notes-card`)**:
  * Surface: Crisp, high-clarity mint/sage tint (`background: #F4F8F7`, `border: 1.5px solid #D1E5E1`, `16px` radius).
  * Typography: Deep forest clinical copy (`#0F2F29`, `13.5px Medium`, `line-height: 1.55`).
  * Header Chip: `<span class="info-chip info-chip-sage">✨ Live AI Notes</span>`.
* **Pre-Visit Details Card (`.details-previsit-card`)**:
  * Surface: Soft warm neutral (`background: #FAF8F5`, `border: 1.5px solid #EFE5D6`, `16px` radius).
  * Symptom Title: Displays the specific chief complaint / issue discussed during patient AI triage (e.g. `Sore Throat & Mild Fever`, `Seasonal Allergies & Runny Nose`, `Acid Reflux & Heartburn`), never generic placeholders like `Video Consultation Follow-up`.
  * Meta Row: Shows duration and severity (e.g. `Duration: 3 Days • Severity: Mild (3/10)`).
  * Quote Container (`.details-previsit-quote`): White inner card with warm amber left indicator (`border-left: 3px solid #D97706`, `border: 1px solid #EFE4D4`) and warm brown quote text (`#4A3B2C`) displaying the conversational statement the patient provided to the Onu AI assistant.
  * Header Chip: `<span class="info-chip info-chip-warm">Patient Intake</span>` or `<span class="info-chip info-chip-neutral">Not Submitted</span>` if intake was omitted.
* **Prescription Header**:
  * Clean section title `Issued Prescription` with **no `Signed` badge or tab** anywhere on the screen.
* **No Redundant Bottom Dock for Completed Visits**:
  * For completed/prescribed visit details, the bottom dock button is removed because the **Issued Prescription** card already contains a direct `View Rx` button on top of the page. Fixed bottom dock CTAs are reserved strictly for active actions (e.g. `Review & Finalize Rx` for Draft Rx, `Re-join Active Call` for In Call).

### 19.7 Pre-Shift Locked State & 2-Minute Unlock Protocol
* **Clinical Principle**: Shift serial calls cannot be triggered prematurely before the scheduled time window. The calling room and live queue unlock strictly **2 minutes before shift start** (e.g., at 8:58 AM for a 9:00 AM shift).
* **Pre-Shift Locked State (> 2 mins before start, e.g. 8:22 AM)**:
  * **Card Surface**: Standard neutral card (`--color-card-neutral`: `#F6F8F9`, `1.5px solid #EDF2F1`) so it stays subdued, quiet, and does not command false urgency.
  * **Badge**: `<span class="badge-pill-light"><i class="ph ph-lock-key"></i> Shift 1 (9:00 AM)</span>` + `6 in Queue` (white badges with `#E2ECEA` border).
  * **Card Title**: `Shift Starts at 9:00 AM`.
  * **Subtext**: `"Calling room unlocks at 8:58 AM (2 mins before shift)"`.
  * **Button**: `.btn-hero-locked` (white background, `#64748B` text, lock icon) `🔒 Shift Locked Until 8:58 AM`.
* **Ready to Start State (2 mins before start, e.g. 8:58 AM)**:
  * **Card Surface**: Transforms into vibrant active Sage (`--color-card-sage`: `#D6EAE6`), creating an immediate, unmistakable visual cue that the shift is ready.
  * **Badge**: `Shift 1 Ready` + `6 in Queue`.
  * **Card Title**: `Start Shift 1`.
  * **Subtext**: `9:00 AM – 11:00 AM • 6 Patients Waiting` (does NOT prematurely show individual patient demographics because full patient viewing starts on the next page).
  * **Button**: `.btn-hero-action` with `<i class="ph-fill ph-play"></i> Start Shift 1` (`#052E28`).
  * **Seamless Consultation Launch**: Tapping `Start Shift 1` immediately opens the full-screen Video Consultation view (`#pageVideoCall`), where the first queued patient's demographics, vitals, and live stream are presented.
* **Interactive Demo Capability**: Tapping the locked button immediately simulates fast-forwarding to 8:58 AM with a smooth micro-animation. Tapping the top clock time (`#statusClockTime`) toggles back and forth between Locked (`8:22 AM`) and Ready (`8:58 AM`) for seamless presentation.

### 19.8 Doctor Offline Subtle Red Alert Standard
* **Purpose**: Signal abnormal / paused clinic state without overwhelming the doctor with jarring alarm colors.
* **Tokens Applied**:
  * **Card Surface**: Very soft blush surface (`#FEFAF9`) with gentle rose border (`1.5px solid #FECDCA`).
  * **Icon Pill**: Soft rose container (`background: #FEF3F2; border: 1px solid #FECDCA;`) with warm red moon icon (`color: #D92D20;`).
  * **Status Tag**: Pill badge (`background: #FEF3F2; border: 1px solid #FECDCA; color: #B42318;`) with a subtle 6px pulsing red status dot.
  * **Top Toggle & Meta**: Label shows `"Doctor Offline"` with a 6px red status indicator dot, and section meta displays `"Shift Paused"` in `#D92D20`.

### 19.9 Offline Auto-Cancellation & All Appointments Queue Handling
* **Clinical Principle**: When a doctor confirms going offline (e.g. for Rest of Today, Next 3 Days, or 1 Week), all booked patient appointments falling within that duration are automatically cancelled and patients receive 1-tap rebooking links.
* **All Appointments Behavior**:
  * **Upcoming Tab**: Days within the offline duration (e.g., `Today`) do not show queued patients because their slots are cancelled.
  * **Contextual Empty State**: If viewing a cancelled day (e.g. `Today`) in Upcoming while offline, the screen renders an informative empty state:
    * Red moon icon (`#D92D20`).
    * Title: `Doctor is Offline`.
    * Subtext: `"Today's appointments were cancelled because you are offline (Rest of Today). Patients were notified to rebook."`
  * **Restoring Queue**: When the doctor toggles back online, the shifts resume and appointments list updates immediately.

---

## 20. My Patients Directory & Patient Profile Redesign Standard

### 20.1 My Patients Directory Screen (`#pagePatientsList`)
* **Purpose**: Provide the doctor with an instantaneous, searchable directory of every patient consulted once or multiple times across all historical and current shifts.
* **Header & Top Brand**:
  * Title: `My Patients` (`Urbanist 25px Bold #000000`, letter-spacing `-0.02em`).
  * Subtitle: `Your patient directory & history` (`DM Sans 13.5px #717171`).
  * *No notification bell* on the My Patients tab (clean, focused layout).
* **Search & Filter Controls**:
  * Unified search input (`#inputPatientsSearch`): Live real-time search matching patient names, ID numbers, or phone numbers (`DM Sans 13.5px Medium` in `#F6F8F9` container with `1.5px solid #EDF2F1`).
  * Filter button: `48px × 48px` neutral square button (`1.5px solid #EDF2F1`) with `ph-sliders-horizontal`.
* **Clinical Metrics Overview Box for Doctor (`.patient-metrics-card`)**:
  * Modern, typography-first 3-column split card in soft sage tint (`#EFF7F5`, border `1.5px solid #D4EAE4`, `18px` radius):
    * `Total Patients`: `8` (Value: `Urbanist 22px Bold #052E28`, Label: `DM Sans 11.5px SemiBold #4A6E67`)
    * `Consultations`: `24`
    * `Repeat Rate`: `62%`
    * Dividers: Minimal `1px solid #D0E5E0` vertical dividers.
  * Sleek, high-end European healthtech presentation without clunky icon circles, with values accurately matching the directory records.
* **All Patients Section Header (`.section-text-group`)**:
  * Title: `All Patients` (`Urbanist 20px Bold #000000`, letter-spacing `-0.02em`).
  * Subtext: `8 Patients` (`DM Sans 13px #717171`).
  * Follows the exact universal typography standard used by top headers (Urbanist Title + DM Sans Subtext in `#717171`), scaled contextually for secondary section headers.
* **Patient Directory List Items**:
  * Flat, clean neutral surface `#F6F8F9` with `1.5px solid #EDF2F1` border and `16px` radius.
  * Initials Avatar: `44px × 44px` circular pastel sage badge (`#E8F4F1`, `1px solid #D1E5E1`) with bold initials in `#052E28`.
  * Minimalist Subtext: Strictly formatted as `[X] Visits` (e.g. `4 Visits` or `1 Visit`) in `DM Sans 12px #717171`. Ultra-clean, zero visual clutter, no patient IDs or dates.
  * Trailing Chevron: `<i class="ph ph-caret-right" style="color: #94a3b8; font-size: 16px;"></i>`.

### 20.2 Patient Profile Screen (`#pagePatientProfile`)
* **Elevation & Top Navigation**:
  * Full-screen subview with top sticky header (`.patient-profile-top-bar`) containing:
    * Left cluster: Circular back button (`btn-circle-icon` with `ph-arrow-left`) + Page title `Patient Profile` (`Urbanist 22px Bold #000000`).
    * Right cluster: Circular phone call button (`btn-circle-icon` with `ph-phone-call`).
* **Patient Hero Card**:
  * Neutral surface `#F6F8F9` with `1.5px solid #EDF2F1` border and `18px` radius.
  * Circular Initials Avatar (`52px × 52px` in `#E8F4F1` with `1.5px solid #D1E5E1`).
  * Name: `Urbanist 18px Bold #000000`.
  * Demographics: `[Age] Yrs • [Gender]` (e.g. `28 Yrs • Male`). Clean, human-centered without patient ID.
  * Phone Link: Interactive phone number with phone icon in `#052E28`.
* **Patient Info & Vitals Card**:
  * Header: `Patient Info` (`Urbanist 19px Bold #000000`).
  * Vitals Container (`.profile-vitals-card`): Neutral card `#F6F8F9` with 2-column grid (`Age`, `Gender`, `Visits`, `Blood`, `Weight`, `Height`).
  * Each vital item features a crisp white circular icon bubble (`36px × 36px`, `1px solid #E2ECEA`), uppercase 10px label (`DM Sans 10px Bold #717171`), and bold value (`Urbanist 14px Bold #000000`).
* **Visits Log Section (Max 3 Default + Inline "See All" Expansion)**:
  * Header: `Visits Log` + count subtitle (e.g. `4 visits`).
  * Default View: Displays at most the 3 most recent visits.
  * Visit Tiles: `#F6F8F9` surface with circular icon bubble (`38px × 38px`), Date (`Urbanist 14px Bold`), Subtitle (`DM Sans 12px #717171`), and chevron `>`.
  * **Interactive Tap Flow**: Tapping any past visit tile opens the **Visit Details (`#pageAppointmentDetails`)** view for that visit with full consultation notes, issued prescription, and pre-visit details. The top back button returns cleanly to the Patient Profile.
  * Inline Expansion Action: If a patient has >3 visits, a clean pill button `.btn-see-all-visits` (`See all [N] visits` with `ph-caret-down`) is rendered below the 3rd visit. Tapping expands all visits inline and turns into `Show less` with `ph-caret-up`.
* **Completed & Prescribed Visit Meta Card Transformation**:
  * For **Patient Visit Log Details** and **Completed / Prescribed Appointments**: The 3-box `Status / Serial / Type` strip is replaced by the unified `.visit-details-meta-card`:
    * Top row: `● COMPLETED` green badge + consultation mode & duration pill (e.g. `[video camera icon] Video Call • 25 Mins`).
    * Bottom row: Consultation date (`[calendar icon] Aug 20, 2026`) + call time (`[clock icon] 08:00 PM`).
  * For **Upcoming / Queued / Draft Rx / Skipped Appointments**: Retains the 3-box `Status / Serial / Type` info strip.
* **Files Section Removal**:
  * The dedicated Files section has been completely removed from the Patient Profile. Consultation documents and prescriptions are attached to specific appointment records, maintaining a clean, scannable profile.

---

## 21. Universal Bottom Navigation Bar System

### 21.1 Selected vs. Unselected Tab Rule (Strict Master Standard)
* **Docked Container**: Floating pill docked at viewport bottom (`height: 58px`, `background: #FFFFFF`, `border: 1.5px solid #EDF4F2`, `border-radius: 28px`, `box-shadow: 0 4px 20px rgba(0, 0, 0, 0.04)`).
* **Selected Tab**:
  * Rendered inside a soft rounded pastel pill (`.active-nav-pill`: `width: 44px`, `height: 38px`, `border-radius: 12px`, `background: #EFF7F5`).
  * Features the **filled icon** (`ph-fill ph-[icon]`) in deep forest green (`#052E28`).
  * Displays a subtle horizontal indicator line below the icon (`width: 18px`, `height: 2.5px`, `background: #A3D4C9`, `border-radius: 4px`).
  * **NO text title/label** when selected (decluttered, hyper-focused).
* **Unselected Tabs**:
  * Features the **outline icon** (`ph ph-[icon]`) in `#717171` (`font-size: 21px`).
  * Displays the text title/label beneath the icon in `DM Sans 11px Medium #717171` (`Desk`, `Patients`, `Onu`, `Wallet`, `Profile`).
* **Interactive State Management**:
  * Handled autonomously via `setActiveNavTab(tabName)` in JavaScript, ensuring seamless synchronization across all pages now and in the future.

---

## 22. Onu Clinical AI Copilot & Unified Screen Standard

### 22.1 Default Landing & Gemini Ambient Brand Gradient
* **Default Active View**: When the doctor opens the app, **Onu (`#pageOnu`)** is the default active view (`.active-page`), and the bottom navigation bar selects the center **Onu** tab.
* **Ambient Brand Gradient**: Luminous, subtle multi-point radial gradient inspired by Google Gemini, crafted with Onu's signature sage, mint, and aquamarine palette:
  * Center aura: `rgba(214, 234, 230, 0.75)` (Soft Sage) fading gently to `rgba(232, 246, 243, 0.5)` and white.
  * Top-right ambient highlight: `rgba(204, 251, 241, 0.5)` (Soft Aquamarine).
  * Bottom-left ambient tint: `rgba(239, 247, 245, 0.7)`.
  * **Dynamic Chat Transition**: Smoothly transitions to pure `#FFFFFF` as soon as the doctor starts a chat session (`.page-onu.chat-active`).
* **Unified Universal App Header**:
  * **Left**: Screen Title `Onu` in `Urbanist 25px Bold #000000` + Subtitle `Your Clinical AI Assistant` in `DM Sans 13.5px Regular #717171`.
  * **Right**: Circular action button (`.btn-circle-icon` with `ph-clock-counter-clockwise` in `#052E28` on soft `#F0F6F5` background) positioned on the top right for natural right-handed mobile thumb access.
  * **Right-Hand History Drawer**: Tapping the top-right history icon slides out the full-height chat thread history drawer (`#onuHistoryDrawer`) from the right.

### 22.2 Welcome State (Gemini Pure Clean Empty State)
* **Design Philosophy**: Mirroring Google Gemini's minimalist mobile experience with generous negative space and zero cluttered cards or suggestion grids.
* **Centered Sparkle & Refined Greeting**:
  * **Gradient Sparkle Icon**: Clean 4-point star SVG with emerald-teal-sky gradient (`#0D7A5F` → `#2DD4BF` → `#38BDF8`) and soft ambient drop shadow (`0 4px 14px rgba(13, 122, 95, 0.25)`).
  * **Refined Greeting Heading**: `Ask away, Dr. Sifat !` in `Urbanist 21px SemiBold #0F172A` (`letter-spacing: -0.015em`, lighter and more elegant than heavy bold).
  * **Greeting Subtitle**: `Your clinical AI copilot is ready.` in `DM Sans 13.5px Regular #64748B`.

### 22.3 Conversational Feed & Realistic Clinical AI Intelligence
* **User Messages**: Rounded speech bubble (`#EEF2F4` surface, `#0F172A` text, `20px` radius, `14.5px` body) with micro-actions for Copy and Edit.
* **Onu AI Responses**: Collapsible reasoning indicators (`● Thought for 2-4 seconds`), clean high-contrast clinical text, and structured metric overview cards when relevant (without extra action chips).
* **Realistic Clinical Knowledge Engine (`generateOnuClinicalResponse`)**:
  * **Clinical Conditions**: Dedicated evidence-based protocols for Hypertension (AHA/ACC targets & first-line agents), Diabetes (ADA HbA1c goals & Metformin/SGLT2i), Cephalalgia/Headaches (SNOOP4 red flags & acute abortive therapies), and Fever/Infections (antipyretics, hydration, CBC/CRP lab stewardship).
  * **Practice Intelligence Fallback**: For any general or freeform typed query, Onu provides realistic clinical context connecting the query to active queue patients (Farzana Khan, Alif Khan, Tariqul Islam) with diagnostic considerations and safe medication guidance instead of generic robotic fallbacks.

### 22.4 Floating Input Dock (Google Gemini Unified Pill Model)
* **Dock Position**: Floats above the bottom navigation bar (`position: absolute; bottom: 64px; left: 0; right: 0;`).
* **Single Unified Input Pill Container (`.onu-input-pill-box`)**:
  * Height `52px`, `background: #FFFFFF`, `border: 1.5px solid #E2ECEA`, `border-radius: 28px`, `box-shadow: 0 4px 20px rgba(5, 46, 40, 0.08)`.
  * **Left**: `+` Attach/Tag button (`.btn-onu-attach` with `ph-plus`).
  * **Center**: Text input field (`Ask anything...` placeholder in `DM Sans 15px`).
  * **Right**: Speech-to-Text dictation mic button (`.btn-onu-mic` with `ph-microphone`).
  * **Far Right Action (Morphing Voice Bot / Send Button)**:
    * **Empty Input State (Voice Mode)**: Displays a circular soft sage pill button (`.btn-onu-action-morph.voice-mode`: `#E8F6F3` background, `#0D7A5F` waveform icon `ph-waveform`). Tapping immediately opens the full-screen **Live AI Voice Bot Modal (`#modalLiveVoiceBot`)**.
    * **Active Typing State (Send Mode)**: Smoothly morphs into a deep forest green circular Send button (`.btn-onu-action-morph.send-mode`: `#052E28` background, `#FFFFFF` crisp arrow `ph-bold ph-arrow-up`). Tapping sends the message to Onu.
* **Subtle AI Disclaimer**: `Onubot can make mistakes. Check important info.` (`DM Sans 10px #94A3B8`).

