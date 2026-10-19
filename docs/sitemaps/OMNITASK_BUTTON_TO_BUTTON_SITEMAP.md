# OmniTask OS — Master Button-to-Button Sitemap & Interactive Flow

> **Version:** 2.4 Pro  
> **Architecture:** Responsive Cross-Platform (Mobile Phone, Tablet, Laptop, Desktop)  
> **Status:** Production Ready & Verified (0 missing functions, 0 missing DOM IDs)  

---

## 1. System Navigation Architecture & Screen Flow

```mermaid
flowchart TD
    Login["🚪 Page 0: Login & Persona Gateway (#loginScreen)"] -->|Unlock / Continue as Guest| Home["🏠 Page 1: Home Dashboard & Calendar (#view_home)"]
    
    %% Primary Navigation Links
    Home -->|Sidebar / Bottom Nav| Cal["📅 Page 2: Expanded Weekly Calendar (#view_calendar)"]
    Home -->|Sidebar / Bottom Nav| Meds["💊 Page 3: Medications & Refill Radar (#view_reminders)"]
    Home -->|Sidebar / Bottom Nav| Spend["💳 Page 4: Expenses & Salary Ledger (#view_expense)"]
    Home -->|Sidebar / Bottom Nav| Fit["🏋️ Page 5: Fitness & Habits (#view_fitness)"]
    Home -->|Sidebar / Bottom Nav| Family["🛡️ Page 6: Household Oversight (#view_oversight)"]
    Home -->|Sidebar / Bottom Nav| Insights["📊 Page 7: Insights & Health Analytics (#view_insights)"]

    %% Core Actions from Home
    Home -->|＋ Quick Add| M1["➕ Quick Ingestion Modal (#quickAddModal)"]
    Home -->|Pay Now| Spend
    Home -->|Routine →| Fit
    Home -->|View all →| Meds

    %% Actions from Calendar
    Cal -->|📅 View Dashboard Calendar| Home
    Cal -->|➕ Add Event| M1
    Cal -->|Today| Cal

    %% Actions from Medications
    Meds -->|✏️ Edit Dose / Refill| M5["💊 Edit Dose & Refills Modal (#editDoseModal)"]
    Meds -->|➕ Add Medication| M1
    Meds -->|Take Dose| Meds

    %% Actions from Expenses
    Spend -->|✏️ Edit Monthly Salary| M2["💰 Monthly Salary Setup Modal (#salaryModal)"]
    Spend -->|📷 Scan Bill| M6["📷 Vision OCR Bill Scanner (#billScanModal)"]
    Spend -->|➕ Add Bill| M1
    M6 -->|Verified View| M7["🖼️ Receipt Viewer Modal (#receiptViewModal)"]
    Spend -->|💳 Pay Now| Spend
    Spend -->|💾 Export CSV| CSV["💾 Download expenses.csv"]

    %% Global Emergency SOS
    Anywhere["🚨 Any Screen (#floatingSosBtn)"] -->|🚨 EMERGENCY SOS| M8["🚨 Emergency SOS & Medical ID (#sosModal)"]
    M8 -->|📞 Call 911 / Call John| Bridge["📞 Phone Bridge / 911 Dispatch"]

    %% Senior Mode Actions
    Home -->|👵 Senior Mode -> 🔒 Pause| M9["🔒 Senior Privacy Pause Modal (#privacyPauseModal)"]
    Home -->|👵 Senior Mode -> 🗣️ Read| TTS["🔊 Web Speech TTS Audio Engine"]

    %% Family Hub & Security Settings
    Anywhere -->|Family Hub / Settings| M3["👨‍👩‍👧 Family Circle & PIN Modal (#familySettingsModal)"]

    %% Task Editing
    Home -->|Calendar Day Item Pencil| M4["✏️ Task / Event Editor Modal (#editModal)"]

    %% Logout & Switch Account
    Anywhere -->|Profile Dropdown -> 🚪 Sign Out| Login
```

---

## 2. Exhaustive Button-to-Button Matrix (17 Functional Screens & States)

### Gateway & Authentication
| # | Screen Name | DOM Container | How to Arrive (Incoming Buttons) | Outgoing Buttons & Actions |
|---|---|---|---|---|
| **0** | **Login & Persona Gateway** | `#loginScreen` | • Top simulation banner: `🚪 Switch Account / Login Gateway`<br>• User profile menu: `🚪 Sign Out / Switch User` | • `🚀 Continue as Guest` ➔ Enters Dashboard (Page 1) as Guest<br>• `🔑 Access Vault & Dashboard` ➔ Enters Dashboard in selected persona<br>• Persona cards (`👤 Aswin`, `👵 Eleanor`, `🛡️ John`) ➔ Switches active profile |

---

### Primary Tab Pages (The 7 Core Views)
| # | Screen Name | DOM Container | How to Arrive (Incoming Buttons) | Outgoing Buttons & Actions |
|---|---|---|---|---|
| **1** | **Home Dashboard & Centerpiece Calendar** | `#view_home` | • Sidebar: `Home` (`#sideBtn_home`)<br>• Bottom nav: `Home` (`#mobBtn_home`)<br>• Topbar logo brand click<br>• Calendar page: `📅 View Dashboard Calendar` | • `◀` / `▶` ➔ Previous / Next Calendar Month<br>• `Today` ➔ Snaps calendar to today<br>• `Month` / `Week` / `Day` ➔ Toggles calendar view format<br>• Calendar Day Cell ➔ Focuses date & slides agenda with `.timeline-swap`<br>• `＋ Quick Add` ➔ Opens Speed-Dial Quick Ingestion Modal<br>• `💊 Med Log` ➔ Switches to Medications Hub<br>• `Pay Now` ➔ Switches to Expenses Hub<br>• `Routine →` ➔ Switches to Fitness Hub<br>• `View all →` ➔ Switches to Medications Hub<br>• Bento Status Tiles ➔ Deep-links to Spend, Fitness, or Household |
| **2** | **Expanded Weekly Calendar** | `#view_calendar` | • Sidebar: `Calendar` (`#sideBtn_calendar`)<br>• Bottom nav: `Calendar` (`#mobBtn_calendar`) | • `📅 View Dashboard Calendar` ➔ Jumps to Home Dashboard (Page 1)<br>• `Today` ➔ Snaps view to today<br>• `➕ Add Event` ➔ Opens Quick Ingestion Modal<br>• Hourly event pills ➔ Deep-link to Medications, Expenses, or Fitness |
| **3** | **Medications & Prescriptions Hub** | `#view_reminders` | • Sidebar: `Medications` (`#sideBtn_reminders`)<br>• Bottom nav: `Meds` (`#mobBtn_reminders`)<br>• Hero button: `💊 Med Log`<br>• Dashboard medications card: `View all →` | • `💊 Take Dose` ➔ Increments day count & triggers adherence sound<br>• `✏️` (Pencil button) ➔ Opens Prescription Dose & Refill Editor Modal<br>• `➕ Add Rx` ➔ Opens Quick Add Modal for Prescriptions<br>• `↺ Undo` ➔ Reverts last taken dose |
| **4** | **Expenses & Budget Ledger** | `#view_expense` | • Sidebar: `Expenses & Bills` (`#sideBtn_expense`)<br>• Bottom nav: `Spend` (`#mobBtn_expense`)<br>• Today's spend card: `Pay Now` | • `✏️ Edit Monthly Salary` ➔ Opens Monthly Salary Setup Modal<br>• `📷 Scan Bill` ➔ Opens Vision OCR Bill Scanner Modal<br>• `➕ Add Bill` ➔ Opens Quick Ingestion Modal for Bills<br>• Category pills (`All`, `Utility`, `Food`, `Travel`, `Household`, `Medical`) ➔ Filters ledger<br>• `💳 Pay Now` ➔ Reconciles bill, records expense, and auto-links<br>• `📷 View Photo` ➔ Opens High-Res Verified Receipt Viewer Modal<br>• `💾 Export CSV` ➔ Generates and downloads `expenses.csv` |
| **5** | **Fitness & Habits Hub** | `#view_fitness` | • Sidebar: `Fitness & Habits` (`#sideBtn_fitness`)<br>• Dashboard bento tile: `Fitness & Habits`<br>• Motivational botanical card: `Routine →` | • `✓ Complete Workout` ➔ Marks workout done & increases weekly streak<br>• `+1 Log` ➔ Increments emoji habit count & animates streak flame<br>• `➕ Add Routine` ➔ Opens Quick Add Modal for workouts |
| **6** | **Household Oversight Command Center** | `#view_oversight` | • Sidebar: `Household` (`#sideBtn_oversight`)<br>• Topbar: `Family Hub` (`#btnHeaderFamily`)<br>• Scenic hero chips (`Eleanor Vance`, `John Vance`)<br>• User profile dropdown: `🛡️ Household Oversight Hub` | • `📞 Call Eleanor` ➔ Connects caregiver phone bridge<br>• `+ Add Member` ➔ Opens Family Circle Modal<br>• Dignity controls ➔ Adjusts senior high-contrast typography |
| **7** | **Insights & Health Analytics** | `#view_insights` | • Sidebar: `Insights` (`#sideBtn_insights`)<br>• User profile dropdown: `📋 Doctor Visit Summary (PDF)` | • `📄 Export Summary` ➔ Prepares and prints clinician PDF report<br>• `💾 Export CSV` ➔ Exports full audit dataset |

---

### Specialized Persona Cockpit Modes
| Mode | Trigger | UI Manifestation |
|---|---|---|
| **Power User Mode** | Topbar pill `#btnRolePower` | Wide multi-column layout, interactive split calendar, quick ingestion tools, and advanced financial velocity meters. |
| **Senior Dignity Mode** | Topbar pill `#btnRoleSenior` | Hides complex multi-column bento grids; activates `#seniorTabletCockpit` with **24pt+ typography**, **56dp touch buttons**, giant pill cards, digital clock, **"🗣️ Read Schedule"** audio readout, and **"🔒 Pause Tracking"**. |
| **Caregiver Mode** | Topbar pill `#btnRoleCaregiver` | Activates `#caregiverBar` and `#caregiverTelemetryCockpit` with live compliance status, dose escalation ladders, and audit logs for Eleanor Vance. |

---

### The 9 Action & Tool Modals
| Modal Name | DOM ID | How to Trigger (Button) | Actions Inside Modal |
|---|---|---|---|
| **1. Speed-Dial Quick Ingestion** | `#quickAddModal` | `＋ Quick Add`, `➕ Add Event`, `＋ Add Rx`, `＋ Add Bill` | • Select domain (`Pill`, `Bill`, `Expense`, `Fitness`, `Habit`, `Appointment`)<br>• Fill title, category, time, cost/dosage<br>• `Save & Aggregate` ➔ Inserts into calendar and ledger<br>• `✕` ➔ Dismisses modal |
| **2. Monthly Salary Setup** | `#salaryModal` | `✏️ Edit Monthly Salary` (Expenses Hub) | • Preset buttons (`$3,500`, `$5,000`, `$7,500`, `$10,000`)<br>• Custom salary number input<br>• `💾 Save Monthly Income` ➔ Recalculates burn velocity and surplus<br>• `✕` ➔ Cancels |
| **3. Family Circle & PIN Settings** | `#familySettingsModal` | `Family Hub`, `+ Add Member`, `Family Circle (+)` | • Add/edit family members and roles<br>• Set/change 4-digit Senior Dignity PIN<br>• `💾 Save Family Hub Settings` ➔ Updates vault credentials<br>• `✕` ➔ Closes modal |
| **4. Task / Event Cascade Editor** | `#editModal` | Calendar day item pencil icon | • Edit task title, domain, scheduled time<br>• `💾 Save Changes` ➔ Updates aggregated event record<br>• `🗑️ Delete Event` ➔ Removes task and frees schedule<br>• `✕` ➔ Closes editor |
| **5. Prescription Dose & Refill Editor** | `#editDoseModal` | Prescription card pencil icon (`✏️`) | • `+1 Day`, `-1 Day` ➔ Manually corrects intake record<br>• `+5 Total` ➔ Extends prescription duration<br>• `Reset to Day 1` ➔ Restarts full 30-day bottle regimen<br>• `💾 Update Dose Record` ➔ Recomputes radar warnings<br>• `✕` ➔ Closes modal |
| **6. Vision OCR Bill Scanner** | `#billScanModal` | `📷 Scan Bill` (Expenses page) | • `📸 Trigger Camera` ➔ Activates native device camera<br>• `📄 Sample Bill` ➔ Loads high-fidelity mock electric utility bill<br>• Automated OCR vision parser: detects amount, due date, vendor, line items<br>• `✓ Confirm & Link to Ledger` ➔ Reconciles into expense ledger<br>• `✕` ➔ Exits scanner |
| **7. High-Res Receipt Viewer** | `#receiptViewModal` | Line item `📷 View Photo` link | • Full-resolution view of verified OCR capture<br>• `💾 Download Image` ➔ Saves receipt photo<br>• `✕` / backdrop click ➔ Closes viewer |
| **8. Emergency SOS & Medical ID** | `#sosModal` | Floating `🚨 EMERGENCY SOS` button / 1-Tap SOS tile | • `🚨 BROADCAST IMMEDIATE EMERGENCY ALERT` ➔ Fires visual/auditory pulse and alerts family network<br>• `📞 Call 911` ➔ Dials emergency services<br>• `📞 Call Caregiver John` ➔ Voice bridge to caregiver (+1 555-0144)<br>• `📋 Medical ID` ➔ Displays Eleanor's blood type (O+), allergies, and conditions<br>• `✕` ➔ Dismisses emergency window |
| **9. Senior Privacy Pause** | `#privacyPauseModal` | `🔒 Pause Tracking` (Senior Cockpit) | • Duration presets (`15 min`, `30 min`, `1 hour`, `2 hours`)<br>• `Apply Privacy Pause` ➔ Temporarily suspends caregiver telemetry<br>• `Cancel Pause` ➔ Restores live monitoring immediately |

---

## 3. Responsive Navigation Elements

* **Desktop Glass Sidebar (Pinned Left, 250px):** Always accessible on screens ≥ 1025px.
* **Mobile Floating Glass Bottom Navigation (`#mobileBottomNav`):** Fixed bottom nav with 5 touch zones (Home, Calendar, Meds, Spend, More) active on screens ≤ 768px.
* **Mobile Off-Canvas Drawer (`#appSidebar` + `#sidebarBackdrop`):** Glides from left with blurred backdrop; triggered by the topbar hamburger `#mobileMenuToggleBtn` or the bottom nav "More" button `#mobBtn_more`.
* **Floating Emergency SOS Button (`#floatingSosBtn`):** Fixed bottom-right; auto-adjusts elevation (`bottom: 74px`) on mobile devices to float cleanly above the bottom navigation bar.
